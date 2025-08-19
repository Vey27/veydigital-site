<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>VeyDigital – Home</title>
  <meta name="description" content="AI dashboards, automation, and predictive analytics." />
  <meta name="keywords" content="VeyDigital, AI Workflow, data analytics, interactive dashboard, automation services" />
  <link rel="icon" href="/assets/img/logotranparentoutlinetext.png" />
  <style>
    :root{
      --bg:#0E1116; --panel:#151A22; --ink:#E8EEF6;
      --brand:#00AEEF; --accent:#FFC857; --muted:#8DA2B5;
      --radius:16px;
    }
    *{box-sizing:border-box}
    body{margin:0; font-family:system-ui,-apple-system,Segoe UI,Roboto,Inter,Arial; color:var(--ink); background:var(--bg); display:flex; min-height:100vh}
    /* Sidebar */
    .sidebar{width:270px; background:var(--panel); padding:20px; position:sticky; top:0; height:100vh; border-right:1px solid #1f2630}
    .brand{display:flex; align-items:center; gap:12px; margin-bottom:18px}
    .brand img{height:36px; width:auto}
    .brand h1{font-size:18px; margin:0}
    .nav{display:flex; flex-direction:column; gap:10px; margin-top:12px}
    .btn{display:block; width:100%; padding:12px 14px; text-align:left; background:#0f141c; color:var(--ink); border:1px solid #1f2630; border-radius:12px; text-decoration:none; transition:all .2s}
    .btn:hover{border-color:var(--brand)}
    .btn.active{outline:2px solid var(--brand)}
    .muted{color:var(--muted); font-size:12px; margin-top:12px}
    /* Header + content */
    .wrap{flex:1; display:flex; flex-direction:column}
    .topbar{display:flex; align-items:center; justify-content:space-between; padding:16px 20px; border-bottom:1px solid #1f2630; position:sticky; top:0; background:rgba(14,17,22,.8); backdrop-filter:blur(8px); z-index:10}
    .topbar .title{font-weight:600}
    .menu-btn{display:none; border:1px solid #1f2630; background:#0f141c; color:var(--ink); border-radius:10px; padding:8px 12px}
    .content{padding:24px; max-width:1100px}
    .card{background:var(--panel); border:1px solid #1f2630; border-radius:var(--radius); padding:22px; margin-bottom:16px}
    .pill{display:inline-block; padding:6px 10px; border:1px solid #253042; border-radius:999px; font-size:12px; color:var(--muted)}
    a.inline{color:var(--brand); text-decoration:none}
    /* README area */
    #readme{scroll-margin-top:90px}
    .markdown-body{line-height:1.65}
    .markdown-body h1,.markdown-body h2,.markdown-body h3{margin-top:1.2em}
    .markdown-body code, .markdown-body pre{background:#0f141c; border:1px solid #1f2630; border-radius:10px; padding:2px 6px}
    /* Mobile */
    @media (max-width: 980px){
      .sidebar{position:fixed; left:-300px; transition:left .25s ease; z-index:20}
      .sidebar.open{left:0}
      .menu-btn{display:inline-block}
      .wrap{margin-left:0}
      body{overflow-x:hidden}
    }
  </style>
  <!-- Marked: small, fast Markdown renderer -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
</head>
<body>
  <aside class="sidebar" id="sidebar">
    <div class="brand">
      <img src="/assets/img/logotranparentoutlinetext.png" alt="VeyDigital logo" />
      <h1>VeyDigital</h1>
    </div>
    <nav class="nav">
      <a class="btn active" href="/">🏠 Home</a>
      <a class="btn" href="/work.html">🧰 Work</a>
      <a class="btn" href="/#readme">📄 README</a>
      <a class="btn" href="https://github.com/Vey27/veydigital" target="_blank" rel="noopener">⭐ GitHub</a>
    </nav>
    <div class="muted">Website → <a class="inline" href="https://www.veydigital.com">www.veydigital.com</a></div>
  </aside>

  <main class="wrap">
    <header class="topbar">
      <div class="title">Home</div>
      <button class="menu-btn" onclick="toggleSidebar()">☰ Menu</button>
    </header>

    <section class="content">
      <div class="card">
        <span class="pill">Welcome</span>
        <h2 style="margin:.4em 0 0">Modern AI dashboards, automation & analytics</h2>
        <p>Built for speed, accuracy, and growth. Explore our <a class="inline" href="/work.html">work</a> or read the in‑site <a class="inline" href="#readme">README</a>.</p>
      </div>

      <!-- README rendered inside the website -->
      <section id="readme" class="card">
        <span class="pill">In‑site</span>
        <h3 style="margin:.4em 0 12px">README.md</h3>
        <div id="readme-body" class="markdown-body">Loading README…</div>
      </section>
    </section>
  </main>

  <script>
    function toggleSidebar(){
      document.getElementById('sidebar').classList.toggle('open');
    }
    // Mark active link by URL
    [...document.querySelectorAll('.btn')].forEach(a=>{
      const here = location.pathname + location.hash;
      if(a.getAttribute('href') === here || (a.getAttribute('href')==='/#readme' && location.hash==='#readme')){
        a.classList.add('active');
      }
    });
    // Load README.md into the page
    async function loadReadme(){
      try{
        const res = await fetch('/README.md', {cache:'no-store'});
        if(!res.ok) throw new Error('Fetch failed');
        const md = await res.text();
        document.getElementById('readme-body').innerHTML = marked.parse(md);
      }catch(e){
        document.getElementById('readme-body').innerHTML = '<p>Could not load README.md. You can still view it on <a class="inline" href="https://github.com/Vey27/veydigital">GitHub</a>.</p>';
      }
    }
    loadReadme();
  </script>
</body>
</html>
