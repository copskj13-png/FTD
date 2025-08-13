# FTD
spill
<!DOCTYPE html>
<html lang="no">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
  <title>Spillhub – Higher/Lower</title>
  <style>
    /* --------- Theme --------- */
    :root {
      --bg: #0a0f1a;
      --bg2: #0d1220;
      --panel: #0f1726;
      --panel2: #121b2d;
      --border: #1f2b45;
      --text: #e9f1ff;
      --muted: #9fb1c8;
      --success: #54e1a6;
      --warn: #ffd166;
      --danger: #ff6b6b;
      --accent1: #6ea8fe;
      --accent2: #8a7dff;
      --accent3: #4dd4c6;
      --glass: rgba(255,255,255,.06);
      --shadow: 0 8px 16px rgba(0,0,0,.3);
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial;
      color: var(--text);
      background: radial-gradient(circle at 20% 10%, #1e3a8a33, transparent 40%),
                  radial-gradient(circle at 80% 80%, #9333ea33, transparent 40%),
                  linear-gradient(135deg, #0a0f1a, #1e293b);
      min-height: 100dvh;
      overflow-x: hidden;
      position: relative;
    }
    body::before {
      content: '';
      position: absolute;
      inset: 0;
      background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='5' cy='5' r='1' fill='%236ea8fe33'/%3E%3Ccircle cx='95' cy='95' r='1' fill='%238a7dff33'/%3E%3Ccircle cx='50' cy='20' r='1' fill='%234dd4c633'/%3E%3C/svg%3E") repeat;
      opacity: 0.3;
      pointer-events: none;
    }

    /* --------- Topbar / Navbar --------- */
    .topbar {
      position: sticky;
      top: 0;
      z-index: 50;
      backdrop-filter: blur(10px);
      background: linear-gradient(180deg, rgba(7,11,20,.85), rgba(7,11,20,.6));
      border-bottom: 1px solid var(--border);
    }
    .topinner {
      max-width: 1200px;
      margin: 0 auto;
      padding: 8px 12px;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 8px;
    }
    .brand {
      display: flex;
      align-items: center;
      gap: 8px;
      font-weight: 900;
      font-size: 16px;
      letter-spacing: 0.3px;
    }
    .brand .logo {
      width: 32px;
      height: 32px;
      border-radius: 8px;
      border: 1px solid var(--border);
      background: radial-gradient(70% 70% at 30% 20%, #6ea8fe66, transparent 60%), linear-gradient(180deg, #0f1728, #0a1221);
      display: grid;
      place-items: center;
      box-shadow: var(--shadow);
      animation: pulse 2s infinite ease-in-out;
    }
    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }
    .brand .logo span { font-size: 16px; }
    .grow { flex: 1; }
    .modepicker { display: flex; gap: 6px; align-items: center; }
    .modebtn {
      display: flex;
      align-items: center;
      gap: 6px;
      padding: 12px 16px;
      border-radius: 999px;
      border: 1px solid #2c3a5c;
      background: linear-gradient(180deg, #1a2236, #121a2e);
      color: var(--text);
      font-weight: 800;
      font-size: 15px;
      cursor: pointer;
      touch-action: manipulation;
      transition: transform 0.1s ease, box-shadow 0.2s ease, background 0.2s ease;
    }
    .modebtn .ico { width: 18px; height: 18px; display: grid; place-items: center; }
    .modebtn.active {
      background: linear-gradient(180deg, var(--accent1), var(--accent2));
      color: #081020;
      border-color: transparent;
      box-shadow: 0 8px 16px rgba(0,0,0,.4);
    }
    .modebtn.active .ico { filter: contrast(0) brightness(0); }
    .modebtn:hover { transform: scale(1.05); box-shadow: 0 10px 20px rgba(0,0,0,.4); }
    .modebtn:active { transform: scale(0.98); box-shadow: 0 6px 12px rgba(0,0,0,.3); }
    .playbtn {
      padding: 12px 18px;
      border-radius: 12px;
      border: 1px solid transparent;
      background: linear-gradient(180deg, var(--accent3), #2cd0b9);
      color: #081020;
      font-weight: 900;
      font-size: 15px;
      cursor: pointer;
      touch-action: manipulation;
      box-shadow: 0 8px 16px rgba(0,0,0,.4);
      transition: transform 0.1s ease, box-shadow 0.2s ease;
    }
    .playbtn:hover { transform: scale(1.05); box-shadow: 0 10px 20px rgba(0,0,0,.4); }
    .playbtn:active { transform: scale(0.98); box-shadow: 0 6px 12px rgba(0,0,0,.3); }

    /* --------- Containers --------- */
    main { max-width: 1200px; margin: 0 auto; padding: 12px; }
    .panel {
      background: linear-gradient(180deg, var(--panel), var(--panel2));
      border: 1px solid var(--border);
      border-radius: 16px;
      box-shadow: var(--shadow);
      overflow: hidden;
      transition: transform 0.2s ease;
    }
    .panel:hover { transform: translateY(-5px); box-shadow: 0 12px 24px rgba(0,0,0,.4); }
    .grid { display: grid; gap: 12px; }

    /* --------- Home --------- */
    .hero {
      display: grid;
      grid-template-columns: 1fr;
      gap: 12px;
    }
    @media (min-width: 768px) { .hero { grid-template-columns: 1.3fr .7fr; } }
    .hero .big { padding: 16px; }
    .hero h1 {
      margin: 0;
      font-size: 28px;
      background: linear-gradient(90deg, var(--accent1), var(--accent2), var(--accent3));
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 0 10px rgba(110, 168, 254, 0.3);
    }
    .hero p { color: var(--muted); margin: 8px 0; font-size: 14px; }
    .cards { display: grid; grid-template-columns: 1fr; gap: 12px; }
    @media (min-width: 600px) { .cards { grid-template-columns: repeat(2, 1fr); } }
    .gamecard {
      position: relative;
      padding: 14px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: linear-gradient(180deg, #0f1628, #0b1321);
      touch-action: manipulation;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }
    .gamecard:hover { transform: scale(1.02); box-shadow: 0 10px 20px rgba(0,0,0,.4); }
    .gamecard h3 { margin: 0 0 6px; font-size: 18px; }
    .gamecard p { margin: 0; color: var(--muted); font-size: 13px; }
    .tag {
      padding: 4px 8px;
      border: 1px solid var(--border);
      border-radius: 999px;
      font-size: 12px;
      background: var(--glass);
    }
    .homefooter { display: flex; gap: 8px; flex-wrap: wrap; align-items: center; }

    /* --------- Home Popup --------- */
    .homePopup {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: linear-gradient(180deg, var(--panel), var(--panel2));
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 20px;
      box-shadow: var(--shadow);
      z-index: 100;
      text-align: center;
      animation: popIn 0.3s ease;
    }
    @keyframes popIn {
      0% { transform: translate(-50%, -50%) scale(0.8); opacity: 0; }
      100% { transform: translate(-50%, -50%) scale(1); opacity: 1; }
    }
    .homePopup p { color: var(--muted); margin: 0 0 15px; font-size: 14px; }
    .homePopup button {
      padding: 10px 20px;
      background: linear-gradient(180deg, var(--accent3), #2cd0b9);
      border: none;
      border-radius: 12px;
      color: #081020;
      font-weight: 900;
      cursor: pointer;
      transition: transform 0.1s ease;
    }
    .homePopup button:hover { transform: scale(1.05); }
    .homePopup button:active { transform: scale(0.98); }

    /* --------- Game View --------- */
    .layout { display: grid; grid-template-columns: 1fr; gap: 12px; }
    @media (min-width: 768px) { .layout { grid-template-columns: 1.2fr .8fr; } }
    .controls { padding: 12px; display: grid; gap: 10px; }
    .row { display: flex; gap: 8px; align-items: center; flex-wrap: wrap; }
    .pill {
      padding: 6px 10px;
      border: 1px solid var(--border);
      border-radius: 999px;
      font-size: 12px;
      color: var(--muted);
      background: var(--glass);
    }

    button {
      position: relative;
      padding: 12px 16px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: linear-gradient(180deg, #1a2236, #121a2e);
      color: var(--text);
      font-weight: 700;
      font-size: 14px;
      cursor: pointer;
      touch-action: manipulation;
      transition: transform 0.1s ease, box-shadow 0.2s ease;
    }
    button:hover { transform: scale(1.05); box-shadow: 0 10px 20px rgba(0,0,0,.4); }
    button:active { transform: scale(0.98); box-shadow: 0 6px 12px rgba(0,0,0,.3); }
    button.primary {
      background: linear-gradient(180deg, var(--accent1), var(--accent2));
      border-color: transparent;
      color: #081020;
      box-shadow: 0 8px 16px rgba(0,0,0,.4);
      font-size: 15px;
    }
    button:disabled { opacity: 0.65; cursor: not-allowed; filter: saturate(0.5); }

    .cardwrap { perspective: 1000px; }
    .card {
      position: relative;
      height: 200px;
      border-radius: 16px;
      border: 1px solid var(--border);
      box-shadow: var(--shadow);
      background: radial-gradient(80% 60% at 50% -20%, #3a5bff22, transparent 70%), linear-gradient(180deg, #0d1527, #0a1120);
      overflow: hidden;
      transition: transform 0.2s ease;
    }
    @media (min-width: 600px) { .card { height: 250px; } }
    .card:hover { transform: rotateY(5deg); }
    .flip {
      width: 100%;
      height: 100%;
      position: relative;
      transform-style: preserve-3d;
      transition: transform 0.6s cubic-bezier(0.2, 0.8, 0.2, 1);
    }
    .card.revealed .flip { transform: rotateY(180deg); }
    .face {
      position: absolute;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 48px;
      backface-visibility: hidden;
    }
    @media (min-width: 600px) { .face { font-size: 64px; } }
    .front { color: #a9b7ff; }
    .back { transform: rotateY(180deg); gap: 8px; }
    .back .suit { font-size: 0.7em; opacity: 0.9; }

    .status {
      padding: 12px 14px;
      border-top: 1px solid var(--border);
      color: var(--muted);
      font-size: 13px;
    }
    .status .ok { color: var(--success); }
    .status .warn { color: var(--warn); }
    .status .bad { color: var(--danger); }

    .list { max-height: 300px; overflow: auto; }
    .list h2 { margin: 8px; font-size: 16px; color: #c7d1db; }
    .list ul { list-style: none; padding: 0; margin: 0; }
    .list li { padding: 8px 10px; border-bottom: 1px solid var(--border); display: flex; justify-content: space-between; color: #c7d1db; font-size: 13px; }

    .players { padding: 12px; }
    .players h2 { margin: 8px; font-size: 16px; color: #c7d1db; }
    .players ul { list-style: none; margin: 0; padding: 0; }
    .players li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 12px;
      border: 1px solid var(--border);
      border-radius: 12px;
      margin-bottom: 8px;
      background: linear-gradient(180deg, #0c1426, #0b1322);
      font-size: 13px;
      transition: transform 0.2s ease;
    }
    .players li:hover { transform: scale(1.02); }
    .players .me { outline: 2px solid var(--accent3); box-shadow: 0 0 0 3px #0a0f1a inset; }
    .name { font-weight: 800; }
    .score { font-variant-numeric: tabular-nums; }

    .panel.choices { padding: 12px; }
    .choicesgrid {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 8px;
    }
    @media (min-width: 600px) { .choicesgrid { grid-template-columns: repeat(7, 1fr); } }
    @media (min-width: 900px) { .choicesgrid { grid-template-columns: repeat(13, 1fr); } }
    .choice {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      aspect-ratio: 3/4;
      min-width: 48px;
      border-radius: 12px;
      border: 1px solid var(--border);
      background: linear-gradient(180deg, #0f1728, #0b1321);
      box-shadow: var(--shadow);
      touch-action: manipulation;
      transition: transform 0.1s ease, box-shadow 0.2s ease;
    }
    .choice:hover { transform: scale(1.1); box-shadow: 0 12px 24px rgba(0,0,0,.4); }
    .choice .big { font-size: 18px; font-weight: 900; }
    .choice .small { font-size: 10px; color: #9bb0c0; }
    .choice:active { transform: scale(0.98); box-shadow: 0 6px 12px rgba(0,0,0,.3); }

    .vA, .vK { background: linear-gradient(180deg, #152041, #0d1325); }
    .vQ, .vJ { background: linear-gradient(180deg, #1a2a52, #0f1831); }
    .v10, .v9, .v8 { background: linear-gradient(180deg, #0f2a2a, #0b161d); }
    .v7, .v6, .v5 { background: linear-gradient(180deg, #2a1f3d, #121025); }
    .v4, .v3, .v2 { background: linear-gradient(180deg, #1d2a14, #0d1710); }

    .jokergrid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-top: 8px; }
    .joker {
      aspect-ratio: 3/4;
      border-radius: 12px;
      border: 1px dashed #36476b;
      background: linear-gradient(180deg, #1a0f22, #120b19);
      display: grid;
      place-items: center;
      box-shadow: var(--shadow);
      touch-action: manipulation;
      transition: transform 0.1s ease;
    }
    .joker:hover { transform: scale(1.1); box-shadow: 0 12px 24px rgba(0,0,0,.4); }
    .joker .big { font-size: 18px; font-weight: 900; }
    .joker .small { font-size: 10px; color: #caa9ff; }
    .joker:active { transform: scale(0.98); box-shadow: 0 6px 12px rgba(0,0,0,.3); }

    .hidden { display: none; }
  </style>
</head>
<body>
  <!-- NAVBAR -->
  <div class="topbar">
    <div class="topinner">
      <div class="brand">
        <div class="logo"><span>🂡</span></div>
        <div>Spillhub</div>
      </div>
      <div class="grow"></div>
      <div class="modepicker" aria-label="Velg spillmodus">
        <button id="modeHL" class="modebtn active" title="HL – klassisk">
          <span class="ico">🂱</span><span>HL</span>
        </button>
        <button id="modeHLK" class="modebtn" title="HLK – kaos (med jokere)">
          <span class="ico">💥</span><span>HLK</span>
        </button>
      </div>
      <button id="goHome" class="modebtn" title="Hjem">🏠 Hjem</button>
      <button id="playNow" class="playbtn" title="Start">Spill nå</button>
    </div>
  </div>

  <!-- HOME POPUP -->
  <div id="homePopup" class="homePopup">
    <p>Velkommen til Spillhub! Velg modus og spill nå!</p>
    <button id="closePopup">Lukk</button>
  </div>

  <main>
    <!-- HOME VIEW -->
    <section id="homeView" class="grid">
      <div class="hero">
        <div class="panel big">
          <h1>Velg spilltype</h1>
          <p>Velkommen til Higher/Lower!</p>
          <div class="homefooter">
            <span class="tag">Aktiv modus: <strong id="activeModeText">HL</strong></span>
            <button id="startFromHome" class="playbtn">Spill nå</button>
          </div>
        </div>
        <div class="panel big">
          <div class="cards">
            <div class="gamecard" id="cardHL">
              <div class="tag">HL</div>
              <h3>Higher/Lower</h3>
              <p>Klassisk – 52 kort.</p>
            </div>
            <div class="gamecard" id="cardHLK">
              <div class="tag">HLK</div>
              <h3>Higher/Lower Kaos</h3>
              <p>Med tre jokere!</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- GAME VIEW -->
    <section id="gameView" class="hidden">
      <div class="layout">
        <section>
          <div class="cardwrap panel">
            <div class="card" id="card">
              <div class="flip">
                <div class="face front" id="cardFront">❓</div>
                <div class="face back" id="cardBack"><span id="cardBackVal">A</span><span class="suit" id="cardBackSuit">♠</span></div>
              </div>
            </div>
          </div>
          <div class="panel controls" aria-live="polite">
            <div class="row">
              <span class="pill" id="turnInfo">Tur: –</span>
              <span class="pill" id="attempts">Forsøk: 0/2</span>
              <span class="pill" id="deckLeft">Kort igjen: 52</span>
            </div>
            <div class="row">
              <button id="nextBtn" class="primary" disabled>Neste tur</button>
              <button id="reshuffleBtn">Bland stokken</button>
            </div>
            <div class="status" id="status">Legg til spillere for å starte. Velg et kort (A..K) nedenfor for å gjette.</div>
          </div>
          <div class="panel choices">
            <h2 style="margin:0 0 8px 4px;color:#c7d1db">Velg kort for gjetning</h2>
            <div id="choices" class="choicesgrid" role="group" aria-label="Kortvalg"></div>
            <div id="jokerRow" class="jokergrid hidden" aria-label="Jokervalg"></div>
          </div>
          <div class="panel list">
            <h2>Historikk</h2>
            <ul id="history"></ul>
          </div>
        </section>
        <aside>
          <div class="panel players">
            <h2>Spillere</h2>
            <div class="row">
              <input id="playerName" type="text" placeholder="Spillernavn" style="flex:1; padding:10px 12px; border-radius:12px; border:1px solid var(--border); background:#0b1220; color:var(--text); font-size:14px;" />
              <button id="addPlayer" class="primary">Legg til</button>
              <button id="startBtn" class="primary">Start spill</button>
            </div>
            <ul id="playerList"></ul>
            <div class="row" style="margin-top:8px">
              <span class="pill" id="scoreHint">Poengsum oppdateres per tur</span>
            </div>
          </div>
        </aside>
      </div>
    </section>
  </main>

  <script>
    // ----- Elements -----
    const modeHLBtn = document.getElementById('modeHL');
    const modeHLKBtn = document.getElementById('modeHLK');
    const goHomeBtn = document.getElementById('goHome');
    const playNowBtn = document.getElementById('playNow');
    const startFromHomeBtn = document.getElementById('startFromHome');
    const activeModeText = document.getElementById('activeModeText');
    const homePopup = document.getElementById('homePopup');
    const closePopupBtn = document.getElementById('closePopup');

    const homeView = document.getElementById('homeView');
    const gameView = document.getElementById('gameView');
    const cardHL = document.getElementById('cardHL');
    const cardHLK = document.getElementById('cardHLK');

    const nextBtn = document.getElementById('nextBtn');
    const reshuffleBtn = document.getElementById('reshuffleBtn');
    const statusEl = document.getElementById('status');
    const historyEl = document.getElementById('history');
    const deckLeftEl = document.getElementById('deckLeft');
    const attemptsEl = document.getElementById('attempts');
    const turnInfoEl = document.getElementById('turnInfo');
    const choicesEl = document.getElementById('choices');
    const jokerRow = document.getElementById('jokerRow');

    const card = document.getElementById('card');
    const cardBackVal = document.getElementById('cardBackVal');
    const cardBackSuit = document.getElementById('cardBackSuit');

    const playerNameInput = document.getElementById('playerName');
    const addPlayerBtn = document.getElementById('addPlayer');
    const startBtn = document.getElementById('startBtn');
    const playerList = document.getElementById('playerList');

    // ----- Game State -----
    const SUITS = ['♠', '♥', '♦', '♣'];
    const NAME = v => ({1: 'A', 11: 'J', 12: 'Q', 13: 'K'}[v] || v);

    let deck = [];
    let hidden = null;
    let lastGuess = null;
    let roundAttempts = 0;
    let roundResolved = false;
    let inputLocked = false;

    let players = [];
    let current = 0;
    let gameMode = 'HL';

    // ----- View helpers -----
    function showHome() { homeView.classList.remove('hidden'); gameView.classList.add('hidden'); homePopup.style.display = 'none'; }
    function showGame() { homeView.classList.add('hidden'); gameView.classList.remove('hidden'); homePopup.style.display = 'none'; }
    function showPopup() { homePopup.style.display = 'block'; }

    function setMode(mode) {
      gameMode = mode;
      modeHLBtn.classList.toggle('active', mode === 'HL');
      modeHLKBtn.classList.toggle('active', mode === 'HLK');
      activeModeText.textContent = mode;
      buildChoices();
      if (mode === 'HLK') { jokerRow.classList.remove('hidden'); } else { jokerRow.classList.add('hidden'); }
      createDeck(); shuffle();
      if (!homeView.classList.contains('hidden')) return;
      newRound(true);
      setStatus(`Byttet til ${mode}.`);
    }

    // ----- Deck helpers -----
    function createDeck() {
      deck = [];
      for (let v = 1; v <= 13; v++) { for (const s of SUITS) { deck.push({ v, s }); } }
      if (gameMode === 'HLK') {
        deck.push({ joker: 1, label: 'Joker 1' });
        deck.push({ joker: 2, label: 'Joker 2' });
        deck.push({ joker: 3, label: 'Joker 3' });
      }
    }
    function shuffle() { for (let i = deck.length - 1; i > 0; i--) { const j = Math.floor(Math.random() * (i + 1)); [deck[i], deck[j]] = [deck[j], deck[i]]; } }
    function drawCard() { if (deck.length === 0) { createDeck(); shuffle(); } hidden = deck.pop(); card.classList.remove('revealed'); updateCardBack('❓', ''); updateMeta(); }

    // ----- UI helpers -----
    function setStatus(msg) { statusEl.innerHTML = msg; }
    function addHistory(text, badge) { const li = document.createElement('li'); li.innerHTML = `<span>${text}</span>` + (badge ? `<span class="pill">${badge}</span>` : ''); historyEl.prepend(li); }
    function updateCardBack(val, suit) { cardBackVal.textContent = val === '❓' ? '❓' : val; cardBackSuit.textContent = suit || ''; }
    function reveal() {
      if (isJoker(hidden)) {
        updateCardBack('🃏', '');
      } else {
        updateCardBack(NAME(hidden.v), hidden.s);
      }
      card.classList.add('revealed');
    }
    function updateMeta() { deckLeftEl.textContent = `Kort igjen: ${deck.length}`; attemptsEl.textContent = `Forsøk: ${roundAttempts}/2`; turnInfoEl.textContent = players.length ? `Tur: ${players[current].name}` : 'Tur: –'; renderPlayers(); }

    // ----- Players -----
    function renderPlayers() {
      playerList.innerHTML = '';
      players.forEach((p, idx) => {
        const li = document.createElement('li');
        li.className = idx === current ? 'me' : '';
        li.innerHTML = `<span class="name">${p.name}</span><span class="score">${p.score}</span>`;
        playerList.appendChild(li);
      });
    }

    addPlayerBtn.addEventListener('click', () => {
      const n = (playerNameInput.value || '').trim();
      if (!n) return;
      players.push({ name: n, score: 0 });
      playerNameInput.value = '';
      renderPlayers();
      setStatus('Spiller lagt til. Trykk Start spill når alle er klare.');
    });

    startBtn.addEventListener('click', () => {
      if (players.length === 0) { players = [{ name: 'Spiller 1', score: 0 }]; }
      current = 0; createDeck(); shuffle(); showGame(); newRound(true);
      setStatus('Spillet er i gang! Velg et kort for å gjette.');
    });

    function nextPlayer() { current = (current + 1) % players.length; }

    function newRound(initial = false) {
      roundAttempts = 0; lastGuess = null; roundResolved = false; inputLocked = false; drawCard();
      nextBtn.disabled = true; if (!initial) nextPlayer(); updateMeta();
    }

    // ----- Helpers -----
    function isJoker(card) { return card && typeof card.joker === 'number'; }

    // ----- Guess (A..K + ev. Jokere) -----
    function handleGuess(guess) {
      if (roundResolved || inputLocked) return;

      const player = players[current];
      roundAttempts++;
      updateMeta();

      let isMatch = false;
      if (typeof guess === 'number' && !isJoker(hidden)) isMatch = (guess === hidden.v);
      if (guess && guess.type === 'joker' && isJoker(hidden)) isMatch = (guess.id === hidden.joker);

      // If the hidden card is a joker, always reveal it and give 0 points
      if (isJoker(hidden)) {
        reveal();
        setStatus(`<strong>${player.name}</strong> gjettet ${typeof guess === 'number' ? NAME(guess) : 'Joker ' + guess.id}. Kortet var <strong>🃏 Joker ${hidden.joker}</strong>. <span class="warn">Ingen poeng for jokere.</span>`);
        addHistory(`${player.name} traff joker`, '0');
        if (isMatch) confetti();
        finishRound();
        return;
      }

      // If guess is a number but hidden is a joker, reveal immediately
      if (typeof guess === 'number' && isJoker(hidden)) {
        reveal();
        setStatus(`<strong>${player.name}</strong> gjettet ${NAME(guess)}. Kortet var <strong>🃏 Joker ${hidden.joker}</strong>. <span class="warn">Ingen poeng for jokere.</span>`);
        addHistory(`${player.name} bomma (joker)`, '0');
        finishRound();
        return;
      }

      // Normal card guess logic
      if (isMatch) {
        reveal();
        const gained = (roundAttempts === 1) ? 10 : 3;
        player.score += gained;
        const diffMsg = (roundAttempts === 1) ? '<span class="ok">Differanse: 0</span>' : `<span class="ok">Differanse: ${Math.abs(lastGuess - hidden.v)}</span>`;
        addHistory(`${player.name} traf riktig`, `+${gained}`);
        setStatus(`<strong>${player.name}</strong> traff! Kortet var <strong>${NAME(hidden.v)}${hidden.s}</strong>. ${diffMsg} <span class="ok">+${gained} poeng.</span>`);
        confetti();
        finishRound();
      } else {
        if (roundAttempts === 2) {
          let penalty = Math.abs(guess - hidden.v);
          player.score -= penalty;
          reveal();
          setStatus(`<strong>${player.name}</strong> bomma på 2. forsøk. Kortet var <strong>${NAME(hidden.v)}${hidden.s}</strong>. <span class="bad">Differanse: ${penalty}. −${penalty} poeng.</span>`);
          addHistory(`${player.name} bomma 2×`, `−${penalty}`);
          finishRound();
        } else {
          let hint = (guess < hidden.v) ? '<span class="warn">Høyere!</span>' : '<span class="warn">Lavere!</span>';
          setStatus(`${hint} Du har ett forsøk igjen.`);
          addHistory(`${player.name} gjettet feil`);
        }
      }

      lastGuess = (typeof guess === 'number') ? guess : lastGuess;
    }

    function finishRound() { roundResolved = true; inputLocked = true; nextBtn.disabled = false; updateMeta(); }

    // ----- Build choice buttons -----
    function buildChoices() {
      const values = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13];
      choicesEl.innerHTML = '';
      values.forEach(v => {
        const btn = document.createElement('button');
        btn.className = `choice v${v === 1 ? 'A' : v}`;
        btn.setAttribute('aria-label', `Velg ${NAME(v)} (${v})`);
        btn.innerHTML = `<div class="big">${NAME(v)}</div><div class="small">${v === 1 ? 'A' : v === 11 ? 'J' : v === 12 ? 'Q' : v === 13 ? 'K' : v}</div>`;
        btn.addEventListener('click', () => handleGuess(v));
        choicesEl.appendChild(btn);
      });

      jokerRow.innerHTML = '';
      if (gameMode === 'HLK') {
        [1, 2, 3].forEach(id => {
          const jb = document.createElement('button');
          jb.className = 'joker';
          jb.setAttribute('aria-label', `Velg Joker ${id}`);
          jb.innerHTML = `<div class="big">🃏</div><div class="small">Joker ${id}</div>`;
          jb.addEventListener('click', () => handleGuess({ type: 'joker', id }));
          jokerRow.appendChild(jb);
        });
      }
    }

    // ----- Confetti (optimized for mobile) -----
    function confetti() {
      const burst = document.createElement('div');
      burst.style.position = 'fixed';
      burst.style.inset = '0';
      burst.style.pointerEvents = 'none';
      const n = 40;
      const centerX = window.innerWidth / 2;
      const centerY = window.innerHeight / 4;
      for (let i = 0; i < n; i++) {
        const p = document.createElement('div');
        p.style.position = 'absolute';
        p.style.width = '5px';
        p.style.height = '5px';
        p.style.background = i % 3 === 0 ? 'var(--accent1)' : i % 3 === 1 ? 'var(--accent2)' : 'var(--accent3)';
        p.style.left = centerX + 'px';
        p.style.top = centerY + 'px';
        p.style.borderRadius = '2px';
        const ang = Math.random() * Math.PI * 2;
        const dist = 60 + Math.random() * 100;
        const dx = Math.cos(ang) * dist;
        const dy = Math.sin(ang) * dist;
        p.animate([
          { transform: `translate(0,0)`, opacity: 1 },
          { transform: `translate(${dx}px, ${dy}px) rotate(${Math.random() * 360}deg)`, opacity: 0 }
        ], { duration: 800 + Math.random() * 400, easing: 'cubic-bezier(.2,.8,.2,1)', fill: 'forwards' });
        burst.appendChild(p);
      }
      document.body.appendChild(burst);
      setTimeout(() => burst.remove(), 1200);
    }

    // ----- Global controls -----
    nextBtn.addEventListener('click', () => newRound());
    reshuffleBtn.addEventListener('click', () => { createDeck(); shuffle(); newRound(true); setStatus('Ny stokking. Kort trukket.'); });

    // Navbar actions
    modeHLBtn.addEventListener('click', () => setMode('HL'));
    modeHLKBtn.addEventListener('click', () => setMode('HLK'));
    goHomeBtn.addEventListener('click', () => { showHome(); showPopup(); });
    playNowBtn.addEventListener('click', () => { showGame(); if (deck.length === 0) { createDeck(); shuffle(); } newRound(true); });
    startFromHomeBtn.addEventListener('click', () => playNowBtn.click());
    closePopupBtn.addEventListener('click', () => { homePopup.style.display = 'none'; });

    // Clickable cards on home to switch mode
    cardHL.addEventListener('click', () => setMode('HL'));
    cardHLK.addEventListener('click', () => setMode('HLK'));

    // ----- Init -----
    showHome();
    setMode('HL');
    buildChoices();
    (function initMeta() { const deckLeft = document.getElementById('deckLeft'); if (deckLeft) deckLeft.textContent = 'Kort igjen: –'; })();
  </script>
</body>
</html>
