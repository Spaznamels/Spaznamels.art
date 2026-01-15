# Spaznamels.art
Spaznamels - Enameling Silver art
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Spaznamels — One-of-One Enameled Silver Rounds</title>
  <meta name="description" content="Spaznamels — unique, hand-enameled .999 fine silver rounds. Each piece is one-of-one." />
  <link rel="stylesheet" href="style.css" />
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <meta property="og:title" content="Spaznamels — One-of-One Enameled Silver Rounds" />
  <meta property="og:description" content="Unique hand-enameled .999 fine silver rounds. Each piece is one-of-one." />
  <link rel="canonical" href="https://spaznamels.art/" />
</head>
<body>
  <a class="skip-link" href="#main">Skip to content</a>

  <header class="site-header" role="banner">
    <div class="header-inner">
      <img src="logo.png" alt="Spaznamels logo" class="logo" width="240" height="80" />
      <p class="tagline">One-of-One Enameled Silver Rounds</p>
    </div>
  </header>

  <main id="main" role="main" class="container">
    <section class="intro" aria-labelledby="intro-title">
      <h1 id="intro-title" class="site-title">Spaznamels</h1>
      <p class="lede">Singular, hand-enameled .999 silver rounds — each released as a unique one-of-one.</p>
    </section>

    <section id="gallery" class="gallery" aria-labelledby="gallery-title">
      <h2 id="gallery-title">Available Works</h2>
      <div id="cards" class="cards" aria-live="polite"></div>
    </section>

    <section class="archive" aria-labelledby="archive-title">
      <h2 id="archive-title">Archive</h2>
      <p class="muted">Previously sold one-of-one works.</p>
      <ul id="archive-list" class="archive-list"></ul>
    </section>
  </main>

  <footer class="site-footer" role="contentinfo">
    <nav class="footer-nav" aria-label="Footer">
      <a href="/privacy.html">Privacy</a>
      <a href="/terms.html">Terms</a>
      <a href="mailto:you@spaznamels.art">Contact</a>
    </nav>
    <p class="copyright">© Spaznamels LLC</p>
  </footer>

  <!-- Client-side script: load products.json and render the gallery -->
  <script>
    async function loadProducts() {
      try {
        const res = await fetch('products.json', {cache: 'no-cache'});
        if (!res.ok) throw new Error('Failed to load products.json');
        const products = await res.json();

        const cards = document.getElementById('cards');
        const archiveList = document.getElementById('archive-list');

        products.forEach(p => {
          const card = document.createElement('article');
          card.className = 'card';
          card.id = p.id;

          const imgWrap = document.createElement('a');
          imgWrap.href = `product.html?id=${encodeURIComponent(p.id)}`;
          imgWrap.className = 'card-media';

          const img = document.createElement('img');
          img.src = p.image;
          img.alt = p.alt || p.title;
          img.loading = 'lazy';
          img.width = 800;
          img.height = 800;
          imgWrap.appendChild(img);

          const body = document.createElement('div');
          body.className = 'card-body';

          const title = document.createElement('h3');
          title.className = 'card-title';
          title.textContent = p.title;
          body.appendChild(title);

          const meta = document.createElement('p');
          meta.className = 'card-meta';
          meta.textContent = p.metal;
          body.appendChild(meta);

          const price = document.createElement('p');
          price.className = 'card-price';
          if (p.sold) {
            price.textContent = 'SOLD';
            price.classList.add('sold');
          } else {
            price.textContent = p.price ? p.price : 'Contact for price';
          }
          body.appendChild(price);

          const actions = document.createElement('div');
          actions.className = 'card-actions';

          if (!p.sold) {
            if (p.stripe) {
              const a = document.createElement('a');
              a.className = 'btn btn-primary';
              a.href = p.stripe;
              a.target = '_blank';
              a.rel = 'noopener noreferrer';
              a.textContent = 'Pay by Card';
              actions.appendChild(a);
            }
            if (p.paypal) {
              const a = document.createElement('a');
              a.className = 'btn';
              a.href = p.paypal;
              a.target = '_blank';
              a.rel = 'noopener noreferrer';
              a.textContent = 'Pay with PayPal';
              actions.appendChild(a);
            }
            if (p.crypto) {
              const a = document.createElement('a');
              a.className = 'btn';
              a.href = p.crypto;
              a.target = '_blank';
              a.rel = 'noopener noreferrer';
              a.textContent = 'Pay with Crypto';
              actions.appendChild(a);
            }
            const bank = document.createElement('a');
            bank.className = 'btn btn-ghost';
            bank.href = 'mailto:you@spaznamels.art?subject=Bank transfer for ' + encodeURIComponent(p.title);
            bank.textContent = 'Bank transfer';
            actions.appendChild(bank);
          }

          body.appendChild(actions);

          card.appendChild(imgWrap);
          card.appendChild(body);
          cards.appendChild(card);

          if (p.sold) {
            const li = document.createElement('li');
            li.textContent = `${p.title} — SOLD`;
            archiveList.appendChild(li);
          }
        });
      } catch (err) {
        console.error(err);
        document.getElementById('cards').textContent = 'Unable to load catalog.';
      }
    }

    loadProducts();
  </script>
