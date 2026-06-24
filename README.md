<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CarWorld — Dunyo Mashinalari</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Inter:wght@300;400;500;600&display=swap');

  :root {
    --bg: #0a0a0f;
    --surface: #12121a;
    --card: #1a1a26;
    --border: #2a2a3e;
    --accent: #e8401a;
    --accent2: #ff6b35;
    --text: #e8e8f0;
    --muted: #7070a0;
    --glow: rgba(232, 64, 26, 0.3);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    min-height: 100vh;
  }

  /* HEADER */
  header {
    background: linear-gradient(135deg, #0a0a0f 0%, #1a0a05 50%, #0a0a0f 100%);
    border-bottom: 1px solid var(--border);
    padding: 18px 20px;
    position: sticky;
    top: 0;
    z-index: 100;
    backdrop-filter: blur(10px);
  }

  .header-inner {
    max-width: 900px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .logo {
    font-family: 'Orbitron', monospace;
    font-size: 22px;
    font-weight: 900;
    color: var(--accent);
    letter-spacing: 2px;
    text-shadow: 0 0 20px var(--glow);
  }

  .logo span { color: var(--text); }

  .tagline {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-left: auto;
  }

  /* HERO */
  .hero {
    background: radial-gradient(ellipse at 50% 0%, rgba(232,64,26,0.15) 0%, transparent 70%);
    padding: 40px 20px 30px;
    text-align: center;
  }

  .hero h1 {
    font-family: 'Orbitron', monospace;
    font-size: clamp(24px, 6vw, 42px);
    font-weight: 900;
    line-height: 1.1;
    margin-bottom: 10px;
  }

  .hero h1 em {
    font-style: normal;
    color: var(--accent);
    text-shadow: 0 0 30px var(--glow);
  }

  .hero p {
    color: var(--muted);
    font-size: 14px;
    margin-bottom: 28px;
  }

  /* SEARCH */
  .search-wrap {
    max-width: 600px;
    margin: 0 auto;
    position: relative;
  }

  .search-input {
    width: 100%;
    background: var(--card);
    border: 2px solid var(--border);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    font-size: 15px;
    padding: 14px 120px 14px 18px;
    border-radius: 12px;
    outline: none;
    transition: border-color 0.3s, box-shadow 0.3s;
  }

  .search-input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--glow);
  }

  .search-input::placeholder { color: var(--muted); }

  .search-btn {
    position: absolute;
    right: 6px;
    top: 50%;
    transform: translateY(-50%);
    background: var(--accent);
    color: white;
    border: none;
    font-family: 'Orbitron', monospace;
    font-size: 12px;
    font-weight: 700;
    padding: 10px 18px;
    border-radius: 8px;
    cursor: pointer;
    letter-spacing: 1px;
    transition: background 0.2s, box-shadow 0.2s;
  }

  .search-btn:hover { background: var(--accent2); box-shadow: 0 0 20px var(--glow); }
  .search-btn:disabled { opacity: 0.6; cursor: not-allowed; }

  /* POPULAR */
  .quick-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: center;
    margin-top: 16px;
  }

  .tag {
    background: var(--card);
    border: 1px solid var(--border);
    color: var(--muted);
    font-size: 12px;
    padding: 5px 12px;
    border-radius: 20px;
    cursor: pointer;
    transition: all 0.2s;
  }

  .tag:hover { border-color: var(--accent); color: var(--accent); }

  /* STATS BAR */
  .stats-bar {
    display: flex;
    justify-content: center;
    gap: 30px;
    padding: 20px;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    background: var(--surface);
    flex-wrap: wrap;
  }

  .stat { text-align: center; }
  .stat-num {
    font-family: 'Orbitron', monospace;
    font-size: 20px;
    font-weight: 700;
    color: var(--accent);
  }
  .stat-label {
    font-size: 11px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  /* RESULT AREA */
  .result-area {
    max-width: 900px;
    margin: 0 auto;
    padding: 24px 20px;
  }

  /* LOADING */
  .loading {
    display: none;
    text-align: center;
    padding: 40px;
  }

  .spinner {
    width: 48px;
    height: 48px;
    border: 3px solid var(--border);
    border-top-color: var(--accent);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
    margin: 0 auto 16px;
  }

  @keyframes spin { to { transform: rotate(360deg); } }

  .loading p {
    color: var(--muted);
    font-size: 13px;
    font-family: 'Orbitron', monospace;
    letter-spacing: 2px;
  }

  /* RESULT CARD */
  .result-card {
    display: none;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
  }

  .result-header {
    background: linear-gradient(135deg, var(--surface), var(--card));
    border-bottom: 1px solid var(--border);
    padding: 20px 24px;
    display: flex;
    align-items: flex-start;
    gap: 16px;
  }

  .car-icon {
    font-size: 40px;
    line-height: 1;
  }

  .car-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(18px, 5vw, 28px);
    font-weight: 900;
    color: var(--accent);
    text-shadow: 0 0 20px var(--glow);
  }

  .car-subtitle {
    font-size: 13px;
    color: var(--muted);
    margin-top: 4px;
  }

  .result-body {
    padding: 20px 24px;
  }

  /* INFO GRID */
  .info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 12px;
    margin-bottom: 20px;
  }

  .info-tile {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px;
  }

  .info-tile-label {
    font-size: 10px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 1.5px;
    margin-bottom: 6px;
  }

  .info-tile-value {
    font-size: 14px;
    font-weight: 600;
    color: var(--text);
  }

  .info-tile-value.highlight {
    color: var(--accent);
    font-family: 'Orbitron', monospace;
  }

  /* SECTIONS */
  .section-title {
    font-family: 'Orbitron', monospace;
    font-size: 12px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 12px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .ai-response {
    font-size: 14px;
    line-height: 1.7;
    color: #c0c0d8;
    white-space: pre-wrap;
  }

  /* PARTS TABLE */
  .parts-section {
    margin-top: 20px;
  }

  .parts-grid {
    display: grid;
    gap: 8px;
  }

  .part-row {
    display: flex;
    align-items: center;
    gap: 12px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 14px;
    font-size: 13px;
  }

  .part-icon { font-size: 18px; min-width: 24px; }
  .part-name { flex: 1; color: var(--text); font-weight: 500; }
  .part-detail { color: var(--muted); font-size: 12px; }

  /* POPULAR MODELS */
  .popular-section {
    padding: 30px 20px;
    max-width: 900px;
    margin: 0 auto;
  }

  .section-header {
    font-family: 'Orbitron', monospace;
    font-size: 14px;
    font-weight: 700;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 16px;
  }

  .brand-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 10px;
  }

  .brand-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 10px;
    text-align: center;
    cursor: pointer;
    transition: all 0.25s;
  }

  .brand-card:hover {
    border-color: var(--accent);
    transform: translateY(-3px);
    box-shadow: 0 8px 24px rgba(232,64,26,0.15);
  }

  .brand-logo { font-size: 28px; margin-bottom: 6px; }
  .brand-name { font-size: 12px; font-weight: 600; color: var(--text); }
  .brand-country { font-size: 10px; color: var(--muted); margin-top: 2px; }

  /* ERROR */
  .error-msg {
    display: none;
    background: rgba(232,64,26,0.1);
    border: 1px solid rgba(232,64,26,0.3);
    border-radius: 10px;
    padding: 16px;
    color: var(--accent2);
    text-align: center;
    font-size: 14px;
  }

  /* FOOTER */
  footer {
    text-align: center;
    padding: 30px 20px;
    color: var(--muted);
    font-size: 12px;
    border-top: 1px solid var(--border);
  }

  footer span { color: var(--accent); }
