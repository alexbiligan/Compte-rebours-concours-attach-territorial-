<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <title>Concours Attaché Territorial</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700;900&display=swap');

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      color: white;
      overflow: hidden;
    }

    /* Animated background particles */
    .bg-particles {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      pointer-events: none;
      z-index: 0;
    }

    .particle {
      position: absolute;
      border-radius: 50%;
      background: rgba(255,255,255,0.05);
      animation: float linear infinite;
    }

    @keyframes float {
      0% { transform: translateY(100vh) scale(0); opacity: 0; }
      10% { opacity: 1; }
      90% { opacity: 1; }
      100% { transform: translateY(-10vh) scale(1); opacity: 0; }
    }

    .container {
      position: relative;
      z-index: 1;
      text-align: center;
      padding: 2rem 1.5rem;
      max-width: 420px;
      width: 100%;
    }

    .badge {
      display: inline-block;
      background: rgba(255, 200, 80, 0.15);
      border: 1px solid rgba(255, 200, 80, 0.4);
      color: #ffc850;
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      padding: 0.4rem 1rem;
      border-radius: 2rem;
      margin-bottom: 1.2rem;
    }

    .title {
      font-size: 1.1rem;
      font-weight: 400;
      color: rgba(255,255,255,0.7);
      margin-bottom: 0.3rem;
      letter-spacing: 0.05em;
    }

    .subtitle {
      font-size: 1.6rem;
      font-weight: 900;
      color: white;
      margin-bottom: 0.4rem;
      line-height: 1.2;
    }

    .exam-date {
      font-size: 0.85rem;
      color: rgba(255,255,255,0.45);
      margin-bottom: 2.5rem;
      letter-spacing: 0.05em;
    }

    /* Main countdown grid */
    .countdown-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0.8rem;
      margin-bottom: 1.5rem;
    }

    .unit-card {
      background: rgba(255,255,255,0.07);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 1rem;
      padding: 1rem 0.5rem;
      backdrop-filter: blur(10px);
      transition: transform 0.1s ease;
    }

    .unit-card:hover { transform: scale(1.03); }

    .unit-value {
      font-size: 2.2rem;
      font-weight: 900;
      line-height: 1;
      color: white;
      font-variant-numeric: tabular-nums;
      /* Pulse animation when value changes */
    }

    .unit-value.pulse {
      animation: pulse 0.3s ease;
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.15); color: #ffc850; }
      100% { transform: scale(1); }
    }

    .unit-label {
      font-size: 0.6rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: rgba(255,255,255,0.45);
      margin-top: 0.4rem;
    }

    /* Progress bar */
    .progress-section {
      margin-bottom: 1.8rem;
    }

    .progress-header {
      display: flex;
      justify-content: space-between;
      font-size: 0.72rem;
      color: rgba(255,255,255,0.45);
      margin-bottom: 0.5rem;
    }

    .progress-bar-bg {
      background: rgba(255,255,255,0.1);
      border-radius: 1rem;
      height: 6px;
      overflow: hidden;
    }

    .progress-bar-fill {
      height: 100%;
      background: linear-gradient(90deg, #ffc850, #ff6b6b);
      border-radius: 1rem;
      transition: width 1s linear;
    }

    /* Total seconds */
    .total-seconds {
      background: rgba(255, 200, 80, 0.08);
      border: 1px solid rgba(255, 200, 80, 0.2);
      border-radius: 0.8rem;
      padding: 1rem;
      margin-bottom: 1.5rem;
    }

    .total-seconds-value {
      font-size: 1.5rem;
      font-weight: 900;
      color: #ffc850;
      font-variant-numeric: tabular-nums;
      letter-spacing: -0.02em;
    }

    .total-seconds-label {
      font-size: 0.65rem;
      color: rgba(255,255,255,0.4);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      margin-top: 0.2rem;
    }

    /* Motivational message */
    .motivation {
      font-size: 0.8rem;
      color: rgba(255,255,255,0.4);
      font-style: italic;
      line-height: 1.5;
    }

    .motivation span {
      color: rgba(255,200,80,0.8);
      font-style: normal;
      font-weight: 600;
    }

    /* Install tip */
    .install-tip {
      position: fixed;
      bottom: 1.5rem;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(0,0,0,0.5);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 0.8rem;
      padding: 0.6rem 1rem;
      font-size: 0.65rem;
      color: rgba(255,255,255,0.4);
      text-align: center;
      width: calc(100% - 3rem);
      max-width: 380px;
      backdrop-filter: blur(5px);
      z-index: 10;
    }
  </style>
</head>
<body>

  <!-- Floating background particles -->
  <div class="bg-particles" id="particles"></div>

  <div class="container">
    <div class="badge">⚖️ Concours externe</div>

    <div class="title">Attaché territorial</div>
    <div class="subtitle">Spécialité Administration<br>Générale</div>
    <div class="exam-date">📅 Jeudi 19 novembre 2026</div>

    <!-- Countdown units -->
    <div class="countdown-grid">
      <div class="unit-card">
        <div class="unit-value" id="days">--</div>
        <div class="unit-label">Jours</div>
      </div>
      <div class="unit-card">
        <div class="unit-value" id="hours">--</div>
        <div class="unit-label">Heures</div>
      </div>
      <div class="unit-card">
        <div class="unit-value" id="minutes">--</div>
        <div class="unit-label">Minutes</div>
      </div>
      <div class="unit-card">
        <div class="unit-value" id="seconds">--</div>
        <div class="unit-label">Secondes</div>
      </div>
    </div>

    <!-- Progress bar -->
    <div class="progress-section">
      <div class="progress-header">
        <span>Progression de ta préparation</span>
        <span id="pct">0%</span>
      </div>
      <div class="progress-bar-bg">
        <div class="progress-bar-fill" id="progressBar" style="width:0%"></div>
      </div>
    </div>

    <!-- Total seconds block -->
    <div class="total-seconds">
      <div class="total-seconds-value" id="totalSeconds">--</div>
      <div class="total-seconds-label">secondes restantes au total</div>
    </div>

    <!-- Motivation -->
    <div class="motivation" id="motivMsg">
      Chaque seconde compte.<br>
      <span>La note de synthèse s'apprivoise avec la méthode.</span>
    </div>
  </div>

  <!-- Install tip -->
  <div class="install-tip" id="installTip">
    💡 Pour l'ajouter à ton écran d'accueil : <strong>Partager → Sur l'écran d'accueil</strong> (iOS) 
    ou <strong>Menu → Ajouter à l'écran d'accueil</strong> (Android)
  </div>

  <script>
    // ── Configuration ──────────────────────────────────────────────
    // Le concours commence à 8h00 le 19 novembre 2026
    const EXAM_DATE = new Date('2026-11-19T08:00:00');
    // Date de début de préparation (estimée : aujourd'hui)
    const START_DATE = new Date();

    // ── Particles ──────────────────────────────────────────────────
    function createParticles() {
      const container = document.getElementById('particles');
      for (let i = 0; i < 15; i++) {
        const p = document.createElement('div');
        p.className = 'particle';
        const size = Math.random() * 40 + 10;
        p.style.cssText = `
          width: ${size}px;
          height: ${size}px;
          left: ${Math.random() * 100}%;
          animation-duration: ${Math.random() * 15 + 10}s;
          animation-delay: ${Math.random() * 10}s;
        `;
        container.appendChild(p);
      }
    }

    // ── Motivational messages ───────────────────────────────────────
    const messages = [
      'Chaque seconde compte.<br><span>La note de synthèse s\'apprivoise avec la méthode.</span>',
      'Moins de X jours pour maîtriser l\'épreuve reine.<br><span>Plan • Hiérarchisation • Reformulation.</span>',
      'Le jury attend un professionnel, pas un encyclopédiste.<br><span>Sélectionne, structure, convaincs.</span>',
      'Une note réussie = dossier + plan + style sobre.<br><span>Tu as le temps. Utilise-le bien.</span>',
      'Coefficient 4 — c\'est l\'épreuve qui fait la différence.<br><span>Entraîne-toi sur les annales.</span>',
    ];

    let msgIndex = 0;

    // ── Padding helper ─────────────────────────────────────────────
    const pad = n => String(n).padStart(2, '0');

    // ── Format large numbers with spaces ───────────────────────────
    const fmtBig = n => n.toLocaleString('fr-FR');

    // ── Pulse animation on element ─────────────────────────────────
    function doPulse(el) {
      el.classList.remove('pulse');
      void el.offsetWidth; // reflow trick to restart animation
      el.classList.add('pulse');
    }

    // ── Previous values (to detect changes for pulse) ──────────────
    let prev = { d: -1, h: -1, m: -1, s: -1 };

    // ── Main tick function ─────────────────────────────────────────
    function tick() {
      const now = new Date();
      const diff = EXAM_DATE - now; // milliseconds

      if (diff <= 0) {
        // Exam day!
        document.querySelector('.subtitle').textContent = '🎓 C\'est le jour J !';
        document.getElementById('days').textContent = '00';
        document.getElementById('hours').textContent = '00';
        document.getElementById('minutes').textContent = '00';
        document.getElementById('seconds').textContent = '00';
        document.getElementById('totalSeconds').textContent = '0';
        document.getElementById('motivMsg').innerHTML =
          '<span>Bonne chance ! Tu as tout ce qu\'il faut.</span>';
        return;
      }

      // Decompose
      const totalSec = Math.floor(diff / 1000);
      const d = Math.floor(totalSec / 86400);
      const h = Math.floor((totalSec % 86400) / 3600);
      const m = Math.floor((totalSec % 3600) / 60);
      const s = totalSec % 60;

      // Update DOM + pulse on change
      const elD = document.getElementById('days');
      const elH = document.getElementById('hours');
      const elM = document.getElementById('minutes');
      const elS = document.getElementById('seconds');

      if (d !== prev.d) { elD.textContent = pad(d); doPulse(elD); prev.d = d; }
      if (h !== prev.h) { elH.textContent = pad(h); doPulse(elH); prev.h = h; }
      if (m !== prev.m) { elM.textContent = pad(m); doPulse(elM); prev.m = m; }
      if (s !== prev.s) { elS.textContent = pad(s); doPulse(elS); prev.s = s; }

      document.getElementById('totalSeconds').textContent = fmtBig(totalSec);

      // Progress bar: % of preparation time elapsed
      const totalPrep = EXAM_DATE - START_DATE;
      const elapsed = now - START_DATE;
      const pct = Math.min(100, Math.max(0, (elapsed / totalPrep) * 100));
      document.getElementById('progressBar').style.width = pct.toFixed(2) + '%';
      document.getElementById('pct').textContent = pct.toFixed(1) + '%';

      // Rotate motivation message every 10 seconds
      const idx = Math.floor(Date.now() / 10000) % messages.length;
      if (idx !== msgIndex) {
        msgIndex = idx;
        document.getElementById('motivMsg').innerHTML = messages[idx];
      }
    }

    // ── Init ───────────────────────────────────────────────────────
    createParticles();
    tick();
    setInterval(tick, 1000);

    // Hide install tip after 8 seconds
    setTimeout(() => {
      const tip = document.getElementById('installTip');
      tip.style.transition = 'opacity 1s';
      tip.style.opacity = '0';
      setTimeout(() => tip.remove(), 1000);
    }, 8000);
  </script>
</body>
</html>
min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      color: white;
      overflow: hidden;
    }

    /* Animated background particles */
    .bg-particles {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      pointer-events: none;
      z-index: 0;
    }

    .particle {
      position: absolute;
      border-radius: 50%;
      background: rgba(255,255,255,0.05);
      animation: float linear infinite;
    }

    @keyframes float {
      0% { transform: translateY(100vh) scale(0); opacity: 0; }
      10% { opacity: 1; }
      90% { opacity: 1; }
      100% { transform: translateY(-10vh) scale(1); opacity: 0; }
    }

    .container {
      position: relative;
      z-index: 1;
      text-align: center;
      padding: 2rem 1.5rem;
      max-width: 420px;
      width: 100%;
    }

    .badge {
      display: inline-block;
      background: rgba(255, 200, 80, 0.15);
      border: 1px solid rgba(255, 200, 80, 0.4);
      color: #ffc850;
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      padding: 0.4rem 1rem;
      border-radius: 2rem;
      margin-bottom: 1.2rem;
    }

    .title {
      font-size: 1.1rem;
      font-weight: 400;
      color: rgba(255,255,255,0.7);
      margin-bottom: 0.3rem;
      letter-spacing: 0.05em;
    }

    .subtitle {
      font-size: 1.6rem;
      font-weight: 900;
      color: white;
      margin-bottom: 0.4rem;
      line-height: 1.2;
    }

    .exam-date {
      font-size: 0.85rem;
      color: rgba(255,255,255,0.45);
      margin-bottom: 2.5rem;
      letter-spacing: 0.05em;
    }

    /* Main countdown grid */
    .countdown-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0.8rem;
      margin-bottom: 1.5rem;
    }

    .unit-card {
      background: rgba(255,255,255,0.07);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 1rem;
      padding: 1rem 0.5rem;
      backdrop-filter: blur(10px);
      transition: transform 0.1s ease;
    }

    .unit-card:hover { transform: scale(1.03); }

    .unit-value {
      font-size: 2.2rem;
      font-weight: 900;
      line-height: 1;
      color: white;
      font-variant-numeric: tabular-nums;
      /* Pulse animation when value changes */
    }

    .unit-value.pulse {
      animation: pulse 0.3s ease;
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.15); color: #ffc850; }
      100% { transform: scale(1); }
    }

    .unit-label {
      font-size: 0.6rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: rgba(255,255,255,0.45);
      margin-top: 0.4rem;
    }

    /* Progress bar */
    .progress-section {
      margin-bottom: 1.8rem;
    }

    .progress-header {
      display: flex;
      justify-content: space-between;
      font-size: 0.72rem;
      color: rgba(255,255,255,0.45);
      margin-bottom: 0.5rem;
    }

    .progress-bar-bg {
      background: rgba(255,255,255,0.1);
      border-radius: 1rem;
      height: 6px;
      overflow: hidden;
    }

    .progress-bar-fill {
      height: 100%;
      background: linear-gradient(90deg, #ffc850, #ff6b6b);
      border-radius: 1rem;
      transition: width 1s linear;
    }

    /* Total seconds */
    .total-seconds {
      background: rgba(255, 200, 80, 0.08);
      border: 1px solid rgba(255, 200, 80, 0.2);
      border-radius: 0.8rem;
      padding: 1rem;
      margin-bottom: 1.5rem;
    }

    .total-seconds-value {
      font-size: 1.5rem;
      font-weight: 900;
      color: #ffc850;
      font-variant-numeric: tabular-nums;
      letter-spacing: -0.02em;
    }

    .total-seconds-label {
      font-size: 0.65rem;
      color: rgba(255,255,255,0.4);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      margin-top: 0.2rem;
    }

    /* Motivational message */
    .motivation {
      font-size: 0.8rem;
      color: rgba(255,255,255,0.4);
      font-style: italic;
      line-height: 1.5;
    }

    .motivation span {
      color: rgba(255,200,80,0.8);
      font-style: normal;
      font-weight: 600;
    }

    /* Install tip */
    .install-tip {
      position: fixed;
      bottom: 1.5rem;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(0,0,0,0.5);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 0.8rem;
      padding: 0.6rem 1rem;
      font-size: 0.65rem;
      color: rgba(255,255,255,0.4);
      text-align: center;
      width: calc(100% - 3rem);
      max-width: 380px;
      backdrop-filter: blur(5px);
      z-index: 10;
    }
  </style>
</head>
<body>

  <!-- Floating background particles -->
  <div class="bg-particles" id="particles"></div>

  <div class="container">
    <div class="badge">⚖️ Concours externe</div>

    <div class="title">Attaché territorial</div>
    <div class="subtitle">Spécialité Administration<br>Générale</div>
    <div class="exam-date">📅 Jeudi 19 novembre 2026</div>

    <!-- Countdown units -->
    <div class="countdown-grid">
      <div class="unit-card">
        <div class="unit-value" id="days">--</div>
        <div class="unit-label">Jours</div>
      </div>
      <div class="unit-card">
        <div class="unit-value" id="hours">--</div>
        <div class="unit-label">Heures</div>
      </div>
      <div class="unit-card">
        <div class="unit-value" id="minutes">--</div>
        <div class="unit-label">Minutes</div>
      </div>
      <div class="unit-card">
        <div class="unit-value" id="seconds">--</div>
        <div class="unit-label">Secondes</div>
      </div>
    </div>

    <!-- Progress bar -->
    <div class="progress-section">
      <div class="progress-header">
        <span>Progression de ta préparation</span>
        <span id="pct">0%</span>
      </div>
      <div class="progress-bar-bg">
        <div class="progress-bar-fill" id="progressBar" style="width:0%"></div>
      </div>
    </div>

    <!-- Total seconds block -->
    <div class="total-seconds">
      <div class="total-seconds-value" id="totalSeconds">--</div>
      <div class="total-seconds-label">secondes restantes au total</div>
    </div>

    <!-- Motivation -->
    <div class="motivation" id="motivMsg">
      Chaque seconde compte.<br>
      <span>La note de synthèse s'apprivoise avec la méthode.</span>
    </div>
  </div>

  <!-- Install tip -->
  <div class="install-tip" id="installTip">
    💡 Pour l'ajouter à ton écran d'accueil : <strong>Partager → Sur l'écran d'accueil</strong> (iOS) 
    ou <strong>Menu → Ajouter à l'écran d'accueil</strong> (Android)
  </div>

  <script>
    // ── Configuration ──────────────────────────────────────────────
    // Le concours commence à 8h00 le 19 novembre 2026
    const EXAM_DATE = new Date('2026-11-19T08:00:00');
    // Date de début de préparation (estimée : aujourd'hui)
    const START_DATE = new Date();

    // ── Particles ──────────────────────────────────────────────────
    function createParticles() {
      const container = document.getElementById('particles');
      for (let i = 0; i < 15; i++) {
        const p = document.createElement('div');
        p.className = 'particle';
        const size = Math.random() * 40 + 10;
        p.style.cssText = `
          width: ${size}px;
          height: ${size}px;
          left: ${Math.random() * 100}%;
          animation-duration: ${Math.random() * 15 + 10}s;
          animation-delay: ${Math.random() * 10}s;
        `;
        container.appendChild(p);
      }
    }

    // ── Motivational messages ───────────────────────────────────────
    const messages = [
      'Chaque seconde compte.<br><span>La note de synthèse s\'apprivoise avec la méthode.</span>',
      'Moins de X jours pour maîtriser l\'épreuve reine.<br><span>Plan • Hiérarchisation • Reformulation.</span>',
      'Le jury attend un professionnel, pas un encyclopédiste.<br><span>Sélectionne, structure, convaincs.</span>',
      'Une note réussie = dossier + plan + style sobre.<br><span>Tu as le temps. Utilise-le bien.</span>',
      'Coefficient 4 — c\'est l\'épreuve qui fait la différence.<br><span>Entraîne-toi sur les annales.</span>',
    ];

    let msgIndex = 0;

    // ── Padding helper ─────────────────────────────────────────────
    const pad = n => String(n).padStart(2, '0');

    // ── Format large numbers with spaces ───────────────────────────
    const fmtBig = n => n.toLocaleString('fr-FR');

    // ── Pulse animation on element ─────────────────────────────────
    function doPulse(el) {
      el.classList.remove('pulse');
      void el.offsetWidth; // reflow trick to restart animation
      el.classList.add('pulse');
    }

    // ── Previous values (to detect changes for pulse) ──────────────
    let prev = { d: -1, h: -1, m: -1, s: -1 };

    // ── Main tick function ─────────────────────────────────────────
    function tick() {
      const now = new Date();
      const diff = EXAM_DATE - now; // milliseconds

      if (diff <= 0) {
        // Exam day!
        document.querySelector('.subtitle').textContent = '🎓 C\'est le jour J !';
        document.getElementById('days').textContent = '00';
        document.getElementById('hours').textContent = '00';
        document.getElementById('minutes').textContent = '00';
        document.getElementById('seconds').textContent = '00';
        document.getElementById('totalSeconds').textContent = '0';
        document.getElementById('motivMsg').innerHTML =
          '<span>Bonne chance ! Tu as tout ce qu\'il faut.</span>';
        return;
      }

      // Decompose
      const totalSec = Math.floor(diff / 1000);
      const d = Math.floor(totalSec / 86400);
      const h = Math.floor((totalSec % 86400) / 3600);
      const m = Math.floor((totalSec % 3600) / 60);
      const s = totalSec % 60;

      // Update DOM + pulse on change
      const elD = document.getElementById('days');
      const elH = document.getElementById('hours');
      const elM = document.getElementById('minutes');
      const elS = document.getElementById('seconds');

      if (d !== prev.d) { elD.textContent = pad(d); doPulse(elD); prev.d = d; }
      if (h !== prev.h) { elH.textContent = pad(h); doPulse(elH); prev.h = h; }
      if (m !== prev.m) { elM.textContent = pad(m); doPulse(elM); prev.m = m; }
      if (s !== prev.s) { elS.textContent = pad(s); doPulse(elS); prev.s = s; }

      document.getElementById('totalSeconds').textContent = fmtBig(totalSec);

      // Progress bar: % of preparation time elapsed
      const totalPrep = EXAM_DATE - START_DATE;
      const elapsed = now - START_DATE;
      const pct = Math.min(100, Math.max(0, (elapsed / totalPrep) * 100));
      document.getElementById('progressBar').style.width = pct.toFixed(2) + '%';
      document.getElementById('pct').textContent = pct.toFixed(1) + '%';

      // Rotate motivation message every 10 seconds
      const idx = Math.floor(Date.now() / 10000) % messages.length;
      if (idx !== msgIndex) {
        msgIndex = idx;
        document.getElementById('motivMsg').innerHTML = messages[idx];
      }
    }

    // ── Init ───────────────────────────────────────────────────────
    createParticles();
    tick();
    setInterval(tick, 1000);

    // Hide install tip after 8 seconds
    setTimeout(() => {
      const tip = document.getElementById('installTip');
      tip.style.transition = 'opacity 1s';
      tip.style.opacity = '0';
      setTimeout(() => tip.remove(), 1000);
    }, 8000);
  </script>
</body>
</html>
