[AI chat Bot.html](https://github.com/user-attachments/files/26140317/AI.chat.Bot.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Alex — AI Career Mentor</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #12121a;
    --surface2: #1a1a26;
    --border: rgba(120,100,255,0.15);
    --border2: rgba(120,100,255,0.3);
    --accent: #7c5cfc;
    --accent2: #00d4a8;
    --accent3: #ff6b9d;
    --text: #f0eeff;
    --muted: #8880aa;
    --bot-bubble: #1e1c30;
    --user-bubble: linear-gradient(135deg, #7c5cfc, #5c3dd8);
    --glow: 0 0 30px rgba(124,92,252,0.25);
    --glow2: 0 0 20px rgba(0,212,168,0.2);
    --radius: 20px;
    --radius-sm: 12px;
    --font-head: 'Syne', sans-serif;
    --font-body: 'DM Sans', sans-serif;
    --font-code: 'JetBrains Mono', monospace;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    font-family: var(--font-body);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  /* Animated background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 60% 50% at 20% 20%, rgba(124,92,252,0.12) 0%, transparent 60%),
      radial-gradient(ellipse 50% 60% at 80% 80%, rgba(0,212,168,0.08) 0%, transparent 60%),
      radial-gradient(ellipse 40% 40% at 50% 50%, rgba(255,107,157,0.05) 0%, transparent 60%);
    pointer-events: none;
    z-index: 0;
    animation: bgPulse 8s ease-in-out infinite alternate;
  }

  @keyframes bgPulse {
    0% { opacity: 0.7; }
    100% { opacity: 1; }
  }

  /* Floating particles */
  .particles { position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden; }
  .p {
    position: absolute;
    border-radius: 50%;
    animation: float linear infinite;
    opacity: 0;
  }
  @keyframes float {
    0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
    10% { opacity: 1; }
    90% { opacity: 0.6; }
    100% { transform: translateY(-100px) rotate(360deg); opacity: 0; }
  }

  /* Main container */
  #app {
    position: relative;
    z-index: 1;
    width: 100%;
    max-width: 780px;
    height: 100vh;
    max-height: 100vh;
    display: flex;
    flex-direction: column;
    background: var(--surface);
    border: 1px solid var(--border2);
    box-shadow: 0 0 80px rgba(124,92,252,0.15), 0 0 0 1px rgba(255,255,255,0.04);
    overflow: hidden;
  }

  /* HEADER */
  #header {
    padding: 18px 24px;
    background: linear-gradient(135deg, rgba(124,92,252,0.1), rgba(0,212,168,0.05));
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 16px;
    flex-shrink: 0;
  }

  /* Animated avatar */
  #avatar-wrap {
    position: relative;
    width: 52px;
    height: 52px;
    flex-shrink: 0;
  }

  #avatar-wrap::before, #avatar-wrap::after {
    content: '';
    position: absolute;
    border-radius: 50%;
    animation: ringPulse 2.5s ease-in-out infinite;
  }
  #avatar-wrap::before {
    inset: -5px;
    border: 2px solid rgba(124,92,252,0.5);
  }
  #avatar-wrap::after {
    inset: -10px;
    border: 1px solid rgba(124,92,252,0.2);
    animation-delay: 0.4s;
  }
  @keyframes ringPulse {
    0%, 100% { transform: scale(1); opacity: 0.8; }
    50% { transform: scale(1.08); opacity: 0.3; }
  }

  #avatar {
    width: 52px;
    height: 52px;
    border-radius: 50%;
    background: linear-gradient(135deg, #7c5cfc 0%, #00d4a8 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    position: relative;
    box-shadow: var(--glow);
    animation: avatarFloat 4s ease-in-out infinite;
  }
  @keyframes avatarFloat {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-3px); }
  }

  #status-dot {
    width: 12px;
    height: 12px;
    background: var(--accent2);
    border-radius: 50%;
    position: absolute;
    bottom: 2px;
    right: 2px;
    border: 2px solid var(--surface);
    animation: statusPulse 2s ease-in-out infinite;
    box-shadow: 0 0 8px var(--accent2);
  }
  @keyframes statusPulse {
    0%, 100% { transform: scale(1); box-shadow: 0 0 8px var(--accent2); }
    50% { transform: scale(1.15); box-shadow: 0 0 16px var(--accent2); }
  }

  #header-info { flex: 1; }
  #header-info h1 { font-family: var(--font-head); font-size: 18px; font-weight: 700; letter-spacing: -0.3px; background: linear-gradient(90deg, #fff 40%, var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
  #header-info p { font-size: 12px; color: var(--muted); margin-top: 2px; }

  #header-badges { display: flex; gap: 8px; }
  .badge { font-size: 10px; font-family: var(--font-head); font-weight: 600; padding: 4px 10px; border-radius: 20px; letter-spacing: 0.5px; }
  .badge-ai { background: rgba(124,92,252,0.2); color: var(--accent); border: 1px solid rgba(124,92,252,0.4); }
  .badge-live { background: rgba(0,212,168,0.15); color: var(--accent2); border: 1px solid rgba(0,212,168,0.3); }

  /* Progress bar */
  #progress-wrap {
    padding: 0 24px 12px;
    background: linear-gradient(135deg, rgba(124,92,252,0.05), rgba(0,212,168,0.02));
    border-bottom: 1px solid var(--border);
    flex-shrink: 0;
  }
  #progress-label { font-size: 11px; color: var(--muted); margin-bottom: 6px; font-family: var(--font-head); letter-spacing: 0.5px; }
  #progress-bar { height: 4px; background: rgba(255,255,255,0.06); border-radius: 4px; overflow: hidden; }
  #progress-fill {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    border-radius: 4px;
    transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: 0 0 8px var(--accent);
  }

  /* CHAT AREA */
  #chat {
    flex: 1;
    overflow-y: auto;
    padding: 20px 20px 10px;
    display: flex;
    flex-direction: column;
    gap: 14px;
    scrollbar-width: thin;
    scrollbar-color: var(--border2) transparent;
  }
  #chat::-webkit-scrollbar { width: 4px; }
  #chat::-webkit-scrollbar-track { background: transparent; }
  #chat::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 4px; }

  /* Messages */
  .msg-wrap {
    display: flex;
    gap: 10px;
    align-items: flex-end;
    animation: msgIn 0.4s cubic-bezier(0.34, 1.56, 0.64, 1) both;
  }
  @keyframes msgIn {
    from { opacity: 0; transform: translateY(16px) scale(0.95); }
    to { opacity: 1; transform: translateY(0) scale(1); }
  }
  .msg-wrap.user { flex-direction: row-reverse; }

  .mini-av {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
    background: linear-gradient(135deg, #7c5cfc, #00d4a8);
    box-shadow: 0 0 12px rgba(124,92,252,0.4);
    animation: avFloat 3s ease-in-out infinite;
  }
  @keyframes avFloat {
    0%,100%{transform:translateY(0);}
    50%{transform:translateY(-2px);}
  }
  .user .mini-av { background: linear-gradient(135deg, #ff6b9d, #7c5cfc); box-shadow: 0 0 12px rgba(255,107,157,0.4); animation: none; }

  .bubble {
    max-width: 72%;
    padding: 12px 16px;
    border-radius: var(--radius);
    font-size: 14px;
    line-height: 1.65;
    font-family: var(--font-body);
    position: relative;
    word-break: break-word;
  }
  .bot .bubble {
    background: var(--bot-bubble);
    border: 1px solid var(--border);
    border-bottom-left-radius: 5px;
    color: var(--text);
    box-shadow: 0 4px 20px rgba(0,0,0,0.3);
  }
  .user .bubble {
    background: var(--user-bubble);
    border-bottom-right-radius: 5px;
    color: #fff;
    box-shadow: 0 4px 20px rgba(124,92,252,0.35);
  }

  .bubble strong { color: var(--accent2); font-weight: 500; }
  .bubble code { font-family: var(--font-code); font-size: 12px; background: rgba(124,92,252,0.2); color: #b4a4ff; padding: 2px 6px; border-radius: 5px; border: 1px solid rgba(124,92,252,0.25); }
  .bubble pre { background: rgba(0,0,0,0.4); border: 1px solid var(--border2); border-radius: 10px; padding: 12px; margin-top: 10px; overflow-x: auto; }
  .bubble pre code { background: none; border: none; padding: 0; color: #a8e6cf; }
  .bubble .highlight { color: var(--accent3); }
  .bubble .salary { color: var(--accent2); font-weight: 500; }

  /* Info cards inside bubbles */
  .info-card {
    background: rgba(124,92,252,0.08);
    border: 1px solid rgba(124,92,252,0.2);
    border-radius: 12px;
    padding: 10px 14px;
    margin-top: 10px;
    font-size: 13px;
  }
  .info-card .card-title { font-family: var(--font-head); font-size: 11px; color: var(--accent2); letter-spacing: 1px; text-transform: uppercase; margin-bottom: 6px; }

  /* Typing indicator */
  #typing-wrap {
    display: none;
    gap: 10px;
    align-items: flex-end;
    animation: msgIn 0.3s ease both;
  }
  .typing-bubble {
    background: var(--bot-bubble);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    border-bottom-left-radius: 5px;
    padding: 14px 20px;
    display: flex;
    gap: 6px;
    align-items: center;
    box-shadow: 0 4px 20px rgba(0,0,0,0.3);
  }
  .dot {
    width: 7px;
    height: 7px;
    background: var(--accent);
    border-radius: 50%;
    animation: dotBounce 1.3s ease-in-out infinite;
    box-shadow: 0 0 6px var(--accent);
  }
  .dot:nth-child(2) { animation-delay: 0.18s; background: #a07cfc; }
  .dot:nth-child(3) { animation-delay: 0.36s; background: var(--accent2); box-shadow: 0 0 6px var(--accent2); }
  @keyframes dotBounce {
    0%,60%,100% { transform: translateY(0); }
    30% { transform: translateY(-7px); }
  }

  /* QUICK REPLIES */
  #quick-wrap {
    padding: 10px 20px;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    border-top: 1px solid var(--border);
    background: rgba(10,10,15,0.6);
    flex-shrink: 0;
    min-height: 44px;
  }
  .qr {
    font-family: var(--font-head);
    font-size: 12px;
    font-weight: 600;
    padding: 7px 15px;
    border-radius: 20px;
    border: 1px solid var(--border2);
    background: rgba(124,92,252,0.08);
    color: var(--text);
    cursor: pointer;
    transition: all 0.2s cubic-bezier(0.34,1.56,0.64,1);
    letter-spacing: 0.3px;
    white-space: nowrap;
  }
  .qr:hover {
    background: rgba(124,92,252,0.25);
    border-color: var(--accent);
    color: #fff;
    transform: translateY(-2px);
    box-shadow: 0 4px 15px rgba(124,92,252,0.3);
  }

  /* INPUT ROW */
  #input-row {
    padding: 14px 20px;
    display: flex;
    gap: 10px;
    align-items: center;
    border-top: 1px solid var(--border);
    background: var(--surface2);
    flex-shrink: 0;
  }

  #user-input {
    flex: 1;
    background: rgba(255,255,255,0.04);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 12px 18px;
    font-family: var(--font-body);
    font-size: 14px;
    color: var(--text);
    outline: none;
    transition: border-color 0.2s, box-shadow 0.2s;
    resize: none;
    height: 48px;
    line-height: 1.4;
  }
  #user-input::placeholder { color: var(--muted); }
  #user-input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(124,92,252,0.15), var(--glow);
    background: rgba(124,92,252,0.05);
  }

  #send-btn {
    width: 48px;
    height: 48px;
    border-radius: 14px;
    background: linear-gradient(135deg, var(--accent), #5c3dd8);
    border: none;
    color: #fff;
    font-size: 20px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s cubic-bezier(0.34,1.56,0.64,1);
    box-shadow: 0 4px 20px rgba(124,92,252,0.4);
    flex-shrink: 0;
  }
  #send-btn:hover {
    transform: translateY(-2px) scale(1.05);
    box-shadow: 0 8px 25px rgba(124,92,252,0.5);
  }
  #send-btn:active { transform: scale(0.97); }
  #send-btn svg { width: 20px; height: 20px; }

  /* Shimmer on send btn */
  #send-btn::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.15), transparent);
    transform: translateX(-100%);
    border-radius: 14px;
  }
  #send-btn:hover::after {
    animation: shimmer 0.6s ease forwards;
  }
  @keyframes shimmer {
    to { transform: translateX(100%); }
  }
  #send-btn { position: relative; overflow: hidden; }

  /* PROFILE CARD (shown after onboarding) */
  #profile-card {
    display: none;
    margin: 4px 0;
    background: linear-gradient(135deg, rgba(124,92,252,0.1), rgba(0,212,168,0.06));
    border: 1px solid var(--border2);
    border-radius: 16px;
    padding: 14px 18px;
    font-size: 13px;
    animation: msgIn 0.5s cubic-bezier(0.34,1.56,0.64,1) both;
  }
  #profile-card .pc-title { font-family: var(--font-head); font-size: 11px; color: var(--accent2); letter-spacing: 1px; text-transform: uppercase; margin-bottom: 10px; }
  .pc-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .pc-item { background: rgba(0,0,0,0.25); border-radius: 8px; padding: 7px 10px; border: 1px solid var(--border); }
  .pc-label { font-size: 10px; color: var(--muted); font-family: var(--font-head); letter-spacing: 0.5px; text-transform: uppercase; }
  .pc-val { font-size: 12px; color: var(--text); margin-top: 2px; font-weight: 500; }

  /* Emoji pulse for fresh messages */
  .emoji-pop { display: inline-block; animation: emojiPop 0.5s cubic-bezier(0.34,1.56,0.64,1) both; }
  @keyframes emojiPop { from{transform:scale(0);}to{transform:scale(1);} }

  /* Stars decoration */
  .stars {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
  }
  .star {
    position: absolute;
    background: #fff;
    border-radius: 50%;
    animation: twinkle linear infinite;
    opacity: 0;
  }
  @keyframes twinkle {
    0%,100% { opacity: 0; transform: scale(0.5); }
    50% { opacity: 0.7; transform: scale(1); }
  }

  /* RESPONSIVE */
  @media(max-width:600px){
    #app { max-width: 100%; border: none; }
    #header-badges { display: none; }
    .bubble { max-width: 88%; }
  }

  /* Scrollbar */
  #chat { scroll-behavior: smooth; }

  /* Loading spinner */
  @keyframes spin { to { transform: rotate(360deg); } }
  .spinner { width: 16px; height: 16px; border: 2px solid rgba(124,92,252,0.2); border-top-color: var(--accent); border-radius: 50%; animation: spin 0.7s linear infinite; display: inline-block; }