</style>
</head>
<body>

<header>
  <div class="header-inner">
    <div class="logo">CAR<span>WORLD</span></div>
    <div class="tagline">🌍 Dunyo Mashinalari Ensiklopediyasi</div>
  </div>
</header>

<div class="hero">
  <h1>Dunyo Mashinalari<br>haqida <em>AI</em> ma'lumot</h1>
  <p>Istalgan moshina — kompaniya, ishlab chiqarilgan yil, zapchastlar va ko'proq</p>

  <div class="search-wrap">
    <input class="search-input" id="searchInput" type="text"
      placeholder="Masalan: Toyota Camry 2020, BMW M5, GAZ 21..."
      onkeydown="if(event.key==='Enter') search()">
    <button class="search-btn" id="searchBtn" onclick="search()">IZLA</button>
  </div>

  <div class="quick-tags">
    <div class="tag" onclick="quickSearch('Toyota Corolla')">🇯🇵 Toyota Corolla</div>
    <div class="tag" onclick="quickSearch('BMW 3 Series')">🇩🇪 BMW 3 Series</div>
    <div class="tag" onclick="quickSearch('Tesla Model S')">🇺🇸 Tesla Model S</div>
    <div class="tag" onclick="quickSearch('Chevrolet Cobalt')">🇺🇿 Chevrolet Cobalt</div>
    <div class="tag" onclick="quickSearch('Mercedes-Benz E-Class')">🇩🇪 Mercedes E</div>
    <div class="tag" onclick="quickSearch('Lada Vesta')">🇷🇺 Lada Vesta</div>
  </div>