</body>
</html>
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Product — Spaznamels</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <a class="skip-link" href="#main">Skip to content</a>
  <header class="site-header">
    <div class="header-inner">
      <a href="/" aria-label="Home"><img src="logo.png" alt="Spaznamels" class="logo" width="220" height="72"></a>
      <p class="tagline">One-of-One Enameled Silver Rounds</p>
    </div>
  </header>

  <main id="main" class="container" role="main">
    <div id="product-root" class="product-page">Loading…</div>
  </main>

  <footer class="site-footer">
    <nav class="footer-nav" aria-label="Footer">
      <a href="/privacy.html">Privacy</a>
      <a href="/terms.html">Terms</a>
      <a href="mailto:you@spaznamels.art">Contact</a>
    </nav>
  </footer>

  <script>
    async function renderProduct() {
      const params = new URLSearchParams(location.search);
      const id = params.get('id');
      if (!id) {
        document.getElementById('product-root').textContent = 'No product specified.';
        return;
      }
      try {
        const res = await fetch('products.json', {cache: 'no-cache'});
        const products = await res.json();
        const p = products.find(x => x.id === id);
        if (!p) {
          document.getElementById('product-root').textContent = 'Product not found.';
          return;
        }

        const root = document.getElementById('product-root');
        root.innerHTML = '';

        const left = document.createElement('div');
        left.className = 'product-media';
        const img = document.createElement('img');
        img.src = p.image;
        img.alt = p.alt || p.title;
        img.loading = 'eager';
        left.appendChild(img);

        const right = document.createElement('div');
        right.className = 'product-info';

        const title = document.createElement('h1');
        title.textContent = p.title;
        right.appendChild(title);

        const metal = document.createElement('p');
        metal.className = 'metal';
        metal.textContent = p.metal;
        right.appendChild(metal);

        const price = document.createElement('p');
        price.className = 'price';
        price.textContent = p.sold ? 'SOLD' : (p.price || 'Contact for price');
        if (p.sold) price.classList.add('sold');
        right.appendChild(price);

        if (!p.sold) {
          const actions = document.createElement('div');
          actions.className = 'product-actions';
          if (p.stripe) {
            const a = document.createElement('a'); a.className='btn btn-primary'; a.href=p.stripe; a.target='_blank'; a.rel='noopener noreferrer'; a.textContent='Pay by Card'; actions.appendChild(a);
          }
          if (p.paypal) {
            const a = document.createElement('a'); a.className='btn'; a.href=p.paypal; a.target='_blank'; a.rel='noopener noreferrer'; a.textContent='Pay with PayPal'; actions.appendChild(a);
          }
          if (p.crypto) {
            const a = document.createElement('a'); a.className='btn'; a.href=p.crypto; a.target='_blank'; a.rel='noopener noreferrer'; a.textContent='Pay with Crypto'; actions.appendChild(a);
          }
          const bank = document.createElement('a'); bank.className='btn btn-ghost'; bank.href='mailto:you@spaznamels.art?subject=Bank transfer for '+encodeURIComponent(p.title); bank.textContent='Bank transfer'; actions.appendChild(bank);

          right.appendChild(actions);
        }

        const desc = document.createElement('div');
        desc.className = 'product-desc';
        desc.innerHTML = p.description_html || (`<p>${p.description || ''}</p>`);
        right.appendChild(desc);

        root.appendChild(left);
        root.appendChild(right);

      } catch (err) {
        console.error(err);
        document.getElementById('product-root').textContent = 'Error loading product.';
      }
    }

    renderProduct();
  </script>