</style>
</head>
<body>

<div class="particles" id="particles"></div>
<div class="stars" id="stars"></div>

<div id="app">

  <!-- HEADER -->
  <div id="header">
    <div id="avatar-wrap">
      <div id="avatar">🤖<div id="status-dot"></div></div>
    </div>
    <div id="header-info">
      <h1>Alex — AI Career Mentor</h1>
      <p id="header-sub">Personalizing your tech career path...</p>
    </div>
    <div id="header-badges">
      <span class="badge badge-ai">GPT-Powered</span>
      <span class="badge badge-live">● Live</span>
    </div>
  </div>

  <!-- PROGRESS -->
  <div id="progress-wrap">
    <div id="progress-label">PROFILE SETUP — STEP <span id="step-num">0</span> OF 5</div>
    <div id="progress-bar"><div id="progress-fill"></div></div>
  </div>

  <!-- CHAT -->
  <div id="chat">
    <div id="typing-wrap">
      <div class="mini-av">🤖</div>
      <div class="typing-bubble">
        <div class="dot"></div><div class="dot"></div><div class="dot"></div>
      </div>
    </div>
  </div>

  <!-- PROFILE CARD (injected after onboarding) -->
  <div id="profile-card">
    <div class="pc-title">📋 Your Profile</div>
    <div class="pc-grid" id="pc-grid"></div>
  </div>

  <!-- QUICK REPLIES -->
  <div id="quick-wrap"></div>

  <!-- INPUT -->
  <div id="input-row">
    <input id="user-input" placeholder="Type your message… or pick a quick reply above" />
    <button id="send-btn" title="Send">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
        <line x1="22" y1="2" x2="11" y2="13"></line>
        <polygon points="22 2 15 22 11 13 2 9 22 2"></polygon>
      </svg>
    </button>
  </div>