</div>

<div class="stats-bar">
  <div class="stat">
    <div class="stat-num">500+</div>
    <div class="stat-label">Brend</div>
  </div>
  <div class="stat">
    <div class="stat-num">100+</div>
    <div class="stat-label">Davlat</div>
  </div>
  <div class="stat">
    <div class="stat-num">1886</div>
    <div class="stat-label">Dan buyon</div>
  </div>
  <div class="stat">
    <div class="stat-num">AI</div>
    <div class="stat-label">Powered</div>
  </div>
</div>

<div class="result-area">
  <div class="loading" id="loading">
    <div class="spinner"></div>
    <p>AI IZLAYAPTI...</p>
  </div>

  <div class="error-msg" id="errorMsg">⚠️ Xatolik yuz berdi. Qayta urinib ko'ring.</div>

  <div class="result-card" id="resultCard">
    <div class="result-header">
      <div class="car-icon" id="carIcon">🚗</div>
      <div>
        <div class="car-title" id="carTitle">—</div>
        <div class="car-subtitle" id="carSubtitle">—</div>
      </div>
    </div>
    <div class="result-body">
      <div class="info-grid" id="infoGrid"></div>

      <div class="section-title">🤖 AI TAVSIF</div>
      <div class="ai-response" id="aiDesc">—</div>

      <div class="parts-section">
        <div class="section-title">🔧 ASOSIY ZAPCHASTLAR</div>
        <div class="parts-grid" id="partsGrid"></div>
      </div>
    </div>
  </div>
</div>

<div class="popular-section" id="popularSection">
  <div class="section-header">MASHHUR BRENDLAR</div>
  <div class="brand-grid">
    <div class="brand-card" onclick="quickSearch('Toyota')">
      <div class="brand-logo">🇯🇵</div>
      <div class="brand-name">Toyota</div>
      <div class="brand-country">Yaponiya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('BMW')">
      <div class="brand-logo">🇩🇪</div>
      <div class="brand-name">BMW</div>
      <div class="brand-country">Germaniya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Mercedes-Benz')">
      <div class="brand-logo">🇩🇪</div>
      <div class="brand-name">Mercedes</div>
      <div class="brand-country">Germaniya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Tesla')">
      <div class="brand-logo">🇺🇸</div>
      <div class="brand-name">Tesla</div>
      <div class="brand-country">AQSh</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Honda')">
      <div class="brand-logo">🇯🇵</div>
      <div class="brand-name">Honda</div>
      <div class="brand-country">Yaponiya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Ford')">
      <div class="brand-logo">🇺🇸</div>
      <div class="brand-name">Ford</div>
      <div class="brand-country">AQSh</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Hyundai')">
      <div class="brand-logo">🇰🇷</div>
      <div class="brand-name">Hyundai</div>
      <div class="brand-country">Koreya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Kia')">
      <div class="brand-logo">🇰🇷</div>
      <div class="brand-name">Kia</div>
      <div class="brand-country">Koreya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Audi')">
      <div class="brand-logo">🇩🇪</div>
      <div class="brand-name">Audi</div>
      <div class="brand-country">Germaniya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Chevrolet')">
      <div class="brand-logo">🇺🇸</div>
      <div class="brand-name">Chevrolet</div>
      <div class="brand-country">AQSh / O'zbekiston</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Lada')">
      <div class="brand-logo">🇷🇺</div>
      <div class="brand-name">Lada</div>
      <div class="brand-country">Rossiya</div>
    </div>
    <div class="brand-card" onclick="quickSearch('Volkswagen')">
      <div class="brand-logo">🇩🇪</div>
      <div class="brand-name">Volkswagen</div>
      <div class="brand-country">Germaniya</div>
    </div>
  </div>
</div>

<footer>
  <p>🚗 <span>CarWorld</span> — AI tomonidan quvvatlanadi &nbsp;|&nbsp; Barcha dunyo mashinalari haqida ma'lumot</p>
</footer>

<script>
async function search() {
  const query = document.getElementById('searchInput').value.trim();
  if (!query) return;
  await fetchCarInfo(query);
}