</body>
</html>
:root{
  --bg: #0f0f12;
  --card: #0b0b0d;
  --text: #f3f2f1;
  --muted: #9b9b9b;
  --accent: #c7b27a;
  --accent-2: #bca46a;
  --glass: rgba(255,255,255,0.03);
  --radius: 8px;
  --max-width: 1200px;
  --container-pad: 40px;
  --transition: 220ms cubic-bezier(.2,.9,.3,1);
}

*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;
  background: linear-gradient(180deg,var(--bg), #070708 120%);
  color:var(--text);
  font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  line-height:1.5;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  text-rendering:optimizeLegibility;
}

/* Typographic rhythm */
.site-title{font-family: "Playfair Display", serif; font-size:2rem; margin:0; letter-spacing:0.02em}
.lede{color:var(--muted); margin-top:8px; font-size:1.05rem; max-width:60ch; margin-left:auto; margin-right:auto}

/* Layout */
.container{max-width:var(--max-width); margin:0 auto; padding:var(--container-pad) 20px}
header.site-header{padding:56px 0 24px; text-align:center}
.header-inner{display:flex; flex-direction:column; align-items:center; gap:14px}
.logo{width:260px; height:auto}
.tagline{font-size:12px; color:var(--accent); letter-spacing:2px; text-transform:uppercase; margin:0}

/* Cards grid */
.cards{display:grid; grid-template-columns: repeat(1, 1fr); gap:28px; margin-top:28px}
.card{
  display:flex; flex-direction:column;
  background:linear-gradient(180deg,var(--glass), rgba(255,255,255,0.01));
  border-radius:var(--radius); overflow:hidden; box-shadow: 0 6px 24px rgba(0,0,0,0.6);
  transform: translateZ(0);
  transition: transform var(--transition), box-shadow var(--transition);
}
.card:focus-within, .card:hover{transform: translateY(-6px); box-shadow: 0 18px 48px rgba(0,0,0,0.7)}

/* Media */
.card-media{display:block; overflow:hidden; aspect-ratio: 1/1}
.card-media img{width:100%; height:100%; object-fit:cover; display:block; transition: transform var(--transition)}
.card:hover .card-media img{transform:scale(1.03)}

