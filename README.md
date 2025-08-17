Robot Logic: เป็นเกมการศึกษาที่ออกแบบมาเพื่อช่วยให้นักเรียนมัธยมศึกษาเรียนรู้การเขียนโปรแกรมภาษา Python ผ่านการควบคุมหุ่นยนต์ในสถานการณ์จำลอง โดยผู้เล่นจะต้องใช้ความรู้พื้นฐานด้านการเขียนโปรแกรมเพื่อให้หุ่นยนต์สามารถผ่านด่านต่าง ๆ ได้สำเร็จ
วิธีเล่น
1. เปิดเว็บไซต์ Robot Logic ผ่านเบราว์เซอร์
2. เลือกด่านที่ต้องการเล่นจากเมนูด้านซ้าย
3. อ่านคำอธิบายของด่าน
4. เขียนโค้ด Python ในช่องด้านขวา
5. กด Ctrl + Enter เพื่อรันโค้ด
6. ตรวจสอบผลลัพธ์และปรับปรุงโค้ดตามคำแนะนำ
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Robot Logic: พิชิตด่านด้วย Python</title>
  <!--
  วิธีใช้งานกับ GitHub Pages:
  1) สร้าง repository ใหม่ เช่น robot-logic
  2) วางไฟล์นี้ชื่อ index.html ไว้ที่ราก repo แล้ว commit/push
  3) เปิด Settings ▸ Pages ▸ เลือก Deploy from branch (main) และโฟลเดอร์ /root
  4) รอ build เสร็จ จากนั้นเปิดลิงก์ GitHub Pages ของ repo

  หน้านี้ใช้ Pyodide เพื่อรัน Python ในเบราว์เซอร์ (ออฟไลน์ได้หลังโหลดครั้งแรก)
  -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#0b1020; --panel:#121833; --panel-2:#0f1530; --text:#e7ebff; --muted:#9db0ff;
      --accent:#6ea8fe; --accent-2:#a78bfa; --ok:#24d67b; --warn:#ffcf5a; --err:#ff6b6b;
      --code:#0b1229; --border:rgba(255,255,255,.08);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;background:radial-gradient(1200px 600px at 10% -10%, rgba(167,139,250,.15), transparent),
                 radial-gradient(1000px 700px at 110% 10%, rgba(110,168,254,.12), transparent),
                 var(--bg);
         color:var(--text);font-family:"Noto Sans Thai", system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, sans-serif;}
    header{position:sticky;top:0;z-index:50;background:linear-gradient(180deg, rgba(11,16,32,.95) 0%, rgba(11,16,32,.7) 100%);
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
          border:1px solid var(--border);border-radius:18px;box-shadow:0 10px 40px rgba(0,0,0,.25)}
    .sidebar{padding:14px}
    .search{display:flex;gap:8px;margin-bottom:10px}
    .search input{width:100%;padding:10px 12px;border-radius:12px;border:1px solid var(--border);background:rgba(255,255,255,.03);color:var(--text)}

    .menu{display:grid;gap:8px}
    .menu button{appearance:none;border:none;text-align:left;padding:12px 12px;border-radius:12px;cursor:pointer;color:var(--text);
                 background:rgba(255,255,255,.03);border:1px solid var(--border);transition:.15s}
    .menu button:hover{transform:translateY(-1px);}
    .menu button.active{outline:2px solid var(--accent); background:linear-gradient(180deg, rgba(110,168,254,.15), rgba(255,255,255,.03))}

    .main{display:grid;gap:16px}
    .pane{padding:16px}

    .badges{display:flex;flex-wrap:wrap;gap:8px}
    .badge{padding:6px 10px;border-radius:999px;font-size:.85rem;background:rgba(255,255,255,.06);border:1px solid var(--border);color:var(--muted)}

    .editor{display:grid;gap:12px}
    .editor textarea{width:100%;min-height:240px;resize:vertical;border-radius:14px;padding:12px 12px 36px 12px;font-family:ui-monospace, Menlo, SFMono-Regular, Consolas, "Liberation Mono", monospace;
                     background:var(--code);color:#dfe6ff;border:1px solid var(--border)}

    .toolbar{display:flex;flex-wrap:wrap;gap:8px;align-items:center}
    .toolbar button{appearance:none;border:none;border-radius:12px;padding:10px 14px;cursor:pointer;color:#071025;font-weight:700
                    ;background:var(--accent);box-shadow:0 6px 14px rgba(110,168,254,.35);}
    .ghost{background:transparent !important;color:var(--text) !important;border:1px solid var(--border)}
    .secondary{background:var(--accent-2)}

    .io{display:grid;grid-template-columns:1fr;gap:10px}
    .io pre{margin:0;background:#081226;border-radius:12px;border:1px solid var(--border);padding:12px;overflow:auto}

    .footer{padding:12px 16px;color:var(--muted);text-align:center}
    .pill{display:inline-flex;align-items:center;gap:6px;padding:6px 10px;border-radius:999px;background:rgba(255,255,255,.06);border:1px solid var(--border)}
    .status-dot{width:10px;height:10px;border-radius:999px;background:var(--warn)}
    .status-ok{background:var(--ok)}
    .status-err{background:var(--err)}

    .kbd{font-family:ui-monospace,monospace;background:rgba(255,255,255,.08);padding:0 6px;border-radius:6px;border:1px solid var(--border)}
    .hint{color:var(--muted)}
    .link{color:var(--accent);text-decoration:none}
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

  <!-- Pyodide: โหลด Python สำหรับเบราว์เซอร์ -->
  <script>
    const PYODIDE_VERSION = "0.24.1"; // ทดแทนได้หากต้องการรุ่นใหม่กว่า
    let pyodide = null;

    const levels = [
      {
        id: 1,
        title: "ด่านที่ 1: การประกาศตัวแปร",
        keywords: ["var","ตัวแปร","variable"],
        desc: `กำหนดค่าเริ่มต้นให้หุ่นยนต์:
- สร้างตัวแปรชื่อ name เก็บชื่อหุ่นยนต์เป็นสตริง
- สร้างตัวแปร energy เป็นจำนวนเต็ม เริ่มที่ 100
- สร้างตัวแปร speed เป็นจำนวนจริง 1.5
พิมพ์ค่าด้านล่างนี้ออกมาทีละบรรทัด`,

starter: `# TODO: สร้างตัวแปรให้ครบ แล้วพิมพ์ออกมาทีละบรรทัด`,

judge: async () => {
    return await pyRun(`
try:
    assert isinstance(name, str), "name ต้องเป็นสตริง"
    assert energy == 100 and isinstance(energy, int), "energy ต้องเป็น 100 (int)"
    assert abs(speed - 1.5) < 1e-9, "speed ต้องเป็น 1.5"
    print("ผ่านด่าน 1 ✅")
except AssertionError as e:
    import sys
    print("ไม่ผ่าน ❌:", e)
`);
        }
      },
      {
  id: 2,
  title: "ด่านที่ 2: ตัวดำเนินการทางคณิตศาสตร์",
  keywords: ["math", "+ - * /", "คณิต"],
  desc: `คำนวณพลังงานหลังการเคลื่อนที่:
ให้สร้างตัวแปร moves เป็นจำนวนก้าวที่หุ่นยนต์เคลื่อน เช่น 12
คำนวณ cost = moves * 3 + 5 // 2 (ปัดเศษลง) และพลังงานคงเหลือ left = 200 - cost
พิมพ์ left`,
  starter: `# TODO: คำนวณพลังงานคงเหลือ`,
  judge: async () => {
    return await pyRun(`
try:
    assert 'moves' in globals(), "ต้องมี moves"
    expect = 200 - (moves * 3 + 5 // 2)
    assert left == expect, f"left ควรเป็น {expect}"
    print("ผ่านด่าน 2 ✅")
except AssertionError as e:
    print("ไม่ผ่าน ❌:", e)
`)
  }
      },
      {
        id: 3,
        title: "ด่านที่ 3: if – else",
        keywords: ["if","else","เงื่อนไข"],
        desc: `สร้างฟังก์ชัน <code>move_or_charge(battery)</code>
ถ้าแบตเตอรี่ ≥ 50 ให้คืนค่า <code>"move"</code> มิฉะนั้นคืนค่า <code>"charge"</code>`,
        starter: `# TODO: สร้างฟังก์ชันตามเงื่อนไข

def move_or_charge(battery):
    if battery >= 50:
        return "move"
    else:
        return "charge"

print(move_or_charge(75))
`,
        judge: async () => await pyRun(`
try:
    assert move_or_charge(70)=="move"
    assert move_or_charge(50)=="move"
    assert move_or_charge(10)=="charge"
    print("ผ่านด่าน 3 ✅")
except Exception as e:
    print("ไม่ผ่าน ❌:", e)
`) },
      {
        id: 4,
        title: "ด่านที่ 4: List",
        keywords: ["list","รายการ"],
        desc: `สร้างรายการคำสั่ง <code>commands</code> ที่มีอย่างน้อย 4 รายการ เช่น "up", "right", "down", "left"
พิมพ์คำสั่งตัวแรกและตัวสุดท้าย`,
        starter: `# TODO: สร้าง list ของคำสั่งแล้วพิมพ์ตัวแรก/สุดท้าย
commands = ["up","right","down","left"]
print(commands[0])
print(commands[-1])
`,
        judge: async () => await pyRun(`
try:
    assert isinstance(commands, list) and len(commands)>=4
    assert commands[0] and commands[-1]
    print("ผ่านด่าน 4 ✅")
except Exception as e:
    print("ไม่ผ่าน ❌:", e)
`) },
      {
        id: 5,
        title: "ด่านที่ 5: for loop",
        keywords: ["for","ลูป"],
        desc: `สร้างฟังก์ชัน <code>repeat_cmd(cmd, n)</code> คืนค่า List ที่มี <code>cmd</code> ซ้ำกัน <code>n</code> ครั้ง
ตัวอย่าง: repeat_cmd("up", 3) -> ["up","up","up"]`,
        starter: `# TODO: เขียนฟังก์ชันด้วย for

def repeat_cmd(cmd, n):
    result = []
    for _ in range(n):
        result.append(cmd)
    return result

print(repeat_cmd("up", 3))
`,
        judge: async () => await pyRun(`
try:
    assert repeat_cmd("x",0)==[]
    assert repeat_cmd("up",3)==["up","up","up"]
    print("ผ่านด่าน 5 ✅")
except Exception as e:
    print("ไม่ผ่าน ❌:", e)
`) },
      {
        id: 6,
        title: "ด่านที่ 6: while loop",
        keywords: ["while","ลูป"],
        desc: `สร้างฟังก์ชัน <code>drain(b)</code> ลดค่าแบตทีละ 10 จนกว่าจะ ≤ 0 และคืนค่าจำนวนครั้งที่ลดลง
ตัวอย่าง: drain(35) -> 4 (35→25→15→5→-5)`,
        starter: `# TODO: ใช้ while เพื่อนับรอบการลด

def drain(b):
    count = 0
    while b > 0:
        b -= 10
        count += 1
    return count

print(drain(35))
`,
        judge: async () => await pyRun(`
try:
    assert drain(0)==0
    assert drain(5)==1
    assert drain(35)==4
    print("ผ่านด่าน 6 ✅")
except Exception as e:
    print("ไม่ผ่าน ❌:", e)
`) },
      {
        id: 7,
        title: "ด่านที่ 7: if – elif – else",
        keywords: ["elif","เงื่อนไขหลายทาง"],
        desc: `สร้างฟังก์ชัน <code>classify_cell(code)</code> ดังนี้:
- ถ้า code == 0 คืนค่า "empty"
- ถ้า code == 1 คืนค่า "wall"
- ถ้า code == 9 คืนค่า "goal"
- อื่นๆ คืนค่า "unknown"`,
        starter: `# TODO: เขียนฟังก์ชันด้วย if-elif-else

def classify_cell(code):
    if code == 0:
        return "empty"
    elif code == 1:
        return "wall"
    elif code == 9:
        return "goal"
    else:
        return "unknown"

print(classify_cell(9))
`,
        judge: async () => await pyRun(`
try:
    assert classify_cell(0)=="empty"
    assert classify_cell(1)=="wall"
    assert classify_cell(9)=="goal"
    assert classify_cell(7)=="unknown"
    print("ผ่านด่าน 7 ✅")
except Exception as e:
    print("ไม่ผ่าน ❌:", e)
`) }
    ];

    function renderMenu(filter=""){
      const menu = document.getElementById('menu');
      menu.innerHTML = '';
      levels
        .filter(l => (l.title + ' ' + l.keywords.join(' ')).toLowerCase().includes(filter.toLowerCase()))
        .forEach(l => {
          const b = document.createElement('button');
          b.textContent = `${l.id}. ${l.title}`;
          b.onclick = () => selectLevel(l.id);
          b.id = `menu-${l.id}`;
          menu.appendChild(b);
        });
    }

    let currentLevel = null;

    function selectLevel(id){
      currentLevel = levels.find(l => l.id===id);
      document.querySelectorAll('.menu button').forEach(el=>el.classList.remove('active'));
      document.getElementById(`menu-${id}`).classList.add('active');
      document.getElementById('level-title').innerText = currentLevel.title;
      document.getElementById('level-desc').innerHTML = currentLevel.desc;
      document.getElementById('code').value = currentLevel.starter;
      document.getElementById('stdout').textContent = '';
      document.getElementById('judge').textContent = '';
    }

    async function boot(){
      renderMenu();
      selectLevel(1);
      document.getElementById('search').addEventListener('input', (e)=>{
        renderMenu(e.target.value || '');
      });

      document.getElementById('btn-run').addEventListener('click', runUserCode);
      document.getElementById('btn-check').addEventListener('click', judgeLevel);
      document.getElementById('btn-reset').addEventListener('click', ()=>{
        if(currentLevel) document.getElementById('code').value = currentLevel.starter;
      });
      document.getElementById('btn-copy').addEventListener('click', ()=>{
        navigator.clipboard.writeText(document.getElementById('code').value);
        toast('คัดลอกโค้ดแล้ว');
      });

      document.getElementById('code').addEventListener('keydown', (e)=>{
        if(e.key==='Enter' && (e.ctrlKey||e.metaKey)){
          e.preventDefault();
          runUserCode();
        }
      });

      setRuntimeStatus('กำลังโหลด Python…', 'warn');
      try{
        pyodide = await loadPyodide({indexURL: `https://cdn.jsdelivr.net/pyodide/v${PYODIDE_VERSION}/full/`});
        // support input()
        await pyodide.runPythonAsync(`
import sys
from js import window

class _PromptIn:
    def readline(self):
        return window.prompt("input()", "") + "\n"

sys.stdin = _PromptIn()
`);
        setRuntimeStatus('พร้อมใช้งาน Python', 'ok');
      }catch(err){
        setRuntimeStatus('โหลด Python ไม่สำเร็จ', 'err');
        console.error(err);
      }
    }

    function setRuntimeStatus(text, kind){
      const dot = document.getElementById('runtime-dot');
      const label = document.getElementById('runtime-status');
      label.textContent = text;
      dot.classList.remove('status-ok','status-err');
      if(kind==='ok') dot.classList.add('status-ok');
      if(kind==='err') dot.classList.add('status-err');
    }

    async function runUserCode(){
      if(!pyodide) return;
      const code = document.getElementById('code').value;
      const out = await pyRun(code, true);
      document.getElementById('stdout').textContent = out.trim();
    }

    async function judgeLevel(){
      if(!pyodide || !currentLevel) return;
      // รันโค้ดผู้ใช้ใน global scope เดียวกัน แล้วเรียกตัวตรวจของด่าน
      const code = document.getElementById('code').value;
      const runOut = await pyRun(code, false);
      const judgeOut = await currentLevel.judge();
      document.getElementById('judge').textContent = (runOut? runOut+"\n":"") + judgeOut;
    }

    async function pyRun(code, capturePrint=false){
      if(!pyodide) return "ยังไม่พร้อม";
      const py = `\nimport sys, io\n__buf = io.StringIO()\n__old = sys.stdout\nsys.stdout = __buf\n` + code + `\n\n# flush\nsys.stdout = __old\n__buf.getvalue()\n`;
      try{
        const out = await pyodide.runPythonAsync(py);
        return String(out||'');
      }catch(err){
        return `ข้อผิดพลาด:\n${err}`;
      }
    }

    function toast(msg){
      const el = document.createElement('div');
      el.textContent = msg;
      el.style.position='fixed'; el.style.left='50%'; el.style.bottom='24px'; el.style.transform='translateX(-50%)';
      el.style.background='rgba(0,0,0,.7)'; el.style.color='#fff'; el.style.padding='10px 14px'; el.style.borderRadius='12px'; el.style.zIndex='9999';
      document.body.appendChild(el); setTimeout(()=>{el.remove()}, 1500);
    }

    window.addEventListener('load', boot);
  </script>
  <script src="https://cdn.jsdelivr.net/pyodide/v0.24.1/full/pyodide.js"></script>
</body>
</html>