</div>

<script>
/* ───── CONFIG ─────────────────────────────────────────────── */
const API_KEY  = 'YOUR_ANTHROPIC_API_KEY_HERE';   // ← paste your key
const MODEL    = 'claude-sonnet-4-20250514';
const MAX_TOK  = 900;

/* ───── PARTICLES & STARS ──────────────────────────────────── */
(function spawnParticles(){
  const c = document.getElementById('particles');
  const colors = ['rgba(124,92,252,0.4)','rgba(0,212,168,0.35)','rgba(255,107,157,0.3)','rgba(160,130,255,0.25)'];
  for(let i=0;i<18;i++){
    const p=document.createElement('div');
    p.className='p';
    const size=(Math.random()*4+2)+'px';
    p.style.cssText=`width:${size};height:${size};left:${Math.random()*100}%;background:${colors[i%colors.length]};animation-duration:${Math.random()*12+8}s;animation-delay:${Math.random()*8}s;`;
    c.appendChild(p);
  }
  const s=document.getElementById('stars');
  for(let i=0;i<60;i++){
    const st=document.createElement('div');
    st.className='star';
    const sz=(Math.random()*2+1)+'px';
    st.style.cssText=`width:${sz};height:${sz};top:${Math.random()*100}%;left:${Math.random()*100}%;animation-duration:${Math.random()*4+2}s;animation-delay:${Math.random()*6}s;`;
    s.appendChild(st);
  }
})();

