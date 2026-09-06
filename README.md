<style>
  /* ── Arcade CRT Scanlines ── */
  .arcade-wrapper {
    position: relative;
  }
  .arcade-wrapper::before {
    content: "";
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      rgba(0, 0, 0, 0.08) 0px,
      rgba(0, 0, 0, 0.08) 1px,
      transparent 1px,
      transparent 3px
    );
    pointer-events: none;
    z-index: 9999;
  }

  /* ── Neon Pulse Glow ── */
  @keyframes neonPulse {
    0%, 100% { text-shadow: 0 0 5px #00ff66, 0 0 10px #00ff66, 0 0 20px #00ff66; }
    50% { text-shadow: 0 0 10px #00ff66, 0 0 20px #00ff66, 0 0 40px #00ff66, 0 0 80px #00ff66; }
  }
  @keyframes borderGlow {
    0%, 100% { box-shadow: 0 0 5px #00ff6680, inset 0 0 5px #00ff6620; }
    50% { box-shadow: 0 0 15px #00ff66aa, inset 0 0 10px #00ff6640; }
  }
  @keyframes flowDash {
    to { stroke-dashoffset: -24; }
  }
  @keyframes slideIn {
    from { max-height: 0; opacity: 0; transform: translateY(-10px); }
    to { max-height: 500px; opacity: 1; transform: translateY(0); }
  }
  @keyframes barFill {
    from { width: 0%; }
  }
  @keyframes blink {
    0%, 49% { opacity: 1; }
    50%, 100% { opacity: 0; }
  }
  @keyframes snakeSway {
    0%, 100% { transform: translateX(0) rotate(0deg); }
    25% { transform: translateX(3px) rotate(0.5deg); }
    75% { transform: translateX(-3px) rotate(-0.5deg); }
  }
  @keyframes coinSpin {
    0% { transform: rotateY(0deg); }
    100% { transform: rotateY(360deg); }
  }
  @keyframes glitchShift {
    0%, 100% { transform: translate(0); }
    20% { transform: translate(-2px, 1px); }
    40% { transform: translate(2px, -1px); }
    60% { transform: translate(-1px, 2px); }
    80% { transform: translate(1px, -2px); }
  }

  /* ── Interactive Cards ── */
  .arcade-card {
    transition: all 0.3s ease;
    border: 1px solid #00ff6630;
    background: linear-gradient(135deg, #060d09 0%, #0a1f14 100%);
    border-radius: 8px;
  }
  .arcade-card:hover {
    border-color: #00ff66aa;
    box-shadow: 0 0 20px #00ff6640, inset 0 0 15px #00ff6615;
    transform: translateY(-4px);
  }

  /* ── Stat Bars ── */
  .stat-bar-container {
    background: #0a1f14;
    border-radius: 12px;
    overflow: hidden;
    height: 18px;
    border: 1px solid #00ff6630;
  }
  .stat-bar-fill {
    height: 100%;
    border-radius: 12px;
    background: linear-gradient(90deg, #00ff66, #0a5c32);
    animation: barFill 1.5s ease-out forwards;
    position: relative;
  }
  .stat-bar-fill::after {
    content: "";
    position: absolute;
    right: 0;
    top: 0;
    bottom: 0;
    width: 6px;
    background: #ffffff40;
    border-radius: 0 12px 12px 0;
  }

  /* ── Terminal Cursor ── */
  .terminal-cursor {
    display: inline-block;
    width: 10px;
    height: 1.2em;
    background: #00ff66;
    margin-left: 2px;
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
  }

  /* ── Animated Dividers ── */
  .arcade-divider {
    border: none;
    height: 2px;
    background: linear-gradient(90deg, transparent, #00ff66, transparent);
    margin: 1rem 0;
    position: relative;
  }
  .arcade-divider svg {
    width: 100%;
    height: 2px;
  }
  .arcade-divider line {
    stroke: url(#neonGradient);
    stroke-width: 2;
    stroke-dasharray: 8 4;
    animation: flowDash 0.6s linear infinite;
  }

  /* ── Hover Panels ── */
  .expand-panel {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.4s ease, opacity 0.3s ease, padding 0.3s ease;
    opacity: 0;
    background: #0a1f1480;
    border-radius: 6px;
  }
  .expand-panel.open {
    max-height: 400px;
    opacity: 1;
    padding: 12px;
  }

  /* ── Coin Counter Spin ── */
  .coin-flip {
    display: inline-block;
    animation: coinSpin 3s linear infinite;
    transform-style: preserve-3d;
  }

  /* ── Glitch Effect on Hover ── */
  .glitch-hover:hover {
    animation: glitchShift 0.3s ease infinite;
  }

  /* ── Badge Shield Hover ── */
  .badge-shield {
    transition: transform 0.2s ease, filter 0.2s ease;
  }
  .badge-shield:hover {
    transform: scale(1.1);
    filter: brightness(1.3) drop-shadow(0 0 6px #00ff66);
  }

  /* ── Responsive Grid ── */
  .skill-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 16px;
    padding: 8px;
  }
  @media (max-width: 768px) {
    .skill-grid { grid-template-columns: 1fr; }
  }

  /* ── Clickable Toggle Button ── */
  .toggle-btn {
    background: linear-gradient(135deg, #00ff6620, #00ff6610);
    border: 1px solid #00ff6660;
    color: #00ff66;
    padding: 8px 20px;
    border-radius: 6px;
    cursor: pointer;
    font-family: 'Press Start 2P', monospace;
    font-size: 10px;
    transition: all 0.2s ease;
  }
  .toggle-btn:hover {
    background: linear-gradient(135deg, #00ff6640, #00ff6620);
    box-shadow: 0 0 15px #00ff6660;
  }
</style>

<div class="arcade-wrapper">

<!-- ═══════════════════ HEADER BANNER ═══════════════════ -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:050d09,50:0a1f14,100:030805&height=220&section=header&text=KevinTadashiii&fontSize=48&fontColor=00ff66&fontAlignY=42&desc=%F0%9F%90%8D%20ARCADE%20SNAKE%20EDITION%20%E2%80%A2%20LVL%2017%20DEV%20%E2%80%A2%20SMKN%202%20BDG&descAlignY=66&descAlign=50&descSize=16&stroke=00ff66&strokeWidth=2" width="100%" alt="Header Banner" />

<br/>

<a href="https://github.com/KevinTadashiii">
  <img src="https://readme-typing-svg.demolab.com?font=Press+Start+2P&size=13&pause=1000&color=00FF66&center=true&vCenter=true&width=850&height=45&lines=%3E+PLAYER_1+CONNECTED%3A+KevinTadashiii;%3E+LEVEL%3A+17+Y%2FO+%7C+SMKN+2+BANDUNG;%3E+EXP%3A+CODING+SINCE+GRADE+6+ELEMENTARY;%3E+MISSION%3A+SLITHER+THROUGH+BUGS+%26+DOMINATE+THE+LEADERBOARD+%F0%9F%8F%86;%3E+INSERT+COIN+TO+COMMENCE+GAMEPLAY+%F0%9F%95%B9%EF%B8%8F" alt="Typing Banner" />
</a>

</div>

<!-- ═══════════════════ HUD STATUS BAR ═══════════════════ -->
<br/>

<table style="background: #060d09; border: 1px solid #00ff6640; border-radius: 8px; overflow: hidden; animation: borderGlow 3s ease-in-out infinite;">
  <tr>
    <td align="center" style="padding: 10px;"><b>🎮 PLAYER</b><br/><code style="color:#00ff66;">KevinTadashiii</code></td>
    <td align="center" style="padding: 10px;"><b>❤️ HP</b><br/><span style="color:#ff4444;">♥♥♥♥♥</span> <code>[MAX]</code></td>
    <td align="center" style="padding: 10px;"><b>⚡ LVL</b><br/><code style="animation: neonPulse 2s ease-in-out infinite; display:inline-block;">LEVEL 17</code></td>
    <td align="center" style="padding: 10px;"><b>🏫 GUILD</b><br/><code>SMKN 2 BDG</code></td>
    <td align="center" style="padding: 10px;"><b>⏳ EXP ORIGIN</b><br/><code>6TH GRADE</code></td>
    <td align="center" style="padding: 10px;"><b><span class="coin-flip">🪙</span> COINS</b><br/><code style="color:#ffd700;">9696969</code></td>
  </tr>
</table>

<br/>

<hr class="arcade-divider">
<svg style="display:none"><defs><linearGradient id="neonGradient" x1="0%" y1="0%" x2="100%" y2="0%"><stop offset="0%" stop-color="#00ff66"/><stop offset="50%" stop-color="#00ff66cc"/><stop offset="100%" stop-color="#00ff66"/></linearGradient></defs></svg>

<!-- ═══════════════════ RPG DIALOGUE BOX ═══════════════════ -->

<table width="100%" style="background: #060d09; border: 1px solid #00ff6630; border-radius: 8px; padding: 16px;">
  <tr>
    <td width="100" align="center" valign="middle" style="border-right: 1px solid #00ff6620;">
      <img src="https://api.iconify.design/pixelarticons:human-handsup.svg?color=%2300ff66" width="60" height="60" alt="Pixel Avatar" /><br/>
      <sub><b style="animation: neonPulse 3s ease-in-out infinite; display:inline-block;">[ KEVIN ]</b></sub>
    </td>
    <td style="padding-left: 16px;">
      <img src="https://readme-typing-svg.demolab.com?font=Press+Start+2P&size=10&pause=5000&color=00FF66&vCenter=true&width=550&height=25&lines=%22HELLO+WORLD!+WELCOME+TO+MY+ARCADE+DOMAIN.%22" alt="Speech" /><br/><br/>
      <i>"I'm a 17-year-old student developer from <b>SMKN 2 Bandung</b>. My coding adventure started way back in <b>6th grade elementary school</b> when curiosity took over. Ever since, I've been grinding quests in Full-Stack Web Development, breaking and fixing code, doing some low level stuff, homelabing, making game, and slithering around bugs like a classic snake game!"</i>
      <span class="terminal-cursor"></span>
    </td>
  </tr>
</table>

<br/>

<hr class="arcade-divider">

<!-- ═══════════════════ SNAKE ARENA ═══════════════════ -->
<div align="center">

<table style="background: #060d09; border: 1px solid #00ff6630; border-radius: 8px; padding: 8px;" class="arcade-card">
  <thead>
    <tr>
      <th align="center" style="font-size: 14px; color: #00ff66; text-transform: uppercase; letter-spacing: 2px;">
        🕹️ <b>SNAKE.EXE // REAL-TIME CONTRIBUTION ARENA</b> 🍎
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KevinTadashiii/KevinTadashiii/output/github-contribution-grid-snake-dark.svg">
          <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/KevinTadashiii/KevinTadashiii/output/github-contribution-grid-snake.svg">
          <img alt="Snake Contribution Graph" src="https://raw.githubusercontent.com/KevinTadashiii/KevinTadashiii/output/github-contribution-grid-snake-dark.svg" width="100%">
        </picture>
        <br/>
        <code style="color:#00ff66; font-size:11px;">[ 🟢 ── 🟢 ── 🟢 ── 🟢 ── 🟢 ── 🐍 DEVOURING COMMITS... 🍎 ]</code>
      </td>
    </tr>
  </tbody>
</table>

</div>

<br/>

<hr class="arcade-divider">

<!-- ═══════════════════ INVENTORY & SKILL TREE ═══════════════════ -->
<div align="center">

### 🎒 `[ INVENTORY & SKILL TREE ]`

<div class="skill-grid">

<!-- Weapons Card -->
<div class="arcade-card" style="padding: 16px;">
  <b style="color:#00ff66; animation: neonPulse 4s ease-in-out infinite; display:inline-block;">⚔️ WEAPONS (LANGUAGES)</b>
  <hr style="border-color:#00ff6630;">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=html,css,js,ts,py,c,cpp,rust,kotlin&theme=dark&perline=3" alt="Languages" />
  </a>
  <br/><br/>
  <code>HTML5 • CSS3 • JS</code><br/>
  <code>TS • Python • C</code><br/>
  <code>C++ • Rust • Kotlin</code>
</div>

<!-- Armor Card -->
<div class="arcade-card" style="padding: 16px;">
  <b style="color:#00ff66; animation: neonPulse 4s ease-in-out 0.5s infinite; display:inline-block;">🛡️ ARMOR (FRAMEWORKS)</b>
  <hr style="border-color:#00ff6630;">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=react,nextjs,tailwind,laravel,express,fastapi,flutter&theme=dark&perline=3" alt="Frameworks" />
  </a>
  <br/><br/>
  <code>React • Next.js • Tailwind</code><br/>
  <code>Laravel • Express.js</code><br/>
  <code>FastAPI • Flutter</code>
</div>

<!-- Tools Card -->
<div class="arcade-card" style="padding: 16px;">
  <b style="color:#00ff66; animation: neonPulse 4s ease-in-out 1s infinite; display:inline-block;">🧰 TOOLS & UTILITIES</b>
  <hr style="border-color:#00ff6630;">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=mysql,docker,postman,git,github,vscode,idea,linux,windows&theme=dark&perline=3" alt="Tools" />
  </a>
  <br/><br/>
  <code>MySQL • Docker • Postman</code><br/>
  <code>Git • GitHub • VS Code</code><br/>
  <code>JetBrains • Linux • Windows</code>
</div>

</div>

</div>

<br/>

<hr class="arcade-divider">

<!-- ═══════════════════ CHARACTER ATTRIBUTES ═══════════════════ -->
<div align="center">

### 📊 `[ CHARACTER ATTRIBUTES & METERS ]`

<table>
  <tr>
    <td style="width:30%; vertical-align:middle;"><b>⚡ PROBLEM SOLVING</b></td>
    <td style="width:25%;"><div class="stat-bar-container"><div class="stat-bar-fill" style="width: 90%;"></div></div></td>
    <td><code>[██████████████████░░] 90/100</code></td>
    <td style="width:30%; vertical-align:middle;"><b>🔥 AGILITY & LEARNING</b></td>
    <td style="width:25%;"><div class="stat-bar-container"><div class="stat-bar-fill" style="width: 100%;"></div></div></td>
    <td><code>[████████████████████] MAX</code></td>
  </tr>
  <tr>
    <td style="vertical-align:middle;"><b>🐧 LINUX & HOMELAB</b></td>
    <td><div class="stat-bar-container"><div class="stat-bar-fill" style="width: 100%;"></div></div></td>
    <td><code>[████████████████████] MAX</code></td>
    <td style="vertical-align:middle;"><b>🐍 BUG SLITHERING</b></td>
    <td><div class="stat-bar-container"><div class="stat-bar-fill" style="width: 100%;"></div></div></td>
    <td><code>[████████████████████] MAX</code></td>
  </tr>
  <tr>
    <td style="vertical-align:middle;"><b>☕ CAFFEINE CONSUMPTION</b></td>
    <td><div class="stat-bar-container"><div class="stat-bar-fill" style="width: 5%; background: linear-gradient(90deg, #ffaa00, #ff6600);"></div></div></td>
    <td><code>[░░░░░░░░░░░░░░░░░░░░] LOW</code></td>
    <td style="vertical-align:middle;"><b>🏫 SMKN 2 PRIDE</b></td>
    <td><div class="stat-bar-container"><div class="stat-bar-fill" style="width: 100%; background: linear-gradient(90deg, #00ff66, #00ffaa);"></div></div></td>
    <td><code>[████████████████████] ∞</code></td>
  </tr>
</table>

</div>

<br/>

<hr class="arcade-divider">

<!-- ═══════════════════ HIGH SCORES & TELEMETRY ═══════════════════ -->
<div align="center">

### 🏆 `[ ARCADE HIGH SCORES & TELEMETRY ]`

<table>
  <tr>
    <td align="center" valign="middle">
      <a href="https://github.com/stats-organization/github-stats-extended">
        <img src="https://github-stats-extended.vercel.app/api?username=KevinTadashiii&theme=chartreuse-dark" alt="Kevin's GitHub stats" class="badge-shield" />
      </a>
    </td>
    <td align="center" valign="middle">
      <img src="https://streak-stats.demolab.com?user=KevinTadashiii&theme=matrix&hide_border=false&border=00ff66&background=060d09&ring=00ff66&fire=00ff66&currStreakLabel=00ff66&currStreakNum=00ff66&sideNums=00ff66&sideLabels=80df9e&dates=80df9e" alt="GitHub Streak" class="badge-shield" />
    </td>
  </tr>
  <tr>
    <td colspan="2" align="center">
      <img src="https://github-stats-extended.vercel.app/api/top-langs?username=KevinTadashiii&langs_count=5&theme=chartreuse-dark" alt="Top Languages" class="badge-shield" />
    </td>
  </tr>
</table>

</div>

<br/>

<hr class="arcade-divider">

<!-- ═══════════════════ MULTIPLAYER LOBBY ═══════════════════ -->
<div align="center">

### 🕹️ `[ MULTIPLAYER LOBBY // INSERT COIN TO CO-OP ]`

<table style="background: #060d09; border: 1px solid #00ff6630; border-radius: 8px; padding: 16px;" class="arcade-card">
  <tr>
    <td align="center" colspan="3">
      <code style="color:#00ff66;">[ CONTROLLER 1 ]</code><br/>
      <kbd style="background:#0a1f14; border:1px solid #00ff6660; color:#00ff66; padding:4px 8px; border-radius:4px;">▲ W</kbd><br/>
      <kbd style="background:#0a1f14; border:1px solid #00ff6660; color:#00ff66; padding:4px 8px; border-radius:4px;">◄ A</kbd>
      &nbsp;
      <kbd style="background:#0a1f14; border:1px solid #00ff6660; color:#00ff66; padding:4px 8px; border-radius:4px;">▼ S</kbd>
      &nbsp;
      <kbd style="background:#0a1f14; border:1px solid #00ff6660; color:#00ff66; padding:4px 8px; border-radius:4px;">► D</kbd><br/>
      <small style="color:#80df9e;"><i>CONTROL THE SNAKE & CHOOSE YOUR CONTACT PORTAL:</i></small>
    </td>
  </tr>
  <tr>
    <td align="center" style="padding: 8px;">
      <a href="mailto:kevintadashiii@gmail.com">
        <img src="https://img.shields.io/badge/EMAIL-060d09?style=for-the-badge&logo=gmail&logoColor=00ff66&labelColor=000000" alt="Email" class="badge-shield" />
      </a>
    </td>
    <td align="center" style="padding: 8px;">
      <a href="https://www.instagram.com/bayabaytjn_/" target="_blank">
        <img src="https://img.shields.io/badge/INSTAGRAM-060d09?style=for-the-badge&logo=instagram&logoColor=00ff66&labelColor=000000" alt="Instagram" class="badge-shield" />
      </a>
    </td>
    <td align="center" style="padding: 8px;">
      <a href="https://www.reddit.com/user/kevintadashi/" target="_blank">
        <img src="https://img.shields.io/badge/REDDIT-060d09?style=for-the-badge&logo=reddit&logoColor=00ff66&labelColor=000000" alt="Reddit" class="badge-shield" />
      </a>
    </td>
  </tr>
</table>

<br/>

<img src="https://readme-typing-svg.demolab.com?font=Press+Start+2P&size=14&pause=1000&color=00FF66&center=true&vCenter=true&width=550&height=50&lines=%F0%9F%AA%99+INSERT+COIN+TO+PLAY...;%F0%9F%AA%99+1+CREDIT+INSERTED;%F0%9F%91%BE+READY+FOR+NEW+ADVENTURES%21" alt="Insert Coin" />

<br/>

<div align="center">
  <img src="https://media.giphy.com/media/12cpBxBl4WqlHO/giphy.gif" width="240" alt="Michael Jackson Moonwalk" style="animation: snakeSway 2s ease-in-out infinite;" />
</div>

<br/><br/><br/>

<!-- ═══════════════════ RETRO CHEAT CODES ═══════════════════ -->
<div align="center">

<button class="toggle-btn" onclick="document.getElementById('cheat-menu').classList.toggle('open')">
  🕹️ [ ENTER RETRO CHEAT CODE ]
</button>

<div id="cheat-menu" class="expand-panel" style="margin-top: 12px; text-align: left; max-width: 500px;">
  <table>
    <tr><td style="color:#00ff66; font-family:'Press Start 2P',monospace; font-size:10px; padding:4px 0;">🐍 UP UP DOWN DOWN LEFT RIGHT LEFT RIGHT B A</td></tr>
    <tr><td style="padding:8px 0; color:#80df9e;">➤ <i>* 30 Lives Activated *</i></td></tr>
    <tr style="border-top: 1px dashed #00ff6630;"><td style="color:#00ff66; font-family:'Press Start 2P',monospace; font-size:10px; padding:4px 0;">💰 ZEROZEROZERO</td></tr>
    <tr><td style="padding:8px 0; color:#80df9e;">➤ <i>* Infinite Coins +1 💰💰💰 *</i></td></tr>
    <tr style="border-top: 1px dashed #00ff6630;"><td style="color:#00ff66; font-family:'Press Start 2P',monospace; font-size:10px; padding:4px 0;">🌙 FULLMOON</td></tr>
    <tr><td style="padding:8px 0; color:#80df9e;">➤ <i>* ...heee hee * 🕺</i></td></tr>
    <tr style="border-top: 1px dashed #00ff6630;"><td style="color:#00ff66; font-family:'Press Start 2P',monospace; font-size:10px; padding:4px 0;">👾 KONAMI CODE ↑↑↓↓←→←→BA</td></tr>
    <tr><td style="padding:8px 0; color:#80df9e;">➤ <i>* SECRET UNLOCKED — You found the Konami Code! ✨ *</i></td></tr>
  </table>
</div>

</div>

<!-- Footer Retro Wave -->
<br/><br/>
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:050d09,50:0a1f14,100:00ff66&height=100&section=footer" width="100%" alt="Footer Wave" />

</div>

</div>

</file_path>
</function>
</tool_call>