/* Body */
.card-body{padding:18px 20px 22px}
.card-title{font-family:"Playfair Display", serif; font-size:1.15rem; margin:0 0 6px}
.card-meta{color:var(--muted); margin:0 0 10px}
.card-price{font-weight:700; margin:0 0 12px}
.card-price.sold{color:#ff6b6b}
.card-actions{display:flex; gap:10px; flex-wrap:wrap}

/* Buttons */
.btn{
  display:inline-flex; align-items:center; justify-content:center;
  padding:10px 14px; border-radius:6px; text-decoration:none; cursor:pointer;
  font-weight:600; color:var(--card); background:transparent; border:1px solid rgba(255,255,255,0.04);
  transition: transform var(--transition), background var(--transition), box-shadow var(--transition);
}
.btn-primary{background:linear-gradient(180deg,var(--accent), var(--accent-2)); color:var(--card); border:none}
.btn-ghost{background:transparent; color:var(--accent); border:1px solid rgba(199,178,122,0.12)}
.btn:hover{transform:translateY(-3px); box-shadow:0 8px 20px rgba(0,0,0,0.5)}
.btn:active{transform:translateY(0)}

/* Product page */
.product-page{display:grid; grid-template-columns: 1fr; gap:28px; align-items:start}
.product-media img{width:100%; border-radius:var(--radius); display:block}
.product-info{padding:6px 0}
.product-info h1{font-family:"Playfair Display", serif; margin:0 0 8px; font-size:1.8rem}
.product-info .metal{color:var(--muted); margin:6px 0}
.product-info .price{font-weight:700; margin:8px 0 18px}
.product-actions{display:flex; gap:12px; flex-wrap:wrap}

/* Archive */
.archive-list{list-style:none; padding:0; margin:8px 0 40px; color:var(--muted)}

/* Footer */
.site-footer{padding:36px 20px; text-align:center; color:var(--muted)}
.footer-nav{display:flex; gap:14px; justify-content:center; margin-bottom:10px}
.footer-nav a{color:var(--muted); text-decoration:none}

/* Responsive */
@media(min-width:720px){
  .cards{grid-template-columns: repeat(2, 1fr)}
  .product-page{grid-template-columns: 1fr 420px}
  .container{padding:48px 24px}
}

@media(min-width:1100px){
  .cards{grid-template-columns: repeat(3, 1fr)}
}

/* Accessibility */
.skip-link{position:absolute; left:16px; top:12px; background:#000; color:#fff; padding:8px 12px; border-radius:6px; transform:translateY(-150%); transition:transform .12s}
.skip-link:focus{transform:translateY(0)}

/* Reduced motion */
@media (prefers-reduced-motion:reduce){
  *{transition:none !important}
}
:root{
  --bg: #0f0f12;
  --card: #0b0b0d;
  --text: #f3f2f1;
  --muted: #9b9b9b;
  --accent: #c7b27a;
  --accent-2: #bca46a;
  --glass: rgba(255,255,255,0.03);
  --radius: 8px;
  --max-width: 1200px;
  --container-pad: 40px;
  --transition: 220ms cubic-bezier(.2,.9,.3,1);
}

*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;
  background: linear-gradient(180deg,var(--bg), #070708 120%);
  color:var(--text);
  font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  line-height:1.5;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  text-rendering:optimizeLegibility;
}

/* Typographic rhythm */
.site-title{font-family: "Playfair Display", serif; font-size:2rem; margin:0; letter-spacing:0.02em}
.lede{color:var(--muted); margin-top:8px; font-size:1.05rem; max-width:60ch; margin-left:auto; margin-right:auto}

/* Layout */
.container{max-width:var(--max-width); margin:0 auto; padding:var(--container-pad) 20px}
header.site-header{padding:56px 0 24px; text-align:center}
.header-inner{display:flex; flex-direction:column; align-items:center; gap:14px}
.logo{width:260px; height:auto}
.tagline{font-size:12px; color:var(--accent); letter-spacing:2px; text-transform:uppercase; margin:0}

/* Cards grid */
.cards{display:grid; grid-template-columns: repeat(1, 1fr); gap:28px; margin-top:28px}
.card{
  display:flex; flex-direction:column;
  background:linear-gradient(180deg,var(--glass), rgba(255,255,255,0.01));
  border-radius:var(--radius); overflow:hidden; box-shadow: 0 6px 24px rgba(0,0,0,0.6);
  transform: translateZ(0);
  transition: transform var(--transition), box-shadow var(--transition);
}
.card:focus-within, .card:hover{transform: translateY(-6px); box-shadow: 0 18px 48px rgba(0,0,0,0.7)}

/* Media */
.card-media{display:block; overflow:hidden; aspect-ratio: 1/1}
.card-media img{width:100%; height:100%; object-fit:cover; display:block; transition: transform var(--transition)}
.card:hover .card-media img{transform:scale(1.03)}

/* Body */
.card-body{padding:18px 20px 22px}
.card-title{font-family:"Playfair Display", serif; font-size:1.15rem; margin:0 0 6px}
.card-meta{color:var(--muted); margin:0 0 10px}
.card-price{font-weight:700; margin:0 0 12px}
.card-price.sold{color:#ff6b6b}
.card-actions{display:flex; gap:10px; flex-wrap:wrap}

/* Buttons */
.btn{
  display:inline-flex; align-items:center; justify-content:center;
  padding:10px 14px; border-radius:6px; text-decoration:none; cursor:pointer;
  font-weight:600; color:var(--card); background:transparent; border:1px solid rgba(255,255,255,0.04);
  transition: transform var(--transition), background var(--transition), box-shadow var(--transition);
}
.btn-primary{background:linear-gradient(180deg,var(--accent), var(--accent-2)); color:var(--card); border:none}
.btn-ghost{background:transparent; color:var(--accent); border:1px solid rgba(199,178,122,0.12)}
.btn:hover{transform:translateY(-3px); box-shadow:0 8px 20px rgba(0,0,0,0.5)}
.btn:active{transform:translateY(0)}

/* Product page */
.product-page{display:grid; grid-template-columns: 1fr; gap:28px; align-items:start}
.product-media img{width:100%; border-radius:var(--radius); display:block}
.product-info{padding:6px 0}
.product-info h1{font-family:"Playfair Display", serif; margin:0 0 8px; font-size:1.8rem}
.product-info .metal{color:var(--muted); margin:6px 0}
.product-info .price{font-weight:700; margin:8px 0 18px}
.product-actions{display:flex; gap:12px; flex-wrap:wrap}

/* Archive */
.archive-list{list-style:none; padding:0; margin:8px 0 40px; color:var(--muted)}

/* Footer */
.site-footer{padding:36px 20px; text-align:center; color:var(--muted)}
.footer-nav{display:flex; gap:14px; justify-content:center; margin-bottom:10px}
.footer-nav a{color:var(--muted); text-decoration:none}

/* Responsive */
@media(min-width:720px){
  .cards{grid-template-columns: repeat(2, 1fr)}
  .product-page{grid-template-columns: 1fr 420px}
  .container{padding:48px 24px}
}

@media(min-width:1100px){
  .cards{grid-template-columns: repeat(3, 1fr)}
}

/* Accessibility */
.skip-link{position:absolute; left:16px; top:12px; background:#000; color:#fff; padding:8px 12px; border-radius:6px; transform:translateY(-150%); transition:transform .12s}
.skip-link:focus{transform:translateY(0)}

/* Reduced motion */
@media (prefers-reduced-motion:reduce){
  *{transition:none !important}
}
:root{
  --bg: #0f0f12;
  --card: #0b0b0d;
  --text: #f3f2f1;
  --muted: #9b9b9b;
  --accent: #c7b27a;
  --accent-2: #bca46a;
  --glass: rgba(255,255,255,0.03);
  --radius: 8px;
  --max-width: 1200px;
  --container-pad: 40px;
  --transition: 220ms cubic-bezier(.2,.9,.3,1);
}

*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;
  background: linear-gradient(180deg,var(--bg), #070708 120%);
  color:var(--text);
  font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  line-height:1.5;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  text-rendering:optimizeLegibility;
}

/* Typographic rhythm */
.site-title{font-family: "Playfair Display", serif; font-size:2rem; margin:0; letter-spacing:0.02em}
.lede{color:var(--muted); margin-top:8px; font-size:1.05rem; max-width:60ch; margin-left:auto; margin-right:auto}

/* Layout */
.container{max-width:var(--max-width); margin:0 auto; padding:var(--container-pad) 20px}
header.site-header{padding:56px 0 24px; text-align:center}
.header-inner{display:flex; flex-direction:column; align-items:center; gap:14px}
.logo{width:260px; height:auto}
.tagline{font-size:12px; color:var(--accent); letter-spacing:2px; text-transform:uppercase; margin:0}

/* Cards grid */
.cards{display:grid; grid-template-columns: repeat(1, 1fr); gap:28px; margin-top:28px}
.card{
  display:flex; flex-direction:column;
  background:linear-gradient(180deg,var(--glass), rgba(255,255,255,0.01));
  border-radius:var(--radius); overflow:hidden; box-shadow: 0 6px 24px rgba(0,0,0,0.6);
  transform: translateZ(0);
  transition: transform var(--transition), box-shadow var(--transition);
}
.card:focus-within, .card:hover{transform: translateY(-6px); box-shadow: 0 18px 48px rgba(0,0,0,0.7)}

/* Media */
.card-media{display:block; overflow:hidden; aspect-ratio: 1/1}
.card-media img{width:100%; height:100%; object-fit:cover; display:block; transition: transform var(--transition)}
.card:hover .card-media img{transform:scale(1.03)}

/* Body */
.card-body{padding:18px 20px 22px}
.card-title{font-family:"Playfair Display", serif; font-size:1.15rem; margin:0 0 6px}
.card-meta{color:var(--muted); margin:0 0 10px}
.card-price{font-weight:700; margin:0 0 12px}
.card-price.sold{color:#ff6b6b}
.card-actions{display:flex; gap:10px; flex-wrap:wrap}

/* Buttons */
.btn{
  display:inline-flex; align-items:center; justify-content:center;
  padding:10px 14px; border-radius:6px; text-decoration:none; cursor:pointer;
  font-weight:600; color:var(--card); background:transparent; border:1px solid rgba(255,255,255,0.04);
  transition: transform var(--transition), background var(--transition), box-shadow var(--transition);
}
.btn-primary{background:linear-gradient(180deg,var(--accent), var(--accent-2)); color:var(--card); border:none}
.btn-ghost{background:transparent; color:var(--accent); border:1px solid rgba(199,178,122,0.12)}
.btn:hover{transform:translateY(-3px); box-shadow:0 8px 20px rgba(0,0,0,0.5)}
.btn:active{transform:translateY(0)}

/* Product page */
.product-page{display:grid; grid-template-columns: 1fr; gap:28px; align-items:start}
.product-media img{width:100%; border-radius:var(--radius); display:block}
.product-info{padding:6px 0}
.product-info h1{font-family:"Playfair Display", serif; margin:0 0 8px; font-size:1.8rem}
.product-info .metal{color:var(--muted); margin:6px 0}
.product-info .price{font-weight:700; margin:8px 0 18px}
.product-actions{display:flex; gap:12px; flex-wrap:wrap}

/* Archive */
.archive-list{list-style:none; padding:0; margin:8px 0 40px; color:var(--muted)}

/* Footer */
.site-footer{padding:36px 20px; text-align:center; color:var(--muted)}
.footer-nav{display:flex; gap:14px; justify-content:center; margin-bottom:10px}
.footer-nav a{color:var(--muted); text-decoration:none}

/* Responsive */
@media(min-width:720px){
  .cards{grid-template-columns: repeat(2, 1fr)}
  .product-page{grid-template-columns: 1fr 420px}
  .container{padding:48px 24px}
}

@media(min-width:1100px){
  .cards{grid-template-columns: repeat(3, 1fr)}
}

/* Accessibility */
.skip-link{position:absolute; left:16px; top:12px; background:#000; color:#fff; padding:8px 12px; border-radius:6px; transform:translateY(-150%); transition:transform .12s}
.skip-link:focus{transform:translateY(0)}

/* Reduced motion */
@media (prefers-reduced-motion:reduce){
  *{transition:none !important}
}
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Terms — Spaznamels</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <main class="container">
    <h1>Terms & Conditions</h1>
    <p>Last updated: 2026-01-15</p>
    <p>All works are sold as one-of-one. Shipping and returns are handled per transaction agreement. By purchasing you agree that the item is unique and non-reproducible.</p>
    <h2>Intellectual property</h2>
    <p>All imagery and text are copyright Spaznamels LLC.</p>
  </main>
</body>
</html>
# Spaznamels.art — Static site

This is a minimal static site for selling one-of-one enameled silver rounds. The gallery renders from `products.json` so you can add products by editing that file and uploading images.

Files to add to repo root:
- index.html
- product.html
- style.css
- products.json
- privacy.html
- terms.html
- README.md
- CNAME
- (images) piece-01.jpg, piece-01-800.jpg, piece-01-400.jpg, piece-00.jpg, logo.png

Quick upload via GitHub web UI
1. Go to your repository on GitHub.
2. Click "Add file" → "Create new file".
3. For each file above: paste the file contents and at the bottom choose "Create a new branch for this commit" and name it `site/add-GER-2023`.
4. After adding all files, open a Pull Request, review and merge to `main`.

Or using git (CLI)
- git checkout -b site/add-GER-2023
- Add the files to your repo locally
- git add .
- git commit -m "Add site + Germania product"
- git push origin site/add-GER-2023
- Open a PR on GitHub and merge

CNAME (custom domain)
- Add a file named `CNAME` (no extension) containing:
  ```
  spaznamels.art
  ```
- Configure DNS for your domain:
  - Add A records pointing to these GitHub Pages IPs:
    - 185.199.108.153
    - 185.199.109.153
    - 185.199.110.153
    - 185.199.111.153
  - Wait for DNS propagation; GitHub Pages will provision TLS automatically once DNS and CNAME are set.

Replacing placeholders
- Stripe / Coinbase: replace `"PLACEHOLDER_STRIPE_LINK"` and `"PLACEHOLDER_COINBASE_LINK"` in `products.json` with your actual checkout links.
  - Stripe Payment Links start with `https://buy.stripe.com/`
  - Coinbase Commerce checkout URLs start with `https://commerce.coinbase.com/checkout/`
- PayPal: `products.json` currently uses a direct-pay link with your PayPal email. Replace `amount=XXX` with a numeric price if you want PayPal to auto-fill price.

Add images
- Upload your images referenced in `products.json` (e.g., `piece-01.jpg`) in the repo root (or adjust the `image` paths).
- Use large master images (2000px longest edge) and additional 800/400 px derived files for responsive loading.

Marking a product sold
- Set `"sold": true` for the product in `products.json`. The gallery will mark it SOLD, remove payment buttons, and add it to the Archive.

Security
- Keep API keys and secrets out of the public repo. Only add public checkout links (Stripe Payment Links and Coinbase checkout URLs are safe to include).

Need help?
- I can open a PR and push these files for you if you add the GitHub user `copilot` as a collaborator with write access.
- If you'd like, I can later add a tiny GitHub Action to validate the product JSON, or a simple admin UI (Netlify/Forestry/Netlify CMS) so you can update products without editing JSON.
- spaznamels.art

- 