/* ───── STATE ──────────────────────────────────────────────── */
const profile = {};
const history = [];   // for Anthropic API multi-turn

const SYSTEM_PROMPT = `You are Alex, an enthusiastic, friendly, and expert AI Career Mentor for tech students and fresh graduates.

Your role:
- Guide users in choosing tech careers: Frontend, Backend, Full-Stack, Data Science/AI, Mobile, Cybersecurity
- Provide PERSONALIZED learning roadmaps, certification recommendations, project ideas, job roles, and salary ranges
- Help with coding: HTML, CSS, JavaScript, Python, SQL, React, Node.js and more
- Be motivating, concise, and practical

Formatting rules:
- Use **bold** for key terms
- Use \`code\` for tech names and code
- Keep responses under 200 words unless explaining code
- Add relevant emojis for friendliness (1-3 per message max)
- For code examples use fenced code blocks with language
- Always end with an encouraging line or next step suggestion

Current user profile: ${()=>JSON.stringify(profile)}`;

/* ───── ONBOARDING FLOW ────────────────────────────────────── */
const STEPS = [
  { key:null, msg:"👋 Hey! I'm **Alex**, your AI Career Mentor!\n\nI'll build a personalized career path just for you. Let's start — what's your **name**?", replies:[], next:'name' },
];
const ONBOARD = {
  name: v=>{
    profile.name = v.trim().split(' ')[0];
    return { msg:`Nice to meet you, **${profile.name}**! 🎉\n\nWhat's your **education level**?`, replies:['High School','Pursuing Degree','Bachelor\'s Graduate','Master\'s / PhD','Self-taught Coder'], next:'education', step:1 };
  },
  education: v=>{
    profile.education = v;
    return { msg:`Got it! 📚 What's your **main career goal** right now?`, replies:['Get my first tech job','Switch careers into tech','Level up my current skills','Build my own startup','Freelance & remote work'], next:'goal', step:2 };
  },
  goal: v=>{
    profile.goal = v;
    return { msg:`Love that energy! ⚡ What's your **current coding level**?`, replies:['Complete beginner (no code)','Know HTML & CSS basics','Built a few small projects','Comfortable with a language','Intermediate — want to specialize'], next:'skill', step:3 };
  },
  skill: v=>{
    profile.skill = v;
    return { msg:`Perfect. Which **tech area** excites you most? 🧩`, replies:['Frontend (UI/Design)','Backend (APIs/Servers)','Full-Stack (both)','Data Science / AI/ML','Mobile Apps','Cybersecurity'], next:'interest', step:4 };
  },
  interest: v=>{
    profile.interest = v;
    return { msg:`Almost done! How do you **learn best**? 🧠`, replies:['Building projects hands-on','Structured video courses','Reading docs & books','1-on-1 mentorship','Community & group learning'], next:'personality', step:5 };
  },
  personality: v=>{
    profile.personality = v;
    return { msg: buildSummary(), replies:['Show my learning roadmap 🗺️','Best certifications for me 🏆','Jobs & salaries 💼','Give me a project idea 💡','Help me write code 💻'], next:'__done__', step:5, done:true };
  }
};

