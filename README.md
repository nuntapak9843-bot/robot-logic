# robot-logic
Robot Logic: เขียนโค้ดพิชิตด่านด้วยภาษา Python เกมการศึกษาสำหรับนักเรียนระดับมัธยมศึกษา ที่ออกแบบมาเพื่อฝึกฝนทักษะการเขียนโปรแกรมภาษา Python ผ่านการควบคุมหุ่นยนต์ในสถานการณ์จำลอง ผู้เล่นจะต้องใช้ความรู้ด้านการประกาศตัวแปร การใช้ตัวดำเนินการทางคณิตศาสตร์ คำสั่งเงื่อนไข การใช้ List และลูป เพื่อให้หุ่นยนต์สามารถผ่านด่านต่าง ๆ ได้สำเร็จ

<!doctype html>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Robot Logic: พิชิตด่านด้วย Python</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#f0f4ff; --panel:#ffffff; --panel-2:#e8edff; --text:#1a1a1a; --muted:#5c6b91;
      --accent:#6ea8fe; --accent-2:#a78bfa; --ok:#24d67b; --warn:#ffcf5a; --err:#ff6b6b;
      --code:#e8edff; --border:rgba(0,0,0,.08);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;background:radial-gradient(1200px 600px at 10% -10%, rgba(167,139,250,.15), transparent),
                 radial-gradient(1000px 700px at 110% 10%, rgba(110,168,254,.12), transparent),
                 var(--bg);
         color:var(--text);font-family:"Noto Sans Thai", system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, sans-serif;}
    header{position:sticky;top:0;z-index:50;background:linear-gradient(180deg, rgba(240,244,255,.95) 0%, rgba(240,244,255,.7) 100%);
           border-bottom:1px solid var(--border);backdrop-filter: blur(6px)}
    .wrap{max-width:1200px;margin:0 auto;padding:16px}
    .title{display:flex;gap:14px;align-items:center}
    .logo{width:40px;height:40px;border-radius:12px;background:linear-gradient(135deg, var(--accent), var(--accent-2));
          display:grid;place-items:center;color:#081226;font-weight:900}
    .title h1{font-size:1.4rem;margin:0}
    .subtitle{color:var(--muted);font-size:.95rem}

    .layout{display:grid;grid-template-columns:280px 1fr;gap:18px;padding:18px}
    @media (max-width: 880px){.layout{grid-template-columns:1fr}}

    .card{background:linear-gradient(180deg, var(--panel), var(--panel-2));
          border:1px solid var(--border);border-radius:18px;box-shadow:0 4px 20px rgba(0,0,0,.1)}
    .sidebar{padding:14px}
    .search{display:flex;gap:8px;margin-bottom:10px}
    .search input{width:100%;padding:10px 12px;border-radius:12px;border:1px solid var(--border);background:rgba(0,0,0,.03);color:var(--text)}

    .menu{display:grid;gap:8px}
    .menu button{appearance:none;border:none;text-align:left;padding:12px 12px;border-radius:12px;cursor:pointer;color:var(--text);
                 background:rgba(0,0,0,.03);border:1px solid var(--border);transition:.15s}
    .menu button:hover{transform:translateY(-1px);}
    .menu button.active{outline:2px solid var(--accent); background:linear-gradient(180deg, rgba(110,168,254,.15), rgba(255,255,255,.03))}

    .main{display:grid;gap:16px}
    .pane{padding:16px}

    .badges{display:flex;flex-wrap:wrap;gap:8px}
    .badge{padding:6px 10px;border-radius:999px;font-size:.85rem;background:rgba(0,0,0,.03);border:1px solid var(--border);color:var(--muted)}

    .editor{display:grid;gap:12px}
    .editor textarea{width:100%;min-height:240px;resize:vertical;border-radius:14px;padding:12px 12px 36px 12px;font-family:ui-monospace, Menlo, SFMono-Regular, Consolas, "Liberation Mono", monospace;
                     background:var(--code);color:#1a1a1a;border:1px solid var(--border)}

    .toolbar{display:flex;flex-wrap:wrap;gap:8px;align-items:center}
    .toolbar button{appearance:none;border:none;border-radius:12px;padding:10px 14px;cursor:pointer;color:#fff;font-weight:700;
                    background:var(--accent);box-shadow:0 4px 10px rgba(110,168,254,.25);}
    .ghost{background:transparent !important;color:var(--text) !important;border:1px solid var(--border)}
    .secondary{background:var(--accent-2);color:#fff}

    .io{display:grid;grid-template-columns:1fr;gap:10px}
    .io pre{margin:0;background:#f5f8ff;border-radius:12px;border:1px solid var(--border);padding:12px;overflow:auto;color:#1a1a1a}

    .footer{padding:12px 16px;color:var(--muted);text-align:center}
    .pill{display:inline-flex;align-items:center;gap:6px;padding:6px 10px;border-radius:999px;background:rgba(0,0,0,.03);border:1px solid var(--border)}
    .status-dot{width:10px;height:10px;border-radius:999px;background:var(--warn)}
    .status-ok{background:var(--ok)}
    .status-err{background:var(--err)}

    .kbd{font-family:ui-monospace,monospace;background:rgba(0,0,0,.05);padding:0 6px;border-radius:6px;border:1px solid var(--border)}
    .hint{color:var(--muted)}
    .link{color:var(--accent);text-decoration:none}
    .credits{margin-top:16px;font-size:0.85rem;color:var(--muted);}
  </style>
</head>
<body>
  <header>
    <div class="wrap">
      <div class="title">
        <div class="logo">🤖</div>
        <div>
          <h1>Robot Logic — พิชิตด่านด้วย <span style="color:var(--accent)">Python</span></h1>
          <div class="subtitle">ฝึกตรรกะเขียนโค้ดให้หุ่นยนต์ผ่านด่าน เริ่มจากพื้นฐานไปจนถึงเงื่อนไขซับซ้อน</div>
        </div>
      </div>
    </div>
  </header>

  <main class="wrap layout">
    <aside class="card sidebar">
      <div class="search"><input id="search" placeholder="ค้นหาด่าน… (เช่น for, list, if)" /></div>
      <div class="menu" id="menu"></div>
      <div class="pane" style="border-top:1px solid var(--border);margin-top:12px">
        <div class="badges">
          <span class="badge">Python ในเบราว์เซอร์ด้วย Pyodide</span>
          <span class="badge">เหมาะกับ ม.2–ม.4</span>
          <span class="badge">เปิดซอร์ส โฮสต์บน GitHub Pages</span>
        </div>
      </div>
    </aside>

    <section class="main">
      <div class="card pane">
        <h2 id="level-title" style="margin-top:0">เลือกระดับทางซ้ายเพื่อเริ่ม</h2>
        <p id="level-desc" class="hint">คำอธิบายด่านจะแสดงที่นี่</p>
        <div class="badges" style="margin-bottom:8px">
          <span class="pill"><span class="status-dot" id="runtime-dot"></span> <span id="runtime-status">กำลังโหลด Python…</span></span>
          <span class="pill">เคล็ดลับ: กด <span class="kbd">Ctrl</span> + <span class="kbd">Enter</span> เพื่อ Run</span>
        </div>
        <div class="editor">
          <textarea id="code" spellcheck="false" placeholder="# โค้ดของคุณ…"></textarea>
          <div class="toolbar">
            <button id="btn-run">▶️ Run</button>
            <button id="btn-check" class="secondary">✅ ตรวจด่าน</button>
            <button id="btn-reset" class="ghost">♻️ รีเซ็ตโค้ด</button>
            <a class="ghost link" id="btn-copy" style="padding:10px 14px;border-radius:12px;border:1px solid var(--border)">📋 คัดลอกโค้ด</a>
          </div>
          <div class="io">
            <div>
              <div class="hint">ผลลัพธ์ (stdout)</div>
              <pre id="stdout"></pre>
            </div>
            <div>
              <div class="hint">สถานะด่าน</div>
              <pre id="judge"></pre>
            </div>
          </div>
        </div>
      </div>

      <div class="card pane">
        <h3 style="margin-top:0">คู่มือย่อ</h3>
        <ul>
          <li><b>Run</b> เพื่อรันโค้ดของคุณ ดูผลลัพธ์ในช่อง stdout</li>
          <li><b>ตรวจด่าน</b> จะรันชุดทดสอบอัตโนมัติให้ผ่านเกณฑ์</li>
          <li>คุณสามารถ <b>รีเซ็ตโค้ด</b> กลับเป็นโค้ดตั้งต้นของด่าน</li>
          <li>รองรับ <code>input()</code> ผ่าน popup ถ้าจำเป็น</li>
        </ul>
      </div>

      <div class="footer">
        สร้างเพื่อการเรียนรู้ • หุ่นยนต์จะดีใจทุกครั้งที่คุณผ่านด่าน 💫
        <div class="credits">Created by Nuntapak Kullachot</div>
      </div>
    </section>
  </main>

  <!-- Pyodide script เหมือนเดิม -->
  <script src="https://cdn.jsdelivr.net/pyodide/v0.24.1/full/pyodide.js"></script>
  <script>
  // โค้ด JavaScript เดิมเหมือนเดิม ไม่ต้องแก้
  </script>
</body>
</html>