function quickSearch(q) {
  document.getElementById('searchInput').value = q;
  fetchCarInfo(q);
}

function show(id) { document.getElementById(id).style.display = 'block'; }
function hide(id) { document.getElementById(id).style.display = 'none'; }

async function fetchCarInfo(query) {
  const btn = document.getElementById('searchBtn');
  btn.disabled = true;

  hide('resultCard');
  hide('errorMsg');
  hide('popularSection');
  show('loading');

  const prompt = `Siz avtomobil eksperti va ensiklopediya AI siz. Foydalanuvchi "${query}" haqida so'radi.

Quyidagi JSON formatda javob ber (faqat JSON, boshqa matn yo'q):
{
  "name": "Toʻliq nomi (masalan: Toyota Camry 2020)",
  "icon": "mos emoji (🚗 yoki 🏎️ yoki 🚙 yoki 🚕 yoki 🚐 yoki ⚡)",
  "company": "Kompaniya nomi",
  "country": "Ishlab chiqarilgan davlat (bayroq emoji bilan, masalan: 🇯🇵 Yaponiya)",
  "founded": "Kompaniya tashkil yili",
  "year_range": "Ishlab chiqarilgan yillar (masalan: 1982–2024)",
  "type": "Tur (Sedan / SUV / Sport / Elektr / Yuk / Avtobuslar va h.k.)",
  "engine": "Dvigatel (masalan: 2.5L 4-silindrli benzin)",
  "power": "Quvvat (masalan: 203 ot kuchi)",
  "description": "Ushbu avtomobil haqida to'liq o'zbek tilida 4-5 jumlali tavsif: tarixi, xususiyatlari, mashhurlik sababi",
  "parts": [
    {"icon": "🔧", "name": "Moy filtri", "detail": "Har 5,000-10,000 km"},
    {"icon": "🛞", "name": "Shina", "detail": "205/55 R16"},
    {"icon": "🔋", "name": "Akkumulyator", "detail": "60-70 Ah"},
    {"icon": "💨", "name": "Havo filtri", "detail": "Har 15,000 km"},
    {"icon": "🛑", "name": "Tormoz kolodkasi", "detail": "Har 30,000 km"},
    {"icon": "⚙️", "name": "Transmissiya suyuqligi", "detail": "Har 60,000 km"}
  ]
}

Agar aniq model noma'lum bo'lsa, kompaniya haqida umumiy ma'lumot ber. Faqat JSON qaytargin.`;

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-6',
        max_tokens: 1000,
        messages: [{ role: 'user', content: prompt }]
      })
    });

    const data = await response.json();
    const text = data.content.map(i => i.text || '').join('');
    const clean = text.replace(/```json|```/g, '').trim();
    const car = JSON.parse(clean);

    renderResult(car);
  } catch (e) {
    hide('loading');
    show('errorMsg');
    show('popularSection');
  } finally {
    btn.disabled = false;
  }
}

function renderResult(car) {
  hide('loading');

  document.getElementById('carIcon').textContent = car.icon || '🚗';
  document.getElementById('carTitle').textContent = car.name || '—';
  document.getElementById('carSubtitle').textContent = `${car.company} · ${car.country}`;

  const infoData = [
    { label: 'Kompaniya', value: car.company },
    { label: 'Davlat', value: car.country },
    { label: 'Asos solingan', value: car.founded, hl: true },
    { label: 'Ishlab chiqarilgan', value: car.year_range },
    { label: 'Tur', value: car.type },
    { label: 'Dvigatel', value: car.engine },
    { label: 'Quvvat', value: car.power, hl: true },
  ];

  const grid = document.getElementById('infoGrid');
  grid.innerHTML = infoData.filter(d => d.value).map(d => `
    <div class="info-tile">
      <div class="info-tile-label">${d.label}</div>
      <div class="info-tile-value ${d.hl ? 'highlight' : ''}">${d.value}</div>
    </div>
  `).join('');

  document.getElementById('aiDesc').textContent = car.description || '';

  const partsGrid = document.getElementById('partsGrid');
  partsGrid.innerHTML = (car.parts || []).map(p => `
    <div class="part-row">
      <span class="part-icon">${p.icon}</span>
      <span class="part-name">${p.name}</span>
      <span class="part-detail">${p.detail}</span>
    </div>
  `).join('');

  show('resultCard');
}
</script>
</body>
</html>