function buildSummary(){
  const salaries = {
    'Frontend (UI/Design)':         '$65k–$130k/yr',
    'Backend (APIs/Servers)':       '$75k–$145k/yr',
    'Full-Stack (both)':            '$80k–$155k/yr',
    'Data Science / AI/ML':         '$90k–$165k/yr',
    'Mobile Apps':                  '$70k–$140k/yr',
    'Cybersecurity':                '$80k–$155k/yr',
  };
  const stacks = {
    'Frontend (UI/Design)':   'HTML → CSS → JS → React/Vue → Figma',
    'Backend (APIs/Servers)': 'Python/Node.js → SQL → REST APIs → Docker',
    'Full-Stack (both)':      'HTML/CSS/JS → React → Node.js → PostgreSQL → AWS',
    'Data Science / AI/ML':   'Python → Pandas → Scikit-learn → TensorFlow → MLOps',
    'Mobile Apps':            'React Native or Flutter → Firebase → App Store Deploy',
    'Cybersecurity':          'Linux → Networking → Python → Ethical Hacking → SIEM',
  };
  const s = salaries[profile.interest] || '$70k–$140k/yr';
  const st = stacks[profile.interest] || 'HTML → CSS → JS → React → Node.js';
  return `✅ **Profile complete, ${profile.name}!** Here's your snapshot:\n\n🎯 **Path:** ${st}\n💰 **Salary range:** ${s}\n📚 **Learning style:** ${profile.personality}\n\nWhat would you like to explore first?`;
}

