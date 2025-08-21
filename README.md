# skillcred
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>EduPortal — Student Success Platform</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0b1220;
      --panel: #0f172a;
      --card: #111827;
      --text: #e5e7eb;
      --muted: #94a3b8;
      --brand: #7c3aed;
      --brand-2: #22d3ee;
      --ok: #10b981;
      --warn: #f59e0b;
      --danger: #ef4444;
      --border: #1f2937;
      --chip: #1e293b;
      --shadow: 0 10px 30px rgba(0,0,0,.35);
      --radius: 16px;
    }
    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0; font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(1200px 600px at 10% -10%, rgba(124,58,237,.25), transparent),
                  radial-gradient(800px 400px at 90% -20%, rgba(34,211,238,.18), transparent),
                  var(--bg);
      color: var(--text);
    }
    .app { display: grid; grid-template-columns: 280px 1fr; min-height: 100vh; }

    /* Sidebar */
    .sidebar { position: sticky; top: 0; height: 100vh; background: linear-gradient(180deg, #0f172a, #0b1220 60%); border-right: 1px solid var(--border); padding: 22px 18px; }
    .brand { display: flex; align-items: center; gap: 12px; padding: 8px 10px; margin-bottom: 24px; }
    .logo {
      width: 40px; height: 40px; border-radius: 12px; background: linear-gradient(135deg, var(--brand), var(--brand-2));
      display: grid; place-items: center; color: white; font-weight: 800; box-shadow: var(--shadow);
    }
    .brand h1 { font-size: 18px; margin: 0; letter-spacing: .3px; }
    .sub { font-size: 12px; color: var(--muted); margin-left: 52px; margin-top: -12px; margin-bottom: 8px; }

    .nav { display: grid; gap: 6px; }
    .nav button {
      all: unset; display: flex; align-items: center; gap: 10px; padding: 10px 12px; border-radius: 12px; cursor: pointer; color: var(--text);
    }
    .nav button:hover { background: #0d162a; }
    .nav button.active { background: linear-gradient(90deg, rgba(124,58,237,.18), rgba(34,211,238,.12)); border: 1px solid #2a3650; }
    .nav .dot { width: 8px; height: 8px; border-radius: 999px; background: var(--brand-2); box-shadow: 0 0 0 3px rgba(34,211,238,.18); }

    .sidebar .footer { position: absolute; bottom: 20px; left: 18px; right: 18px; font-size: 12px; color: var(--muted); }

    /* Main */
    .main { padding: 22px; }
    .topbar { display: flex; align-items: center; justify-content: space-between; margin-bottom: 18px; }
    .search { flex: 1; max-width: 520px; background: #0f172a; border: 1px solid var(--border); border-radius: 999px; padding: 10px 14px; display: flex; gap: 10px; }
    .search input { all: unset; flex: 1; font-size: 14px; color: var(--text); }

    .profile { display: flex; align-items: center; gap: 12px; }
    .avatar { width: 38px; height: 38px; border-radius: 12px; background: linear-gradient(135deg, #1f2937, #0b1220); border: 1px solid var(--border); }
    .chip { background: var(--chip); color: var(--muted); padding: 6px 10px; border-radius: 999px; border: 1px solid var(--border); font-size: 12px; }

    /* Panels & Cards */
    .panel { background: rgba(15,23,42,.65); border: 1px solid var(--border); backdrop-filter: blur(6px); border-radius: var(--radius); box-shadow: var(--shadow); }
    .panel.header { padding: 18px 18px 0; }
    .grid { display: grid; grid-template-columns: repeat(12, 1fr); gap: 14px; }
    .card { background: var(--card); border: 1px solid var(--border); border-radius: 14px; padding: 16px; }
    .card h3 { margin: 0 0 10px; font-size: 16px; }
    .muted { color: var(--muted); font-size: 13px; }
    .note { background: rgba(124,58,237,.08); border: 1px dashed rgba(124,58,237,.4); padding: 12px; border-radius: 12px; }
    .btn { all: unset; background: linear-gradient(135deg, var(--brand), var(--brand-2)); padding: 10px 14px; border-radius: 12px; font-weight: 600; cursor: pointer; box-shadow: var(--shadow); display: inline-block; }
    .btn.ghost { background: transparent; border: 1px solid var(--border); box-shadow: none; }
    .btn.danger { background: linear-gradient(135deg, #ef4444, #f97316); }

    /* Forms */
    label { display: block; font-size: 13px; color: var(--muted); margin-bottom: 6px; }
    input[type="text"], input[type="tel"], input[type="number"], input[type="date"], input[type="time"], select, textarea {
      width: 100%; background: #0b1220; color: var(--text); border: 1px solid var(--border); padding: 12px; border-radius: 12px; outline: none; transition: border .2s ease;
    }
    textarea { resize: vertical; min-height: 120px; }
    input:focus, select:focus, textarea:focus { border-color: #2a3650; box-shadow: 0 0 0 3px rgba(124,58,237,.15); }

    /* Sections */
    .section { display: none; }
    .section.active { display: block; }

    .table { width: 100%; border-collapse: collapse; }
    .table th, .table td { border-bottom: 1px solid var(--border); padding: 10px 8px; text-align: left; }
    .table th { color: var(--muted); font-weight: 600; font-size: 12px; }
    .table .actions { display: flex; gap: 8px; }

    .kpi { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-top: 14px; }
    .kpi .card { display: grid; gap: 6px; }
    .kpi .value { font-size: 22px; font-weight: 800; }

    .grid-2 { display: grid; grid-template-columns: repeat(2, 1fr); gap: 14px; }
    .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; }
    .grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }

    /* Onboarding Fullscreen Form */
    .onboard {
      position: fixed; inset: 0; background: radial-gradient(1200px 600px at 10% -10%, rgba(124,58,237,.25), transparent), var(--bg);
      display: none; place-items: center; padding: 24px; z-index: 50; 
    }
    .onboard.active { display: grid; }
    .on-card { width: min(920px, 94vw); background: rgba(15,23,42,.8); border: 1px solid var(--border); border-radius: 18px; box-shadow: var(--shadow); padding: 20px; }
    .on-card h2 { margin: 0 0 12px; }

    .pill { display: inline-flex; gap: 8px; padding: 6px 10px; border: 1px dashed #334155; border-radius: 999px; color: var(--muted); font-size: 12px; }

    footer { padding: 18px; color: var(--muted); text-align: center; }

    @media (max-width: 1000px) {
      .app { grid-template-columns: 1fr; }
      .sidebar { position: relative; height: auto; display: none; }
      .main { padding: 12px; }
    }
  </style>
</head>
<body>
  <div class="app">
    <!-- Sidebar -->
    <aside class="sidebar" id="sidebar">
      <div class="brand">
        <div class="logo">EP</div>
        <div>
          <h1>EduPortal</h1>
          <div class="sub">Student Success Platform</div>
        </div>
      </div>

      <div class="nav" id="nav">
        <button class="active" data-section="dashboard"><span class="dot"></span> Dashboard</button>
        <button data-section="learn"><span class="dot"></span> Learn a Topic</button>
        <button data-section="attendance"><span class="dot"></span> Attendance</button>
        <button data-section="datesheet"><span class="dot"></span> Exam Date Sheet</button>
        <button data-section="syllabus"><span class="dot"></span> Syllabus</button>
        <button data-section="timetable"><span class="dot"></span> Time Table</button>
        <button data-section="cpi"><span class="dot"></span> CPI / CGPA</button>
        <button data-section="profile"><span class="dot"></span> Profile</button>
        <button id="logoutBtn"><span class="dot" style="background: var(--danger);"></span> Logout</button>
      </div>

      <div class="footer">© <span id="year"></span> EduPortal • Crafted for a corporate feel ✨</div>
    </aside>

    <!-- Main -->
    <main class="main">
      <div class="topbar">
        <div class="search"><input placeholder="Search anything (UI only)…" /></div>
        <div class="profile">
          <span class="chip" id="helloChip">Welcome</span>
          <div class="avatar"></div>
        </div>
      </div>

      <!-- DASHBOARD -->
      <section class="section active" id="dashboard">
        <div class="panel header">
          <h2 style="margin:0 0 6px">Good to see you, <span id="studentName">Student</span> 👋</h2>
          <div class="muted">Course: <span id="studentCourse"></span> • College: <span id="studentCollege"></span> • Year: <span id="studentYear"></span> • Contact: <span id="studentContact"></span></div>
          <div class="kpi">
            <div class="card">
              <div class="muted">Attendance</div>
              <div class="value" id="kpiAttendance">—%</div>
              <div class="muted">Target: 75%</div>
            </div>
            <div class="card">
              <div class="muted">Exams Scheduled</div>
              <div class="value" id="kpiExams">0</div>
              <div class="muted">Next: <span id="kpiNextExam">—</span></div>
            </div>
            <div class="card">
              <div class="muted">Syllabus Notes</div>
              <div class="value" id="kpiSyllabus">0</div>
              <div class="muted">Saved items</div>
            </div>
            <div class="card">
              <div class="muted">Weekly Classes</div>
              <div class="value" id="kpiTT">0</div>
              <div class="muted">In timetable</div>
            </div>
          </div>
        </div>
      </section>

      <!-- LEARN A TOPIC -->
      <section class="section" id="learn">
        <div class="grid-2">
          <div class="card">
            <h3>📘 Learn a Topic</h3>
            <label>Subject</label>
            <input type="text" id="subjectInput" placeholder="e.g. maths, science, computer" />
            <label style="margin-top:8px;">Topic</label>
            <input type="text" id="topicInput" placeholder="e.g. integration, arrays" />
            <div style="display:flex; gap:10px; margin-top:12px;">
              <button class="btn" id="teachBtn">Teach Me</button>
              <button class="btn ghost" id="clearLearn">Clear</button>
            </div>
            <div class="note" id="topicResult" style="margin-top:12px; display:none;"></div>
          </div>
          <div class="card">
            <h3>➕ Add / Update Topic</h3>
            <label>Subject</label>
            <input type="text" id="kbSubject" placeholder="e.g. maths" />
            <label>Topic</label>
            <input type="text" id="kbTopic" placeholder="e.g. matrices" />
            <label>Easy Explanation</label>
            <textarea id="kbExplanation" placeholder="Explain like I'm 15…"></textarea>
            <button class="btn" id="saveTopicBtn">Save Topic</button>
            <div class="muted" id="kbSaveMsg" style="margin-top:8px"></div>
          </div>
        </div>
      </section>

      <!-- ATTENDANCE -->
      <section class="section" id="attendance">
        <div class="grid-3">
          <div class="card">
            <h3>📊 Attendance Calculator</h3>
            <label>Total Classes</label><input type="number" id="totalClasses" min="0" />
            <label>Attended Classes</label><input type="number" id="attendedClasses" min="0" />
            <label>Target %</label><input type="number" id="targetPercent" min="1" max="100" value="75" />
            <button class="btn" id="calcAttendanceBtn">Calculate</button>
            <div class="note" id="attendanceResult" style="margin-top:10px"></div>
          </div>
          <div class="card">
            <h3>💡 Strategy</h3>
            <div class="muted">We help you figure out how many consecutive classes you need to attend to reach your target percentage. Data is saved locally.</div>
            <div class="pill" style="margin-top:10px;">Saved automatically</div>
          </div>
          <div class="card">
            <h3>Quick Entry</h3>
            <div style="display:flex; gap:8px;">
              <button class="btn ghost" id="demo75">Demo 60/80</button>
              <button class="btn ghost" id="demo90">Demo 90/100</button>
            </div>
          </div>
        </div>
      </section>

      <!-- DATE SHEET -->
      <section class="section" id="datesheet">
        <div class="card">
          <h3>🗓️ Exam Date Sheet</h3>
          <div class="grid-4">
            <div><label>Subject</label><input id="dsSubject" /></div>
            <div><label>Date</label><input type="date" id="dsDate" /></div>
            <div><label>Time</label><input type="time" id="dsTime" /></div>
            <div style="display:flex; align-items:end; gap:8px;">
              <button class="btn" id="addDateBtn">Add / Update</button>
              <button class="btn ghost" id="exportDS">Export</button>
              <button class="btn ghost" id="clearDS">Clear</button>
            </div>
          </div>
          <table class="table" style="margin-top:12px" id="dateTable">
            <thead><tr><th>Subject</th><th>Date</th><th>Time</th><th>Actions</th></tr></thead>
            <tbody></tbody>
          </table>
          <div class="muted" style="margin-top:8px;">Next exam: <span id="nextExam">—</span></div>
        </div>
      </section>

      <!-- SYLLABUS -->
      <section class="section" id="syllabus">
        <div class="grid-2">
          <div class="card">
            <h3>📄 Syllabus Notes</h3>
            <textarea id="syllabusText" placeholder="- Unit 1: ...&#10;- Unit 2: ..."></textarea>
            <div style="display:flex; gap:8px; margin-top:10px;">
              <button class="btn" id="saveSyllabusBtn">Save</button>
              <button class="btn ghost" id="clearSyllabusBtn">Clear</button>
            </div>
            <div class="muted" id="syllabusMsg" style="margin-top:8px"></div>
          </div>
          <div class="card">
            <h3>Tips</h3>
            <ul class="muted" style="margin-top:0; padding-left:18px; line-height:1.7;">
              <li>Break topics into small, testable points.</li>
              <li>Mark important formulas/theorems with ⭐.</li>
              <li>Keep last-minute revision list at the bottom.</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- TIME TABLE -->
      <section class="section" id="timetable">
        <div class="card">
          <h3>⏰ Weekly Time Table</h3>
          <div class="grid-4">
            <div><label>Day</label>
              <select id="ttDay">
                <option value="">Day</option>
                <option>Monday</option><option>Tuesday</option><option>Wednesday</option>
                <option>Thursday</option><option>Friday</option><option>Saturday</option><option>Sunday</option>
              </select>
            </div>
            <div><label>Subject</label><input id="ttSubject" /></div>
            <div><label>Start</label><input type="time" id="ttStart" /></div>
            <div><label>End</label><input type="time" id="ttEnd" /></div>
          </div>
          <div style="display:flex; gap:8px; margin-top:10px;">
            <button class="btn" id="addTTBtn">Add / Update</button>
            <button class="btn ghost" id="clearTT">Clear</button>
          </div>
          <table class="table" id="ttTable" style="margin-top:12px">
            <thead><tr><th>Day</th><th>Subject</th><th>Start</th><th>End</th><th>Actions</th></tr></thead>
            <tbody></tbody>
          </table>
        </div>
      </section>

      <!-- CPI / CGPA -->
      <section class="section" id="cpi">
        <div class="card">
          <h3>🎯 CPI / CGPA Calculator</h3>
          <div class="muted">Grade mapping: O=10, A+=9, A=8, B+=7, B=6, C=5, P=4, F=0</div>
          <div class="grid-4" style="margin-top:8px;">
            <input id="cgSub" placeholder="Course/Subject" />
            <input type="number" id="cgCred" placeholder="Credits" min="0" />
            <select id="cgGrade">
              <option value="">Grade</option><option>O</option><option>A+</option><option>A</option><option>B+</option>
              <option>B</option><option>C</option><option>P</option><option>F</option>
            </select>
            <button class="btn" id="addCGRowBtn">Add Row</button>
          </div>
          <table class="table" id="cgTable" style="margin-top:12px;">
            <thead><tr><th>Subject</th><th>Credits</th><th>Grade</th><th>Grade Point</th><th>Actions</th></tr></thead>
            <tbody></tbody>
          </table>
          <div style="display:flex; gap:8px; margin-top:10px;">
            <button class="btn" id="calcCPIBtn">Calculate CPI</button>
            <button class="btn ghost" id="clearCG">Clear</button>
          </div>
          <div class="note" id="cpiResult" style="margin-top:10px"></div>
        </div>
      </section>

      <!-- PROFILE -->
      <section class="section" id="profile">
        <div class="grid-2">
          <div class="card">
            <h3>👤 Your Profile</h3>
            <label>Name</label><input id="pName" />
            <label>Course</label><input id="pCourse" />
            <label>College</label><input id="pCollege" />
            <label>Contact</label><input id="pContact" />
            <label>Year</label>
            <select id="pYear">
              <option>1st Year</option><option>2nd Year</option><option>3rd Year</option><option>4th Year</option>
            </select>
            <div style="display:flex; gap:8px; margin-top:10px;">
              <button class="btn" id="saveProfile">Save</button>
              <button class="btn danger" id="hardReset">Hard Reset (All Data)</button>
            </div>
          </div>
          <div class="card">
            <h3>About</h3>
            <div class="muted">Your details personalize the dashboard KPIs and greetings. You can export some modules, but everything is stored in your browser for privacy.</div>
          </div>
        </div>
      </section>

      <footer>Built with ❤️ — All data stays in your browser (localStorage).</footer>
    </main>
  </div>

  <!-- FULLSCREEN ONBOARD FORM (first time) -->
  <div class="onboard" id="onboard">
    <div class="on-card">
      <div style="display:flex; align-items:center; justify-content:space-between; gap:12px;">
        <div style="display:flex; align-items:center; gap:12px;">
          <div class="logo" style="width:46px;height:46px;">EP</div>
          <div>
            <h2 style="margin:0">Welcome to EduPortal</h2>
            <div class="muted">Please fill your details to continue</div>
          </div>
        </div>
        <span class="pill">Secure • Local Only</span>
      </div>
      <div class="grid-2" style="margin-top:14px;">
        <div>
          <label>Student Name</label><input id="oName" placeholder="Your full name" />
          <label>Course</label><input id="oCourse" placeholder="e.g. B.Tech CSE" />
          <label>College</label><input id="oCollege" placeholder="Your college" />
        </div>
        <div>
          <label>Contact (10 digits)</label><input id="oContact" placeholder="9999999999" />
          <label>Course Year</label>
          <select id="oYear"><option>1st Year</option><option>2nd Year</option><option>3rd Year</option><option>4th Year</option></select>
          <button class="btn" id="oSubmit" style="margin-top:16px; width:100%">Enter Portal</button>
        </div>
      </div>
      <div class="muted" style="margin-top:10px">By continuing, you agree to store your data in your browser's storage.</div>
    </div>
  </div>

  <script>
    // ===== Helpers
    const $ = (s) => document.querySelector(s);
    const $$ = (s) => document.querySelectorAll(s);
    const YEAR = $('#year');
    $('#year').textContent = new Date().getFullYear();

    function getLS(key, fallback) { try { return JSON.parse(localStorage.getItem(key)) ?? fallback; } catch(e){ return fallback; } }
    function setLS(key, val) { localStorage.setItem(key, JSON.stringify(val)); }

    // ===== Onboard (first time form)
    const studentKey = 'studentData';

    function showOnboard(){ $('#onboard').classList.add('active'); }
    function hideOnboard(){ $('#onboard').classList.remove('active'); }

    function loadStudent(){ return getLS(studentKey, null); }

    function fillProfileUI(st){
      if(!st) return;
      $('#studentName').textContent = st.name || 'Student';
      $('#studentCourse').textContent = st.course || '—';
      $('#studentCollege').textContent = st.college || '—';
      $('#studentYear').textContent = st.year || '—';
      $('#studentContact').textContent = st.contact || '—';
      $('#helloChip').textContent = `Welcome, ${st.name?.split(' ')[0] || 'Student'}`;
      // profile section fields
      $('#pName').value = st.name || '';
      $('#pCourse').value = st.course || '';
      $('#pCollege').value = st.college || '';
      $('#pContact').value = st.contact || '';
      $('#pYear').value = st.year || '1st Year';
    }

    function initKB(){
      if (!localStorage.getItem('knowledgeBase')) {
        const seedKB = {
          maths: {
            integration: "Integration is the reverse of differentiation. It helps find area under a curve. Example: ∫ x dx = (x²/2) + C.",
            derivative: "Derivative tells the rate of change. Example: d(x²)/dx = 2x."
          },
          science: {
            photosynthesis: "Plants make food using sunlight, water and carbon dioxide. It produces glucose and oxygen.",
            respiration: "Cells break glucose to release energy (ATP) using oxygen."
          },
          computer: {
            arrays: "An array stores multiple values under one name, accessed by index starting at 0.",
            loops: "Loops repeat code. Types: for, while, do-while."
          }
        };
        setLS('knowledgeBase', seedKB);
      }
    }

    function ensureModules(){
      ['dateSheet','timeTable','cgRows'].forEach(key => { if(!localStorage.getItem(key)) setLS(key, []); });
      if(!localStorage.getItem('syllabusText')) localStorage.setItem('syllabusText','');
    }

    function boot(){
      const st = loadStudent();
      if(!st){ showOnboard(); } else { hideOnboard(); fillProfileUI(st); }
      initKB();
      ensureModules();
      renderAll();
    }

    // Onboard submit
    $('#oSubmit').addEventListener('click', () => {
      const name = $('#oName').value.trim();
      const course = $('#oCourse').value.trim();
      const college = $('#oCollege').value.trim();
      const contact = $('#oContact').value.trim();
      const year = $('#oYear').value;
      if(!name || !course || !college || !/^\d{10}$/.test(contact) || !year){
        alert('Please fill all fields correctly (contact must be 10 digits).'); return;
      }
      const student = { name, course, college, contact, year, createdAt: Date.now() };
      setLS(studentKey, student);
      hideOnboard();
      fillProfileUI(student);
    });

    // ===== Navigation
    $$('#nav button').forEach(btn => {
      if(btn.id === 'logoutBtn') return;
      btn.addEventListener('click', () => {
        $$('#nav button').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        const sec = btn.dataset.section;
        $$('.section').forEach(s => s.classList.remove('active'));
        $('#'+sec).classList.add('active');
      });
    });

    // Logout
    $('#logoutBtn').addEventListener('click', () => {
      if(confirm('Log out and clear your profile? (Your academic data will remain)')){
        localStorage.removeItem('studentData');
        location.reload();
      }
    });

    // ===== Learn a Topic
    function getKB(){ return getLS('knowledgeBase', {}); }
    function setKB(kb){ setLS('knowledgeBase', kb); }

    $('#teachBtn').addEventListener('click', () => {
      const subject = $('#subjectInput').value.trim().toLowerCase();
      const topic = $('#topicInput').value.trim().toLowerCase();
      const res = $('#topicResult');
      const kb = getKB();
      if(subject && topic && kb[subject] && kb[subject][topic]){
        res.style.display = 'block';
        res.innerHTML = `<b>${topic.toUpperCase()}</b><br>${kb[subject][topic]}`;
      } else {
        res.style.display = 'block';
        res.textContent = '❌ Topic not found. Add it on the right and try again!';
      }
    });
    $('#clearLearn').addEventListener('click', ()=>{
      $('#subjectInput').value = '';
      $('#topicInput').value = '';
      $('#topicResult').style.display = 'none';
    });

    $('#saveTopicBtn').addEventListener('click', () => {
      const s = $('#kbSubject').value.trim().toLowerCase();
      const t = $('#kbTopic').value.trim().toLowerCase();
      const e = $('#kbExplanation').value.trim();
      const msg = $('#kbSaveMsg');
      if(!s || !t || !e){ msg.textContent = 'Please fill subject, topic and explanation.'; return; }
      const kb = getKB();
      if(!kb[s]) kb[s] = {}; kb[s][t] = e; setKB(kb);
      msg.textContent = `Saved: ${s} → ${t}`;
      $('#kbSubject').value = $('#kbTopic').value = $('#kbExplanation').value = '';
    });

    // ===== Attendance
    function saveAttendance(total, attended){ setLS('attendance', {total, attended}); }
    function loadAttendance(){ return getLS('attendance', {total:0, attended:0}); }

    function calcAttendance(total, attended, target){
      const percent = total>0 ? (attended/total)*100 : 0;
      let msg = `Your attendance is ${percent.toFixed(2)}%.`;
      if(percent < target){
        let x = 0; while(((attended + x)/(total + x))*100 < target) x++;
        msg += ` You need to attend next ${x} class(es) without missing to reach ${target}%.`;
      } else { msg += ` ✅ You meet the ${target}% target.`; }
      return { percent, msg };
    }

    function renderAttendance(){
      const a = loadAttendance();
      $('#totalClasses').value = a.total || '';
      $('#attendedClasses').value = a.attended || '';
      const { percent } = calcAttendance(a.total||0, a.attended||0, 75);
      $('#kpiAttendance').textContent = isFinite(percent)? `${percent.toFixed(1)}%` : '—%';
    }

    $('#calcAttendanceBtn').addEventListener('click', () => {
      const total = parseInt($('#totalClasses').value||'0',10);
      const attended = parseInt($('#attendedClasses').value||'0',10);
      const target = parseFloat($('#targetPercent').value||'75');
      if(total <= 0 || attended < 0 || attended > total || target <= 0 || target > 100){
        $('#attendanceResult').textContent = 'Please enter valid numbers.'; return;
      }
      saveAttendance(total, attended);
      const { msg, percent } = calcAttendance(total, attended, target);
      $('#attendanceResult').textContent = msg;
      $('#kpiAttendance').textContent = `${percent.toFixed(1)}%`;
    });

    $('#demo75').addEventListener('click',()=>{ $('#totalClasses').value=80; $('#attendedClasses').value=60; $('#targetPercent').value=75; });
    $('#demo90').addEventListener('click',()=>{ $('#totalClasses').value=100; $('#attendedClasses').value=90; $('#targetPercent').value=85; });

    // ===== Date Sheet
    const DS_KEY = 'dateSheet';
    function getDS(){ return getLS(DS_KEY, []); }
    function setDS(v){ setLS(DS_KEY, v); }
    function renderDS(){
      const tbody = $('#dateTable tbody'); tbody.innerHTML = '';
      const rows = getDS().sort((a,b)=> new Date(a.date+' '+a.time) - new Date(b.date+' '+b.time));
      rows.forEach((r,i)=>{
        const tr = document.createElement('tr');
        tr.innerHTML = `<td>${r.subject}</td><td>${r.date}</td><td>${r.time}</td>
          <td class="actions"><button class="btn ghost" data-i="${i}" data-act="edit">Edit</button>
          <button class="btn danger" data-i="${i}" data-act="del">Delete</button></td>`;
        tbody.appendChild(tr);
      });
      // KPI next exam
      const upcoming = rows.find(r => new Date(r.date+' '+r.time) >= new Date());
      $('#nextExam').textContent = upcoming ? `${upcoming.subject} on ${upcoming.date} ${upcoming.time}` : '—';
      $('#kpiExams').textContent = rows.length;
      $('#kpiNextExam').textContent = upcoming ? `${upcoming.subject}` : '—';
    }

    $('#addDateBtn').addEventListener('click', ()=>{
      const subject = $('#dsSubject').value.trim();
      const date = $('#dsDate').value; const time = $('#dsTime').value;
      if(!subject || !date || !time){ alert('Fill subject, date, and time.'); return; }
      const arr = getDS();
      const idx = arr.findIndex(x => x.subject.toLowerCase()===subject.toLowerCase());
      const payload = { subject, date, time };
      if(idx>=0) arr[idx]=payload; else arr.push(payload);
      setDS(arr); renderDS();
      $('#dsSubject').value=''; $('#dsDate').value=''; $('#dsTime').value='';
    });

    $('#dateTable').addEventListener('click', (e)=>{
      const btn = e.target.closest('button'); if(!btn) return;
      const i = +btn.dataset.i; const act = btn.dataset.act; const arr = getDS();
      if(act==='edit'){ const r=arr[i]; $('#dsSubject').value=r.subject; $('#dsDate').value=r.date; $('#dsTime').value=r.time; }
      if(act==='del'){ arr.splice(i,1); setDS(arr); renderDS(); }
    });

    $('#exportDS').addEventListener('click', ()=>{
      const data = JSON.stringify(getDS(), null, 2);
      const blob = new Blob([data], {type:'application/json'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href = url; a.download = 'date-sheet.json'; a.click(); URL.revokeObjectURL(url);
    });
    $('#clearDS').addEventListener('click', ()=>{ if(confirm('Clear all exams?')){ setDS([]); renderDS(); } });

    // ===== Syllabus
    const SYL_KEY = 'syllabusText';
    function renderSyllabus(){ $('#syllabusText').value = localStorage.getItem(SYL_KEY) || ''; $('#kpiSyllabus').textContent = ($('#syllabusText').value.match(/\n|\r|-/g)||[]).length; }
    $('#saveSyllabusBtn').addEventListener('click', ()=>{ localStorage.setItem(SYL_KEY, $('#syllabusText').value); $('#syllabusMsg').textContent='Syllabus saved.'; renderSyllabus(); });
    $('#clearSyllabusBtn').addEventListener('click', ()=>{ if(confirm('Clear syllabus?')){ localStorage.removeItem(SYL_KEY); renderSyllabus(); } });

    // ===== Timetable
    const TT_KEY = 'timeTable';
    function getTT(){ return getLS(TT_KEY, []); }
    function setTT(v){ setLS(TT_KEY, v); }
    function renderTT(){
      const tbody = $('#ttTable tbody'); tbody.innerHTML='';
      const rows = getTT();
      rows.forEach((r,i)=>{
        const tr = document.createElement('tr');
        tr.innerHTML = `<td>${r.day}</td><td>${r.subject}</td><td>${r.start}</td><td>${r.end}</td>
          <td class="actions"><button class="btn ghost" data-i="${i}" data-act="edit">Edit</button>
          <button class="btn danger" data-i="${i}" data-act="del">Delete</button></td>`;
        tbody.appendChild(tr);
      });
      $('#kpiTT').textContent = rows.length;
    }

    $('#addTTBtn').addEventListener('click', ()=>{
      const day=$('#ttDay').value; const subject=$('#ttSubject').value.trim(); const start=$('#ttStart').value; const end=$('#ttEnd').value;
      if(!day||!subject||!start||!end){ alert('Fill all timetable fields.'); return; }
      const arr=getTT();
      const idx=arr.findIndex(x=>x.day===day && x.subject.toLowerCase()===subject.toLowerCase() && x.start===start);
      const row={day,subject,start,end}; if(idx>=0) arr[idx]=row; else arr.push(row);
      setTT(arr); renderTT(); $('#ttDay').value=''; $('#ttSubject').value=''; $('#ttStart').value=''; $('#ttEnd').value='';
    });

    $('#ttTable').addEventListener('click', (e)=>{
      const btn=e.target.closest('button'); if(!btn) return; const i=+btn.dataset.i; const act=btn.dataset.act; const arr=getTT();
      if(act==='edit'){ const r=arr[i]; $('#ttDay').value=r.day; $('#ttSubject').value=r.subject; $('#ttStart').value=r.start; $('#ttEnd').value=r.end; }
      if(act==='del'){ arr.splice(i,1); setTT(arr); renderTT(); }
    });
    $('#clearTT').addEventListener('click', ()=>{ if(confirm('Clear timetable?')){ setTT([]); renderTT(); } });

    // ===== CPI/CGPA
    const GRADE_MAP = { 'O':10, 'A+':9, 'A':8, 'B+':7, 'B':6, 'C':5, 'P':4, 'F':0 };
    const CG_KEY = 'cgRows';
    function getCG(){ return getLS(CG_KEY, []); }
    function setCG(v){ setLS(CG_KEY, v); }
    function renderCG(){
      const tbody = $('#cgTable tbody'); tbody.innerHTML=''; const rows=getCG();
      rows.forEach((r,i)=>{
        const tr=document.createElement('tr');
        tr.innerHTML = `<td>${r.sub}</td><td>${r.cred}</td><td>${r.grade}</td><td>${r.gp}</td>
          <td class="actions"><button class="btn ghost" data-i="${i}" data-act="edit">Edit</button>
          <button class="btn danger" data-i="${i}" data-act="del">Delete</button></td>`;
        tbody.appendChild(tr);
      });
    }

    $('#addCGRowBtn').addEventListener('click', ()=>{
      const sub=$('#cgSub').value.trim(); const cred=parseFloat($('#cgCred').value||'0'); const grade=$('#cgGrade').value;
      if(!sub||!cred||!grade){ alert('Fill subject, credits and grade.'); return; }
      const gp=GRADE_MAP[grade]; const rows=getCG(); rows.push({sub,cred,grade,gp}); setCG(rows); renderCG();
      $('#cgSub').value=''; $('#cgCred').value=''; $('#cgGrade').value='';
    });

    $('#cgTable').addEventListener('click', (e)=>{
      const btn=e.target.closest('button'); if(!btn) return; const i=+btn.dataset.i; const act=btn.dataset.act; const rows=getCG();
      if(act==='edit'){ const r=rows[i]; $('#cgSub').value=r.sub; $('#cgCred').value=r.cred; $('#cgGrade').value=r.grade; rows.splice(i,1); setCG(rows); renderCG(); }
      if(act==='del'){ rows.splice(i,1); setCG(rows); renderCG(); }
    });

    $('#calcCPIBtn').addEventListener('click', ()=>{
      const rows=getCG(); if(!rows.length){ $('#cpiResult').textContent='Add some rows first.'; return; }
      const totCred=rows.reduce((a,r)=>a+Number(r.cred),0); const totPts=rows.reduce((a,r)=>a+Number(r.cred)*Number(r.gp),0);
      const cpi=totPts/totCred; $('#cpiResult').textContent = `Total Credits: ${totCred} | Total Grade Points: ${totPts} | CPI: ${cpi.toFixed(2)}`;
    });

    $('#clearCG').addEventListener('click', ()=>{ if(confirm('Clear CPI table?')){ setCG([]); renderCG(); $('#cpiResult').textContent=''; } });

    // ===== Profile Save & Hard Reset
    $('#saveProfile').addEventListener('click', ()=>{
      const st = loadStudent() || {}; st.name=$('#pName').value.trim(); st.course=$('#pCourse').value.trim(); st.college=$('#pCollege').value.trim(); st.contact=$('#pContact').value.trim(); st.year=$('#pYear').value;
      if(!st.name || !st.course || !st.college || !/^\d{10}$/.test(st.contact)) { alert('Fill valid profile fields.'); return; }
      setLS(studentKey, st); fillProfileUI(st); alert('Profile saved.');
    });
    $('#hardReset').addEventListener('click', ()=>{
      if(confirm('Hard reset clears ALL data (profile, exams, syllabus, timetable, CPI, topics). Continue?')){
        localStorage.clear(); location.reload();
      }
    });

    // ===== Render All Modules
    function renderAll(){ renderAttendance(); renderDS(); renderSyllabus(); renderTT(); renderCG(); }

    // Boot app
    boot();
  </script>
</body>
</html>
