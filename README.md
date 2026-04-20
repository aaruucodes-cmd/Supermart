<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SuperMart — Premium Grocery</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Playfair+Display:wght@700;800&display=swap" rel="stylesheet">
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --green:#1a6b3c;--green-light:#e8f5ee;--green-mid:#2d9e5f;--gold:#c9a227;--gold-light:#fdf6e3;
    --dark:#0f1a12;--text:#1c2b20;--text-muted:#5a7060;--border:#e0ece4;--white:#fff;--bg:#f8faf9;
  }
  html{scroll-behavior:smooth}
  body{font-family:'Inter',sans-serif;color:var(--text);background:var(--white);overflow-x:hidden}
  a{text-decoration:none;color:inherit}

  /* NAV */
  nav{position:fixed;top:0;left:0;right:0;z-index:1000;background:rgba(255,255,255,0.95);backdrop-filter:blur(12px);border-bottom:1px solid var(--border);padding:0 5%}
  .nav-inner{display:flex;align-items:center;justify-content:space-between;height:68px;max-width:1200px;margin:0 auto}
  .logo{display:flex;align-items:center;gap:10px;font-weight:800;font-size:1.35rem;color:var(--dark)}
  .logo-icon{width:36px;height:36px;background:var(--green);border-radius:10px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:1.1rem;font-weight:800}
  .logo span{color:var(--green)}
  .nav-links{display:flex;align-items:center;gap:2rem;list-style:none}
  .nav-links a{font-size:0.9rem;font-weight:500;color:var(--text-muted);transition:color 0.2s}
  .nav-links a:hover{color:var(--green)}
  .nav-cta{background:var(--green);color:#fff;padding:10px 22px;border-radius:50px;font-size:0.85rem;font-weight:600;border:none;cursor:pointer;transition:transform 0.2s,background 0.2s}
  .nav-cta:hover{background:#155830;transform:translateY(-1px)}
  .hamburger{display:none;flex-direction:column;gap:5px;cursor:pointer;background:none;border:none;padding:4px}
  .hamburger span{display:block;width:22px;height:2px;background:var(--text);border-radius:2px;transition:0.3s}

  /* HERO */
  .hero{min-height:100vh;background:linear-gradient(135deg,#0f1a12 0%,#1a3a22 50%,#0f2416 100%);display:flex;align-items:center;padding:100px 5% 60px;position:relative;overflow:hidden}
  .hero::before{content:'';position:absolute;inset:0;background:url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%232d9e5f' fill-opacity='0.05'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");pointer-events:none}
  .hero-content{max-width:1200px;margin:0 auto;width:100%;display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center}
  .hero-badge{display:inline-flex;align-items:center;gap:8px;background:rgba(201,162,39,0.15);border:1px solid rgba(201,162,39,0.3);color:var(--gold);padding:8px 16px;border-radius:50px;font-size:0.8rem;font-weight:600;margin-bottom:1.5rem;letter-spacing:0.05em}
  .hero-badge::before{content:'★';font-size:0.75rem}
  h1.hero-title{font-family:'Playfair Display',serif;font-size:clamp(2.2rem,5vw,3.8rem);font-weight:800;color:#fff;line-height:1.15;margin-bottom:1.5rem}
  h1.hero-title span{color:var(--gold)}
  .hero-desc{font-size:1.05rem;color:rgba(255,255,255,0.65);line-height:1.75;margin-bottom:2.5rem;max-width:480px}
  .hero-btns{display:flex;gap:1rem;flex-wrap:wrap}
  .btn-primary{background:var(--green-mid);color:#fff;padding:14px 32px;border-radius:50px;font-weight:600;font-size:0.95rem;cursor:pointer;transition:all 0.2s;border:none;display:inline-flex;align-items:center;gap:8px}
  .btn-primary:hover{background:#27904e;transform:translateY(-2px);box-shadow:0 8px 24px rgba(45,158,95,0.35)}
  .btn-outline{background:transparent;color:#fff;padding:14px 32px;border-radius:50px;font-weight:600;font-size:0.95rem;cursor:pointer;transition:all 0.2s;border:1px solid rgba(255,255,255,0.3)}
  .btn-outline:hover{background:rgba(255,255,255,0.08);border-color:rgba(255,255,255,0.5)}
  .hero-stats{display:flex;gap:2rem;margin-top:3rem;padding-top:2rem;border-top:1px solid rgba(255,255,255,0.1)}
  .stat{text-align:center}
  .stat-num{font-size:1.6rem;font-weight:800;color:#fff}
  .stat-num span{color:var(--gold)}
  .stat-label{font-size:0.78rem;color:rgba(255,255,255,0.5);margin-top:2px;letter-spacing:0.05em;text-transform:uppercase}
  .hero-visual{position:relative;display:flex;align-items:center;justify-content:center}
  .hero-card-main{background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);backdrop-filter:blur(10px);border-radius:24px;padding:2rem;width:100%;max-width:380px}
  .hero-img-box{width:100%;aspect-ratio:1;background:linear-gradient(135deg,rgba(45,158,95,0.2),rgba(26,107,60,0.3));border-radius:16px;display:flex;align-items:center;justify-content:center;font-size:5rem;margin-bottom:1.5rem}
  .hero-card-tag{background:rgba(45,158,95,0.2);color:#7de0a8;font-size:0.75rem;font-weight:600;padding:5px 12px;border-radius:50px;display:inline-block;margin-bottom:0.75rem}
  .hero-card-title{color:#fff;font-weight:700;font-size:1.15rem;margin-bottom:0.5rem}
  .hero-card-price{color:var(--gold);font-size:1.4rem;font-weight:800}
  .hero-card-price span{font-size:0.85rem;color:rgba(255,255,255,0.4);text-decoration:line-through;margin-left:8px;font-weight:400}
  .hero-card-btn{width:100%;background:var(--green-mid);color:#fff;border:none;border-radius:12px;padding:12px;font-weight:600;cursor:pointer;margin-top:1.25rem;transition:background 0.2s}
  .hero-card-btn:hover{background:#27904e}
  .floating-badge{position:absolute;background:#fff;border-radius:16px;padding:12px 16px;box-shadow:0 8px 32px rgba(0,0,0,0.3);display:flex;align-items:center;gap:10px;min-width:160px}
  .floating-badge.top{top:-10px;right:-20px;animation:float 3s ease-in-out infinite}
  .floating-badge.bot{bottom:20px;left:-30px;animation:float 3s ease-in-out infinite 1.5s}
  @keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-8px)}}
  .fb-icon{font-size:1.5rem}
  .fb-text{font-size:0.75rem;font-weight:600;color:var(--dark);line-height:1.3}
  .fb-sub{font-size:0.7rem;color:var(--text-muted);font-weight:400}

  /* SECTION BASE */
  section{padding:80px 5%}
  .section-inner{max-width:1200px;margin:0 auto}
  .section-label{font-size:0.78rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--green);margin-bottom:0.75rem}
  .section-title{font-family:'Playfair Display',serif;font-size:clamp(1.8rem,4vw,2.6rem);font-weight:800;color:var(--dark);line-height:1.25;margin-bottom:1rem}
  .section-desc{font-size:1rem;color:var(--text-muted);max-width:520px;line-height:1.75}
  .section-head{text-align:center;margin-bottom:3.5rem}
  .section-head .section-desc{margin:0 auto}

  /* OFFER BANNER */
  .offer-banner{background:linear-gradient(120deg,#1a6b3c,#2d9e5f);padding:32px 5%;overflow:hidden;position:relative}
  .offer-banner::after{content:'%';position:absolute;right:5%;top:50%;transform:translateY(-50%);font-size:12rem;font-weight:900;color:rgba(255,255,255,0.06);line-height:1;pointer-events:none}
  .offer-inner{max-width:1200px;margin:0 auto;display:flex;align-items:center;justify-content:space-between;gap:2rem;flex-wrap:wrap}
  .offer-text h2{font-family:'Playfair Display',serif;font-size:clamp(1.4rem,3vw,2rem);color:#fff;font-weight:800}
  .offer-text p{color:rgba(255,255,255,0.75);font-size:0.95rem;margin-top:6px}
  .offer-badge{background:var(--gold);color:#fff;font-size:2.5rem;font-weight:900;padding:16px 28px;border-radius:16px;text-align:center;line-height:1}
  .offer-badge small{display:block;font-size:0.75rem;font-weight:600;letter-spacing:0.05em;opacity:0.85}
  .offer-cta{background:#fff;color:var(--green);padding:13px 30px;border-radius:50px;font-weight:700;font-size:0.9rem;cursor:pointer;border:none;transition:all 0.2s;white-space:nowrap}
  .offer-cta:hover{background:var(--gold-light);transform:translateY(-1px)}

  /* CATEGORIES */
  .categories-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:1.25rem}
  .cat-card{background:var(--bg);border:1px solid var(--border);border-radius:20px;padding:1.75rem 1rem;text-align:center;cursor:pointer;transition:all 0.25s;position:relative;overflow:hidden}
  .cat-card::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--green-light),transparent);opacity:0;transition:opacity 0.3s}
  .cat-card:hover{transform:translateY(-4px);border-color:var(--green-mid);box-shadow:0 12px 32px rgba(26,107,60,0.12)}
  .cat-card:hover::before{opacity:1}
  .cat-icon{font-size:2.5rem;margin-bottom:0.75rem;display:block;position:relative}
  .cat-name{font-weight:700;font-size:0.9rem;color:var(--dark);position:relative}
  .cat-count{font-size:0.75rem;color:var(--text-muted);margin-top:4px;position:relative}

  /* PRODUCTS */
  .products-section{background:var(--bg)}
  .products-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(230px,1fr));gap:1.5rem}
  .product-card{background:var(--white);border:1px solid var(--border);border-radius:20px;overflow:hidden;transition:all 0.25s;cursor:pointer}
  .product-card:hover{transform:translateY(-5px);box-shadow:0 16px 48px rgba(0,0,0,0.1);border-color:var(--green-mid)}
  .product-img{width:100%;aspect-ratio:1.2;background:var(--bg);display:flex;align-items:center;justify-content:center;font-size:3.5rem;position:relative}
  .product-badge{position:absolute;top:12px;left:12px;background:var(--green);color:#fff;font-size:0.7rem;font-weight:700;padding:4px 10px;border-radius:50px}
  .product-badge.sale{background:#e53e3e}
  .product-body{padding:1.25rem}
  .product-category{font-size:0.72rem;color:var(--green);font-weight:600;letter-spacing:0.05em;text-transform:uppercase;margin-bottom:5px}
  .product-name{font-weight:700;font-size:0.95rem;color:var(--dark);margin-bottom:8px;line-height:1.35}
  .product-rating{display:flex;align-items:center;gap:5px;margin-bottom:12px}
  .stars{color:var(--gold);font-size:0.8rem}
  .rating-count{font-size:0.75rem;color:var(--text-muted)}
  .product-footer{display:flex;align-items:center;justify-content:space-between}
  .product-price{font-size:1.15rem;font-weight:800;color:var(--dark)}
  .product-price-old{font-size:0.8rem;color:var(--text-muted);text-decoration:line-through;margin-left:6px;font-weight:400}
  .add-btn{background:var(--green);color:#fff;border:none;border-radius:12px;padding:9px 16px;font-size:0.8rem;font-weight:600;cursor:pointer;transition:all 0.2s;display:flex;align-items:center;gap:5px}
  .add-btn:hover{background:#155830;transform:scale(1.05)}

  /* WHY US */
  .why-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1.5rem}
  .why-card{background:var(--white);border:1px solid var(--border);border-radius:20px;padding:2rem 1.5rem;transition:all 0.25s}
  .why-card:hover{border-color:var(--green-mid);box-shadow:0 8px 32px rgba(26,107,60,0.1);transform:translateY(-3px)}
  .why-icon{width:52px;height:52px;background:var(--green-light);border-radius:14px;display:flex;align-items:center;justify-content:center;font-size:1.5rem;margin-bottom:1.25rem}
  .why-title{font-weight:700;font-size:1rem;color:var(--dark);margin-bottom:0.5rem}
  .why-desc{font-size:0.88rem;color:var(--text-muted);line-height:1.65}

  /* TESTIMONIALS */
  .testimonials-section{background:var(--dark)}
  .testimonials-section .section-label{color:#7de0a8}
  .testimonials-section .section-title{color:#fff}
  .testimonials-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:1.5rem}
  .testi-card{background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);border-radius:20px;padding:1.75rem;transition:all 0.25s}
  .testi-card:hover{background:rgba(255,255,255,0.08);border-color:rgba(45,158,95,0.4)}
  .testi-stars{color:var(--gold);font-size:0.9rem;margin-bottom:1rem;letter-spacing:2px}
  .testi-text{color:rgba(255,255,255,0.75);font-size:0.92rem;line-height:1.75;margin-bottom:1.5rem;font-style:italic}
  .testi-author{display:flex;align-items:center;gap:12px}
  .testi-avatar{width:42px;height:42px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:0.9rem;color:#fff}
  .testi-name{font-weight:600;font-size:0.9rem;color:#fff}
  .testi-location{font-size:0.75rem;color:rgba(255,255,255,0.45);margin-top:2px}

  /* FOOTER */
  footer{background:#0a130c;padding:60px 5% 30px}
  .footer-inner{max-width:1200px;margin:0 auto}
  .footer-top{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:3rem;margin-bottom:3rem}
  .footer-brand .logo{margin-bottom:1rem}
  .footer-desc{font-size:0.88rem;color:rgba(255,255,255,0.45);line-height:1.75;max-width:280px;margin-bottom:1.5rem}
  .social-links{display:flex;gap:10px}
  .social-btn{width:36px;height:36px;border-radius:10px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.1);display:flex;align-items:center;justify-content:center;color:rgba(255,255,255,0.5);font-size:0.85rem;cursor:pointer;transition:all 0.2s}
  .social-btn:hover{background:var(--green);color:#fff;border-color:var(--green)}
  .footer-col h4{color:#fff;font-weight:600;font-size:0.9rem;margin-bottom:1.25rem}
  .footer-links{list-style:none;display:flex;flex-direction:column;gap:10px}
  .footer-links a{font-size:0.85rem;color:rgba(255,255,255,0.45);transition:color 0.2s}
  .footer-links a:hover{color:#7de0a8}
  .contact-item{display:flex;align-items:flex-start;gap:10px;margin-bottom:12px}
  .contact-icon{font-size:0.9rem;margin-top:2px;opacity:0.6}
  .contact-text{font-size:0.85rem;color:rgba(255,255,255,0.45);line-height:1.5}
  .footer-bottom{border-top:1px solid rgba(255,255,255,0.08);padding-top:1.5rem;display:flex;align-items:center;justify-content:space-between;flex-wrap:gap:1rem}
  .footer-copy{font-size:0.8rem;color:rgba(255,255,255,0.3)}
  .footer-legal{display:flex;gap:1.5rem}
  .footer-legal a{font-size:0.8rem;color:rgba(255,255,255,0.3);transition:color 0.2s}
  .footer-legal a:hover{color:rgba(255,255,255,0.6)}

  /* MOBILE NAV */
  .mobile-menu{display:none;position:fixed;inset:0;background:#fff;z-index:999;padding:80px 5% 40px;flex-direction:column;gap:1.5rem}
  .mobile-menu.open{display:flex}
  .mobile-menu a{font-size:1.1rem;font-weight:600;color:var(--dark);padding:12px 0;border-bottom:1px solid var(--border)}

  @media(max-width:900px){
    .hero-content{grid-template-columns:1fr;text-align:center}
    .hero-visual{display:none}
    .hero-stats{justify-content:center}
    .footer-top{grid-template-columns:1fr 1fr;gap:2rem}
    .footer-brand{grid-column:1/-1}
  }
  @media(max-width:640px){
    .nav-links,.nav-cta{display:none}
    .hamburger{display:flex}
    .hero-btns{justify-content:center}
    .footer-top{grid-template-columns:1fr}
    .footer-brand{grid-column:auto}
    .offer-inner{flex-direction:column;text-align:center}
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-inner">
    <a href="#" class="logo">
      <div class="logo-icon">S</div>
      Super<span>Mart</span>
    </a>
    <ul class="nav-links">
      <li><a href="#hero">Home</a></li>
      <li><a href="#categories">Categories</a></li>
      <li><a href="#offers">Offers</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <button class="nav-cta" onclick="alert('Opening shop...')">Shop Now →</button>
    <button class="hamburger" onclick="document.getElementById('mobileMenu').classList.toggle('open')" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
  </div>
</nav>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#hero" onclick="document.getElementById('mobileMenu').classList.remove('open')">Home</a>
  <a href="#categories" onclick="document.getElementById('mobileMenu').classList.remove('open')">Categories</a>
  <a href="#offers" onclick="document.getElementById('mobileMenu').classList.remove('open')">Offers</a>
  <a href="#contact" onclick="document.getElementById('mobileMenu').classList.remove('open')">Contact</a>
  <button class="nav-cta" style="width:fit-content" onclick="alert('Opening shop...')">Shop Now →</button>
</div>

<!-- HERO -->
<section id="hero" class="hero">
  <div class="hero-content">
    <div>
      <div class="hero-badge">Premium Grocery Delivery</div>
      <h1 class="hero-title">Fresh from Farm,<br><span>Delivered to Your</span><br>Doorstep</h1>
      <p class="hero-desc">Experience the luxury of farm-fresh produce, artisan goods, and everyday essentials — curated for quality, delivered with care, right to your home.</p>
      <div class="hero-btns">
        <button class="btn-primary" onclick="document.getElementById('categories').scrollIntoView({behavior:'smooth'})">Explore Products →</button>
        <button class="btn-outline" onclick="document.getElementById('offers').scrollIntoView({behavior:'smooth'})">View Offers</button>
      </div>
      <div class="hero-stats">
        <div class="stat"><div class="stat-num">50<span>K+</span></div><div class="stat-label">Happy Customers</div></div>
        <div class="stat"><div class="stat-num">2<span>K+</span></div><div class="stat-label">Products</div></div>
        <div class="stat"><div class="stat-num">30<span>min</span></div><div class="stat-label">Avg Delivery</div></div>
      </div>
    </div>
    <div class="hero-visual">
      <div class="hero-card-main">
        <div class="hero-img-box">🥦</div>
        <div class="hero-card-tag">Best Seller</div>
        <div class="hero-card-title">Organic Vegetable Box</div>
        <div class="hero-card-price">₹499 <span>₹699</span></div>
        <button class="hero-card-btn">Add to Cart +</button>
      </div>
      <div class="floating-badge top">
        <div class="fb-icon">🚚</div>
        <div class="fb-text">Free Delivery<div class="fb-sub">On orders above ₹499</div></div>
      </div>
      <div class="floating-badge bot">
        <div class="fb-icon">⭐</div>
        <div class="fb-text">4.9 Rated<div class="fb-sub">50,000+ reviews</div></div>
      </div>
    </div>
  </div>
</section>

<!-- OFFER BANNER -->
<div id="offers" class="offer-banner">
  <div class="offer-inner">
    <div class="offer-text">
      <h2>Limited Time Special Offer</h2>
      <p>Use code FRESH30 at checkout. Valid on first 3 orders. No minimum order value.</p>
    </div>
    <div class="offer-badge">30% OFF<small>FIRST ORDER</small></div>
    <button class="offer-cta" onclick="alert('Code copied: FRESH30')">Grab This Deal</button>
  </div>
</div>

<!-- CATEGORIES -->
<section id="categories">
  <div class="section-inner">
    <div class="section-head">
      <div class="section-label">Browse by Category</div>
      <h2 class="section-title">Everything Your Kitchen Needs</h2>
      <p class="section-desc">From farm-fresh produce to pantry staples — shop across 6 curated categories.</p>
    </div>
    <div class="categories-grid">
      <div class="cat-card"><span class="cat-icon">🥬</span><div class="cat-name">Fresh Groceries</div><div class="cat-count">320+ items</div></div>
      <div class="cat-card"><span class="cat-icon">🥛</span><div class="cat-name">Dairy & Eggs</div><div class="cat-count">85+ items</div></div>
      <div class="cat-card"><span class="cat-icon">🍞</span><div class="cat-name">Bakery</div><div class="cat-count">60+ items</div></div>
      <div class="cat-card"><span class="cat-icon">🧃</span><div class="cat-name">Beverages</div><div class="cat-count">140+ items</div></div>
      <div class="cat-card"><span class="cat-icon">🏠</span><div class="cat-name">Household</div><div class="cat-count">200+ items</div></div>
      <div class="cat-card"><span class="cat-icon">💆</span><div class="cat-name">Personal Care</div><div class="cat-count">170+ items</div></div>
    </div>
  </div>
</section>

<!-- PRODUCTS -->
<section class="products-section">
  <div class="section-inner">
    <div class="section-head">
      <div class="section-label">Featured Products</div>
      <h2 class="section-title">Today's Top Picks</h2>
      <p class="section-desc">Handpicked for freshness, taste, and value. Restocked daily.</p>
    </div>
    <div class="products-grid" id="productsGrid"></div>
  </div>
</section>

<!-- WHY US -->
<section>
  <div class="section-inner">
    <div class="section-head">
      <div class="section-label">Why SuperMart</div>
      <h2 class="section-title">A Smarter Way to Grocery Shop</h2>
      <p class="section-desc">We've reimagined the supermarket experience — faster, fresher, and more affordable.</p>
    </div>
    <div class="why-grid">
      <div class="why-card"><div class="why-icon">⚡</div><div class="why-title">Lightning Delivery</div><div class="why-desc">Get your groceries delivered in under 30 minutes. Our hyperlocal network ensures speed without compromise.</div></div>
      <div class="why-card"><div class="why-icon">🌿</div><div class="why-title">Farm-Fresh Products</div><div class="why-desc">Sourced directly from certified organic farms. Every product is checked for freshness before it reaches your door.</div></div>
      <div class="why-card"><div class="why-icon">🏆</div><div class="why-title">Trusted Quality</div><div class="why-desc">FSSAI certified. Every item is quality-tested and traceable to its source. We stand by every product we sell.</div></div>
      <div class="why-card"><div class="why-icon">💰</div><div class="why-title">Best Prices Guaranteed</div><div class="why-desc">We price-match any competitor. Found it cheaper elsewhere? We'll beat it — no questions asked.</div></div>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials-section">
  <div class="section-inner">
    <div class="section-head">
      <div class="section-label">Customer Stories</div>
      <h2 class="section-title">Loved by Thousands</h2>
    </div>
    <div class="testimonials-grid">
      <div class="testi-card">
        <div class="testi-stars">★★★★★</div>
        <p class="testi-text">"SuperMart completely changed how I shop for groceries. The quality is outstanding and delivery is always on time. I've cancelled my other subscriptions!"</p>
        <div class="testi-author"><div class="testi-avatar" style="background:#2d6a4f">PR</div><div><div class="testi-name">Priya Rathore</div><div class="testi-location">Raipur, CG</div></div></div>
      </div>
      <div class="testi-card">
        <div class="testi-stars">★★★★★</div>
        <p class="testi-text">"I love the organic section. Everything arrives in premium packaging, perfectly fresh. Worth every rupee. The 30-min delivery promise is real — they've never been late."</p>
        <div class="testi-author"><div class="testi-avatar" style="background:#1a4e8a">AM</div><div><div class="testi-name">Arjun Mehta</div><div class="testi-location">Bhilai, CG</div></div></div>
      </div>
      <div class="testi-card">
        <div class="testi-stars">★★★★★</div>
        <p class="testi-text">"As a working mom, SuperMart is a lifesaver. The app is beautiful, the selection is huge, and the prices are unbeatable. My family is hooked. 10/10 recommend."</p>
        <div class="testi-author"><div class="testi-avatar" style="background:#7b2d8b">SD</div><div><div class="testi-name">Sneha Dubey</div><div class="testi-location">Durg, CG</div></div></div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer id="contact">
  <div class="footer-inner">
    <div class="footer-top">
      <div class="footer-brand">
        <a href="#" class="logo" style="color:#fff"><div class="logo-icon">S</div>Super<span style="color:#7de0a8">Mart</span></a>
        <p class="footer-desc">Premium grocery delivery for modern homes. Fresh, fast, and trusted by 50,000+ families across India.</p>
        <div class="social-links">
          <div class="social-btn" title="Facebook">f</div>
          <div class="social-btn" title="Instagram">in</div>
          <div class="social-btn" title="Twitter">tw</div>
          <div class="social-btn" title="YouTube">yt</div>
        </div>
      </div>
      <div class="footer-col">
        <h4>Quick Links</h4>
        <ul class="footer-links">
          <li><a href="#hero">Home</a></li>
          <li><a href="#categories">Categories</a></li>
          <li><a href="#offers">Offers</a></li>
          <li><a href="#">About Us</a></li>
          <li><a href="#">Blog</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Categories</h4>
        <ul class="footer-links">
          <li><a href="#">Fresh Groceries</a></li>
          <li><a href="#">Dairy & Eggs</a></li>
          <li><a href="#">Bakery</a></li>
          <li><a href="#">Beverages</a></li>
          <li><a href="#">Household</a></li>
        </ul>
      </div>
      <div class="footer-col" id="contact-details">
        <h4>Contact Us</h4>
        <div class="contact-item"><span class="contact-icon">📍</span><div class="contact-text">123 Green Market Street,<br>Raipur, CG 492001</div></div>
        <div class="contact-item"><span class="contact-icon">📞</span><div class="contact-text">+91 98765 43210</div></div>
        <div class="contact-item"><span class="contact-icon">✉️</span><div class="contact-text">hello@supermart.in</div></div>
        <div class="contact-item"><span class="contact-icon">🕐</span><div class="contact-text">7 AM – 11 PM, All Days</div></div>
      </div>
    </div>
    <div class="footer-bottom">
      <span class="footer-copy">© 2025 SuperMart Pvt. Ltd. All rights reserved.</span>
      <div class="footer-legal">
        <a href="#">Privacy Policy</a>
        <a href="#">Terms of Use</a>
        <a href="#">Refund Policy</a>
      </div>
    </div>
  </div>
</footer>

<script>
const products=[
  {icon:'🥑',name:'Organic Avocados',cat:'Fresh Produce',price:'₹189',old:'₹249',rating:'4.8',reviews:'1.2k',badge:'Organic'},
  {icon:'🥛',name:'Farm Fresh Milk 1L',cat:'Dairy',price:'₹68',old:'₹80',rating:'4.9',reviews:'3.4k',badge:'Fresh'},
  {icon:'🍞',name:'Multigrain Bread Loaf',cat:'Bakery',price:'₹55',old:'',rating:'4.7',reviews:'890',badge:''},
  {icon:'🧴',name:'Cold-Press Orange Juice',cat:'Beverages',price:'₹129',old:'₹160',rating:'4.8',reviews:'2.1k',badge:'Sale',badgeClass:'sale'},
  {icon:'🫐',name:'Fresh Blueberries 250g',cat:'Fresh Produce',price:'₹299',old:'₹399',rating:'4.9',reviews:'560',badge:'Sale',badgeClass:'sale'},
  {icon:'🧀',name:'Premium Cheddar Block',cat:'Dairy',price:'₹349',old:'',rating:'4.7',reviews:'410',badge:'Import'},
  {icon:'🍫',name:'Dark Chocolate Muffin',cat:'Bakery',price:'₹75',old:'₹95',rating:'4.8',reviews:'1.8k',badge:''},
  {icon:'🫖',name:'Green Tea Collection',cat:'Beverages',price:'₹245',old:'₹320',rating:'4.9',reviews:'2.7k',badge:'Premium'},
];
const grid=document.getElementById('productsGrid');
products.forEach(p=>{
  grid.innerHTML+=`<div class="product-card">
    <div class="product-img">
      ${p.badge?`<span class="product-badge ${p.badgeClass||''}">${p.badge}</span>`:''}
      <span style="font-size:3.5rem">${p.icon}</span>
    </div>
    <div class="product-body">
      <div class="product-category">${p.cat}</div>
      <div class="product-name">${p.name}</div>
      <div class="product-rating"><span class="stars">★★★★★</span><span class="rating-count">${p.rating} (${p.reviews})</span></div>
      <div class="product-footer">
        <div><span class="product-price">${p.price}</span>${p.old?`<span class="product-price-old">${p.old}</span>`:''}</div>
        <button class="add-btn" onclick="this.textContent='✓ Added';this.style.background='#155830';setTimeout(()=>{this.textContent='+ Add';this.style.background=''},2000)">+ Add</button>
      </div>
    </div>
  </div>`;
});

// Scroll animations
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.style.opacity='1';e.target.style.transform='translateY(0)'}});
},{threshold:0.1});
document.querySelectorAll('.cat-card,.product-card,.why-card,.testi-card').forEach(el=>{
  el.style.opacity='0';el.style.transform='translateY(20px)';
  el.style.transition='opacity 0.5s ease, transform 0.5s ease';
  obs.observe(el);
});
</script>
</body>
</html>