/* ───── DOM HELPERS ────────────────────────────────────────── */
const chatEl   = document.getElementById('chat');
const typingEl = document.getElementById('typing-wrap');
const qrEl     = document.getElementById('quick-wrap');
const inputEl  = document.getElementById('user-input');
const fillEl   = document.getElementById('progress-fill');
const stepNumEl= document.getElementById('step-num');
const pcCard   = document.getElementById('profile-card');
const pcGrid   = document.getElementById('pc-grid');
const headerSub= document.getElementById('header-sub');

function setProgress(n){
  fillEl.style.width = (n/5*100)+'%';
  stepNumEl.textContent = n;
}

function setReplies(arr){
  qrEl.innerHTML='';
  arr.forEach(r=>{
    const b=document.createElement('button');
    b.className='qr';
    b.textContent=r;
    b.onclick=()=>handleSend(r);
    qrEl.appendChild(b);
  });
}

function showTyping(){ typingEl.style.display='flex'; scroll(); }
function hideTyping(){ typingEl.style.display='none'; }

function scroll(){ chatEl.scrollTop=chatEl.scrollHeight; }

function parseMarkdown(text){
  return text
    .replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>')
    .replace(/`([^`]+)`/g,'<code>$1</code>')
    .replace(/```(\w*)\n([\s\S]*?)```/g,(_,lang,code)=>`<pre><code>${escHtml(code.trim())}</code></pre>`)
    .replace(/\n/g,'<br>');
}

function escHtml(t){ return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

function addMsg(text, role){
  const wrap = document.createElement('div');
  wrap.className = `msg-wrap ${role}`;

  const av = document.createElement('div');
  av.className = 'mini-av';
  av.textContent = role==='bot' ? '🤖' : '🙂';

  const bub = document.createElement('div');
  bub.className = 'bubble';
  bub.innerHTML = parseMarkdown(text);

  if(role==='bot'){
    wrap.appendChild(av);
    wrap.appendChild(bub);
  } else {
    wrap.appendChild(av);
    wrap.appendChild(bub);
  }

  chatEl.insertBefore(wrap, typingEl);
  scroll();
  return bub;
}

function showProfileCard(){
  const fields = [
    {label:'Name',    val: profile.name},
    {label:'Education',val: profile.education},
    {label:'Goal',    val: profile.goal},
    {label:'Skill',   val: profile.skill},
    {label:'Interest',val: profile.interest},
    {label:'Learning',val: profile.personality},
  ];
  pcGrid.innerHTML = fields.map(f=>`
    <div class="pc-item">
      <div class="pc-label">${f.label}</div>
      <div class="pc-val">${f.val||'—'}</div>
    </div>`).join('');
  pcCard.style.display='block';
  headerSub.textContent=`Mentoring ${profile.name} · ${profile.interest}`;
}

/* ───── ONBOARDING STATE MACHINE ───────────────────────────── */
let currentStep = 'name';
let onboardingDone = false;

function handleOnboarding(userText){
  const handler = ONBOARD[currentStep];
  if(!handler) return false;
  const res = handler(userText);
  if(res.step !== undefined) setProgress(res.step);

  setTimeout(()=>{
    hideTyping();
    addMsg(res.msg,'bot');
    setReplies(res.replies||[]);
    if(res.done){
      onboardingDone = true;
      showProfileCard();
      // prime history for AI
      history.push({ role:'user',    content:`My profile: Name=${profile.name}, Education=${profile.education}, Goal=${profile.goal}, Skill level=${profile.skill}, Interest=${profile.interest}, Learning style=${profile.personality}` });
      history.push({ role:'assistant', content:`Welcome ${profile.name}! ${buildSummary()}` });
    }
    currentStep = res.next;
  }, 900 + Math.random()*300);
  return true;
}

/* ───── ANTHROPIC API CALL ─────────────────────────────────── */
async function callAI(userMsg){
  history.push({ role:'user', content: userMsg });

  const systemFull = `You are Alex, a friendly, expert AI Career Mentor.
User profile: Name=${profile.name||'unknown'}, Education=${profile.education||'unknown'}, Goal=${profile.goal||'unknown'}, Skill=${profile.skill||'unknown'}, Interest=${profile.interest||'unknown'}, Learning style=${profile.personality||'unknown'}.

Provide personalized, concise answers (max 180 words unless code is needed).
Use **bold** for emphasis, \`code\` for tech terms, fenced blocks for code examples.
Be encouraging and always suggest a clear next step.`;

  try {
    const resp = await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{
        'Content-Type':'application/json',
        'x-api-key': API_KEY,
        'anthropic-version':'2023-06-01',
        'anthropic-dangerous-direct-browser-access':'true'
      },
      body: JSON.stringify({
        model: MODEL,
        max_tokens: MAX_TOK,
        system: systemFull,
        messages: history.slice(-12)   // keep last 12 turns for context
      })
    });

    if(!resp.ok){
      const err = await resp.json().catch(()=>({}));
      throw new Error(err.error?.message || `HTTP ${resp.status}`);
    }

    const data = await resp.json();
    const reply = data.content?.[0]?.text || '*(No response)*';
    history.push({ role:'assistant', content: reply });
    return reply;

  } catch(e){
    console.error(e);
    return `⚠️ **API Error:** ${e.message}\n\nMake sure your **API key** is set in the \`API_KEY\` variable at the top of the script, and that you have access to the Anthropic API.`;
  }
}

/* ───── MAIN SEND HANDLER ──────────────────────────────────── */
async function handleSend(text){
  text = (text || inputEl.value).trim();
  if(!text) return;
  inputEl.value='';
  setReplies([]);
  addMsg(text,'user');
  showTyping();

  if(!onboardingDone){
    handleOnboarding(text);
    return;
  }

  // Post-onboarding: call Anthropic API
  const reply = await callAI(text);
  hideTyping();
  addMsg(reply,'bot');
  setReplies(['Learning roadmap 🗺️','Certifications 🏆','Jobs & salaries 💼','Project idea 💡','Code help 💻','Motivation boost 🔥']);
}

/* ───── INPUT WIRING ───────────────────────────────────────── */
document.getElementById('send-btn').onclick = ()=> handleSend();
inputEl.addEventListener('keydown', e=>{
  if(e.key==='Enter' && !e.shiftKey){ e.preventDefault(); handleSend(); }
});

/* ───── KICK OFF ───────────────────────────────────────────── */
(function init(){
  showTyping();
  setTimeout(()=>{
    hideTyping();
    addMsg("👋 Hey! I'm **Alex**, your AI Career Mentor!\n\nI'm here to build a **personalized tech career path** just for you. Ready? Let's go 🚀\n\nFirst — what's your **name**?",'bot');
    setProgress(0);
  }, 1200);
})();
</script>
</body>
</html>
