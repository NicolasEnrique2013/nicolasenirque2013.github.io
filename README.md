# nicolasenirque2013.github.io
En la siguiente web , se mostrara una simulación de e-comerce que es utilizada para un trabajo practico. No se espera lucrar ni alterar ningún video juego.
[e-comerce-de-skins.html](https://github.com/user-attachments/files/29223069/e-comerce-de-skins.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rift Ledger — Demo</title>
<meta name="description" content="Demo simple del mercado de skins entre jugadores: lista de publicaciones y alta de una nueva skin.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;600;700&family=Work+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#12131a;
    --bg-elevated:#1a1c26;
    --bg-elevated-2:#21232f;
    --line:rgba(237,234,226,.12);
    --line-strong:rgba(237,234,226,.22);
    --text:#edeae2;
    --text-muted:#9d9a8e;
    --gold:#e3b23c;
    --gold-dim:#5c4a23;
    --violet:#8a78f0;
    --violet-dim:#332c5c;
    --crimson:#dd5d6c;
    --crimson-dim:#54262d;
    --slate:#9aa0ad;
    --slate-dim:#3a3d45;
    --teal:#4cc9a8;
    --radius:14px;
    --radius-sm:8px;
    --font-display:'Cinzel', serif;
    --font-body:'Work Sans', sans-serif;
    --font-mono:'JetBrains Mono', monospace;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;background:var(--bg);color:var(--text);
    font-family:var(--font-body);line-height:1.5;-webkit-font-smoothing:antialiased;
  }
  button{font-family:inherit;cursor:pointer;}
  .wrap{max-width:1180px;margin:0 auto;padding:0 28px;}

  /* ---------- topbar ---------- */
  .topbar{border-bottom:1px solid var(--line);}
  .topbar-inner{
    max-width:1180px;margin:0 auto;padding:20px 28px;
    display:flex;align-items:center;justify-content:space-between;gap:20px;flex-wrap:wrap;
  }
  .brand-block{display:flex;align-items:center;gap:12px;}
  .brand-mark{
    width:32px;height:32px;border-radius:8px;
    background:linear-gradient(160deg,var(--gold),#a87a1f);
    display:flex;align-items:center;justify-content:center;
    color:#1a1306;font-size:14px;font-weight:700;font-family:var(--font-display);flex:none;
  }
  .brand-text .name{font-family:var(--font-display);font-size:18px;font-weight:600;}
  .brand-text .tag{font-size:12px;color:var(--text-muted);}
  .topbar-actions{display:flex;align-items:center;gap:14px;}
  .btn{
    border:1px solid var(--line-strong);background:transparent;color:var(--text);
    padding:9px 16px;border-radius:999px;font-size:13px;font-weight:600;
    display:inline-flex;align-items:center;gap:6px;transition:border-color .15s, background .15s;
  }
  .btn:hover{border-color:var(--gold);}
  .btn-gold{background:var(--gold);color:#1a1306;border-color:var(--gold);}
  .btn-gold:hover{background:#f0c357;}
  .avatar{
    width:32px;height:32px;border-radius:50%;background:var(--violet-dim);color:var(--violet);
    display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;
    font-family:var(--font-mono);border:1px solid var(--line-strong);flex:none;
  }
  .icon{width:16px;height:16px;flex:none;}

  /* ---------- filters ---------- */
  .filters{
    max-width:1180px;margin:0 auto;padding:28px 28px 0;
    display:flex;flex-wrap:wrap;gap:14px;align-items:center;justify-content:space-between;
  }
  .pill-group{display:flex;flex-wrap:wrap;gap:8px;}
  .pill{
    border:1px solid var(--line-strong);background:var(--bg-elevated);color:var(--text-muted);
    font-size:12.5px;font-weight:600;padding:7px 14px;border-radius:999px;transition:all .15s;
  }
  .pill:hover{color:var(--text);}
  .pill.active{background:var(--text);color:#15161d;border-color:var(--text);}
  .search-box{
    display:flex;align-items:center;gap:8px;background:var(--bg-elevated);
    border:1px solid var(--line-strong);border-radius:999px;padding:8px 14px;min-width:220px;
  }
  .search-box input{background:none;border:none;outline:none;color:var(--text);font-family:var(--font-body);font-size:13.5px;width:100%;}
  .search-box svg{color:var(--text-muted);}

  .results-count{
    max-width:1180px;margin:0 auto;padding:18px 28px 0;
    font-family:var(--font-mono);font-size:12px;color:var(--text-muted);
  }
  .results-count b{color:var(--text);}

  /* ---------- grid / cards ---------- */
  .grid{
    max-width:1180px;margin:0 auto;padding:14px 28px 70px;
    display:grid;grid-template-columns:repeat(3,1fr);gap:20px;
  }
  .card{
    background:var(--bg-elevated);border:1px solid var(--line);border-radius:var(--radius);
    overflow:hidden;display:flex;flex-direction:column;transition:border-color .2s, transform .2s;
  }
  .card:hover{border-color:var(--line-strong);transform:translateY(-2px);}
  .card-art{height:110px;position:relative;display:flex;align-items:center;justify-content:center;border-bottom:1px solid var(--line);}
  .card-art svg{width:32px;height:32px;opacity:.8;}
  .card-id{position:absolute;top:10px;left:12px;font-family:var(--font-mono);font-size:10.5px;color:rgba(255,255,255,.55);letter-spacing:.05em;}
  .rarity-tag{position:absolute;top:10px;right:12px;font-size:10.5px;font-weight:700;letter-spacing:.04em;text-transform:uppercase;padding:3px 9px;border-radius:999px;}
  .r-comun{background:var(--slate-dim);color:var(--slate);}
  .r-epica{background:var(--violet-dim);color:var(--violet);}
  .r-legendaria{background:var(--gold-dim);color:var(--gold);}
  .r-definitiva{background:var(--crimson-dim);color:var(--crimson);}
  .art-comun{background:linear-gradient(150deg,#23262f,#1a1c24);}
  .art-epica{background:linear-gradient(150deg,#2b2547,#1d1a30);}
  .art-legendaria{background:linear-gradient(150deg,#3a3119,#221d10);}
  .art-definitiva{background:linear-gradient(150deg,#3a2229,#22151a);}

  .card-body{padding:16px 18px 18px;display:flex;flex-direction:column;gap:10px;flex:1;}
  .card-title{font-family:var(--font-display);font-size:16px;font-weight:600;line-height:1.3;}
  .card-champ{font-size:12.5px;color:var(--text-muted);margin-top:-6px;}
  .op-tag{font-size:11px;font-weight:700;letter-spacing:.03em;text-transform:uppercase;padding:3px 9px;border-radius:6px;display:inline-block;}
  .op-venta{background:rgba(227,178,60,.14);color:var(--gold);}
  .op-intercambio{background:rgba(76,201,168,.14);color:var(--teal);}
  .op-ambas{background:rgba(138,120,240,.14);color:var(--violet);}
  .card-price{font-family:var(--font-mono);font-size:14px;color:var(--text);margin-top:auto;}
  .card-price small{display:block;font-size:10.5px;color:var(--text-muted);font-family:var(--font-body);margin-bottom:2px;}
  .card-footer{display:flex;align-items:center;justify-content:space-between;border-top:1px solid var(--line);padding-top:12px;margin-top:4px;}
  .seller{display:flex;align-items:center;gap:8px;font-size:12.5px;color:var(--text-muted);}
  .seller .avatar{width:24px;height:24px;font-size:10px;}
  .card-cta{border:none;background:none;color:var(--gold);font-size:12.5px;font-weight:700;display:flex;align-items:center;gap:4px;}
  .card-cta:hover{text-decoration:underline;}

  .empty-state{
    grid-column:1/-1;text-align:center;padding:60px 20px;color:var(--text-muted);
    font-size:14px;border:1px dashed var(--line-strong);border-radius:var(--radius);
  }

  footer{border-top:1px solid var(--line);padding:24px 28px;}
  .footer-inner{max-width:1180px;margin:0 auto;font-size:11.5px;color:var(--text-muted);line-height:1.6;}

  /* ---------- modal ---------- */
  .modal-overlay{position:fixed;inset:0;background:rgba(8,8,11,.7);display:none;align-items:center;justify-content:center;padding:24px;z-index:100;}
  .modal-overlay.open{display:flex;}
  .modal{background:var(--bg-elevated-2);border:1px solid var(--line-strong);border-radius:16px;max-width:520px;width:100%;max-height:88vh;overflow-y:auto;padding:28px;position:relative;}
  .modal-close{position:absolute;top:18px;right:18px;background:none;border:none;color:var(--text-muted);width:30px;height:30px;border-radius:8px;display:flex;align-items:center;justify-content:center;}
  .modal-close:hover{background:var(--line);color:var(--text);}
  .modal h2{font-family:var(--font-display);font-size:19px;font-weight:600;margin:0 0 4px;}
  .modal .sub{font-size:12px;color:var(--text-muted);margin:0 0 22px;font-family:var(--font-mono);}
  .field{margin-bottom:16px;}
  .field label{display:block;font-size:12.5px;font-weight:600;margin-bottom:6px;color:var(--text-muted);}
  .field input, .field select, .field textarea{
    width:100%;background:var(--bg);border:1px solid var(--line-strong);border-radius:var(--radius-sm);
    padding:10px 12px;color:var(--text);font-family:var(--font-body);font-size:13.5px;outline:none;
  }
  .field input:focus, .field select:focus, .field textarea:focus{border-color:var(--gold);}
  .field-row{display:flex;gap:12px;}
  .field-row .field{flex:1;}
  .radio-row{display:flex;gap:10px;flex-wrap:wrap;}
  .radio-pill{border:1px solid var(--line-strong);border-radius:999px;padding:7px 14px;font-size:12.5px;color:var(--text-muted);cursor:pointer;user-select:none;}
  .radio-pill input{display:none;}
  .radio-pill:has(input:checked){background:var(--gold);color:#1a1306;border-color:var(--gold);font-weight:600;}
  .modal-note{font-size:11.5px;color:var(--text-muted);background:var(--bg);border:1px dashed var(--line-strong);border-radius:var(--radius-sm);padding:10px 12px;margin-top:6px;}
  .modal-submit{width:100%;justify-content:center;margin-top:8px;padding:11px;}

  .detail-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin:20px 0;}
  .detail-field{background:var(--bg);border:1px solid var(--line);border-radius:var(--radius-sm);padding:10px 12px;}
  .detail-field span{display:block;font-size:10.5px;color:var(--text-muted);text-transform:uppercase;letter-spacing:.04em;margin-bottom:3px;}
  .detail-field b{font-size:13.5px;font-weight:500;font-family:var(--font-mono);}
  .detail-desc{font-size:13.5px;color:var(--text-muted);line-height:1.7;border-top:1px solid var(--line);padding-top:16px;}

  @media (max-width:920px){ .grid{grid-template-columns:repeat(2,1fr);} }
  @media (max-width:600px){
    .topbar-inner{padding:16px 18px;}
    .filters{padding:20px 18px 0;}
    .results-count{padding:14px 18px 0;}
    .grid{grid-template-columns:1fr;padding:14px 18px 50px;}
    .field-row{flex-direction:column;}
    .detail-grid{grid-template-columns:1fr;}
  }
</style>
</head>
<body>

<header class="topbar">
  <div class="topbar-inner">
    <div class="brand-block">
      <span class="brand-mark">RL</span>
      <div class="brand-text">
        <div class="name">Rift Ledger</div>
        <div class="tag">Mercado de skins entre jugadores</div>
      </div>
    </div>
    <div class="topbar-actions">
      <button class="btn btn-gold" id="openPublish">
        <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg>
        Publicar skin
      </button>
      <div class="avatar">RW</div>
    </div>
  </div>
</header>

<div class="wrap">
  <section class="filters">
    <div class="pill-group" id="rarityFilters">
      <button class="pill active" data-rareza="todas">Todas las rarezas</button>
      <button class="pill" data-rareza="comun">Común</button>
      <button class="pill" data-rareza="epica">Épica</button>
      <button class="pill" data-rareza="legendaria">Legendaria</button>
      <button class="pill" data-rareza="definitiva">Definitiva</button>
    </div>
    <div class="search-box">
      <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="7"/><path d="M21 21l-4.3-4.3"/></svg>
      <input type="text" id="searchInput" placeholder="Buscar por skin o campeón...">
    </div>
  </section>
  <p class="results-count"><b id="countNum">0</b> publicaciones activas</p>
</div>

<main class="grid" id="grid"></main>

<footer>
  <div class="footer-inner">
    Rift Ledger es una maqueta de proyecto académico, sin relación con Riot Games. League of Legends y los nombres de campeones y skins mencionados pertenecen a Riot Games, Inc.
  </div>
</footer>

<!-- ---------- modal: publicar skin ---------- -->
<div class="modal-overlay" id="publishModal">
  <div class="modal">
    <button class="modal-close" data-close>
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6L6 18M6 6l12 12"/></svg>
    </button>
    <h2>Publicar una skin</h2>
    <p class="sub">REGISTRO · PUBLICACION_SKIN</p>
    <form id="publishForm">
      <div class="field-row">
        <div class="field">
          <label for="f-nombre">Nombre de la skin</label>
          <input id="f-nombre" required placeholder="Ej: PROJECT: Ashe">
        </div>
        <div class="field">
          <label for="f-campeon">Campeón</label>
          <input id="f-campeon" required placeholder="Ej: Ashe">
        </div>
      </div>
      <div class="field-row">
        <div class="field">
          <label for="f-rareza">Rareza</label>
          <select id="f-rareza">
            <option value="comun">Común</option>
            <option value="epica">Épica</option>
            <option value="legendaria" selected>Legendaria</option>
            <option value="definitiva">Definitiva</option>
          </select>
        </div>
        <div class="field">
          <label for="f-precio">Precio (RP equivalente)</label>
          <input id="f-precio" type="number" min="0" placeholder="Ej: 1500">
        </div>
      </div>
      <div class="field">
        <label>Tipo de operación</label>
        <div class="radio-row">
          <label class="radio-pill"><input type="radio" name="operacion" value="venta" checked>Venta</label>
          <label class="radio-pill"><input type="radio" name="operacion" value="intercambio">Intercambio</label>
          <label class="radio-pill"><input type="radio" name="operacion" value="ambas">Ambas</label>
        </div>
      </div>
      <div class="field">
        <label for="f-deseada">Skin que buscás a cambio (opcional)</label>
        <input id="f-deseada" placeholder="Ej: Spirit Blossom Yasuo">
      </div>
      <div class="field">
        <label for="f-desc">Descripción</label>
        <textarea id="f-desc" rows="3" placeholder="Comentario libre para quien la vea..."></textarea>
      </div>
      <div class="modal-note">Demo de diseño: al publicar, la skin se agrega a la lista en pantalla pero no se guarda en ningún servidor.</div>
      <button type="submit" class="btn btn-gold modal-submit">Publicar</button>
    </form>
  </div>
</div>

<!-- ---------- modal: detalle de publicación ---------- -->
<div class="modal-overlay" id="detailModal">
  <div class="modal">
    <button class="modal-close" data-close>
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6L6 18M6 6l12 12"/></svg>
    </button>
    <h2 id="d-titulo">—</h2>
    <p class="sub" id="d-sub">—</p>
    <div class="detail-grid" id="d-grid"></div>
    <p class="detail-desc" id="d-desc"></p>
  </div>
</div>

<script>
// ---------- datos de ejemplo (instancias del registro Publicacion_Skin) ----------
let listings = [
  {id:"0301", skin:"Pulsefire Caitlyn", campeon:"Caitlyn", rareza:"legendaria", operacion:"venta", precio:1820, deseada:null, vendedor:"ChronoSniper", estado:"Activa", fecha:"2026-06-02", desc:"Skin en excelente estado, comprada en evento limitado. Entrego con todos los chromas desbloqueados."},
  {id:"0289", skin:"Pool Party Ziggs", campeon:"Ziggs", rareza:"comun", operacion:"venta", precio:350, deseada:null, vendedor:"SummerSplash", estado:"Activa", fecha:"2026-05-30", desc:"Vendo porque ya no juego Ziggs. Precio negociable."},
  {id:"0276", skin:"Blood Moon Aatrox", campeon:"Aatrox", rareza:"epica", operacion:"intercambio", precio:null, deseada:"Blood Moon Diana", vendedor:"EclipseHunter", estado:"Activa", fecha:"2026-05-28", desc:"Busco completar la colección de luna de sangre. Sólo intercambio, no vendo."},
  {id:"0254", skin:"DJ Sona", campeon:"Sona", rareza:"definitiva", operacion:"venta", precio:3250, deseada:null, vendedor:"BeatDrop", estado:"Activa", fecha:"2026-05-25", desc:"Una de las skins más raras del catálogo. Precio fijo, sin intercambios."},
  {id:"0231", skin:"PROJECT: Ashe", campeon:"Ashe", rareza:"legendaria", operacion:"venta", precio:1500, deseada:null, vendedor:"Riftwalker22", estado:"Activa", fecha:"2026-05-22", desc:"Cuenta verificada, skin nunca usada en clasificatoria."},
  {id:"0207", skin:"Elderwood Lissandra", campeon:"Lissandra", rareza:"epica", operacion:"ambas", precio:975, deseada:"Elderwood Nidalee", vendedor:"FrostWeaver", estado:"Activa", fecha:"2026-05-19", desc:"Acepto venta directa o cambio por la skin de bosque añejo de Nidalee."},
  {id:"0198", skin:"Spirit Blossom Vayne", campeon:"Vayne", rareza:"epica", operacion:"intercambio", precio:null, deseada:"Spirit Blossom Yasuo", vendedor:"LunaNocturna", estado:"Activa", fecha:"2026-05-15", desc:"Sólo busco completar el dúo temático. No vendo por RP."},
  {id:"0162", skin:"KDA Akali (Prestige)", campeon:"Akali", rareza:"legendaria", operacion:"intercambio", precio:null, deseada:"Cualquier edición Prestige", vendedor:"PopStarMain", estado:"Activa", fecha:"2026-05-10", desc:"Abierta a cualquier propuesta de edición Prestige, da igual el campeón."},
  {id:"0143", skin:"Arcade Sona", campeon:"Sona", rareza:"epica", operacion:"venta", precio:975, deseada:null, vendedor:"PixelQueen", estado:"Activa", fecha:"2026-05-04", desc:"Skin clásica, ideal para empezar una colección de Sona."}
];

const rarezaLabel = {comun:"Común", epica:"Épica", legendaria:"Legendaria", definitiva:"Definitiva"};
const operacionLabel = {venta:"Venta", intercambio:"Intercambio", ambas:"Venta o intercambio"};
const iconSword = `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M14.5 3.5L21 10l-2 2-6.5-6.5z"/><path d="M3 21l6-6"/><path d="M9 9l6 6"/><path d="M16 12l5 5-2 2-5-5z"/></svg>`;

function buildCard(item){
  const artColor = {comun:"var(--slate)", epica:"var(--violet)", legendaria:"var(--gold)", definitiva:"var(--crimson)"}[item.rareza];
  const priceBlock = item.operacion === "intercambio"
    ? `<small>Busca a cambio</small>${item.deseada}`
    : item.operacion === "ambas"
      ? `<small>Precio o cambio por</small>${item.precio} RP eq. / ${item.deseada}`
      : `<small>Precio</small>${item.precio} RP eq.`;

  return `
  <article class="card" data-rareza="${item.rareza}" data-search="${(item.skin+' '+item.campeon).toLowerCase()}">
    <div class="card-art art-${item.rareza}">
      <span class="card-id">LOTE #${item.id}</span>
      <span class="rarity-tag r-${item.rareza}">${rarezaLabel[item.rareza]}</span>
      <div style="color:${artColor}">${iconSword}</div>
    </div>
    <div class="card-body">
      <div class="card-title">${item.skin}</div>
      <div class="card-champ">${item.campeon}</div>
      <span class="op-tag op-${item.operacion}">${operacionLabel[item.operacion]}</span>
      <div class="card-price">${priceBlock}</div>
      <div class="card-footer">
        <div class="seller">
          <span class="avatar">${item.vendedor.slice(0,2).toUpperCase()}</span>
          ${item.vendedor}
        </div>
        <button class="card-cta" data-id="${item.id}">Ver publicación →</button>
      </div>
    </div>
  </article>`;
}

// ---------- referencias al DOM (todas primero, antes de cualquier llamada) ----------
const grid = document.getElementById('grid');
const countNum = document.getElementById('countNum');
const rarityFilters = document.getElementById('rarityFilters');
const searchInput = document.getElementById('searchInput');
const publishModal = document.getElementById('publishModal');
const detailModal = document.getElementById('detailModal');
let activeRareza = 'todas';

// ---------- funciones (declaradas antes de usarse) ----------
function openModal(modal){ modal.classList.add('open'); }
function closeModal(modal){ modal.classList.remove('open'); }

function applyFilters(){
  const term = searchInput.value.trim().toLowerCase();
  let visible = 0;
  document.querySelectorAll('#grid .card').forEach(card => {
    const matchesRareza = activeRareza === 'todas' || card.dataset.rareza === activeRareza;
    const matchesSearch = !term || card.dataset.search.includes(term);
    const show = matchesRareza && matchesSearch;
    card.style.display = show ? '' : 'none';
    if(show) visible++;
  });
  countNum.textContent = visible;
}

function attachCardEvents(){
  document.querySelectorAll('.card-cta').forEach(btn => {
    btn.addEventListener('click', () => {
      const item = listings.find(l => l.id === btn.dataset.id);
      if(!item) return;
      document.getElementById('d-titulo').textContent = item.skin;
      document.getElementById('d-sub').textContent = `LOTE #${item.id} · PUBLICACION_SKIN`;
      document.getElementById('d-grid').innerHTML = `
        <div class="detail-field"><span>Vendedor</span><b>${item.vendedor}</b></div>
        <div class="detail-field"><span>Campeón</span><b>${item.campeon}</b></div>
        <div class="detail-field"><span>Rareza</span><b>${rarezaLabel[item.rareza]}</b></div>
        <div class="detail-field"><span>Operación</span><b>${operacionLabel[item.operacion]}</b></div>
        <div class="detail-field"><span>Precio</span><b>${item.precio ? item.precio + " RP eq." : "—"}</b></div>
        <div class="detail-field"><span>Skin deseada</span><b>${item.deseada || "—"}</b></div>
        <div class="detail-field"><span>Estado</span><b>${item.estado}</b></div>
        <div class="detail-field"><span>Fecha publicación</span><b>${item.fecha}</b></div>
      `;
      document.getElementById('d-desc').textContent = item.desc;
      openModal(detailModal);
    });
  });
}

function renderGrid(){
  grid.innerHTML = listings.length ? listings.map(buildCard).join('') : '<div class="empty-state">No hay publicaciones que coincidan con el filtro.</div>';
  attachCardEvents();
  applyFilters();
}

// ---------- listeners (se registran antes del primer render) ----------
rarityFilters.addEventListener('click', e => {
  const btn = e.target.closest('.pill');
  if(!btn) return;
  rarityFilters.querySelectorAll('.pill').forEach(p => p.classList.remove('active'));
  btn.classList.add('active');
  activeRareza = btn.dataset.rareza;
  applyFilters();
});
searchInput.addEventListener('input', applyFilters);

document.getElementById('openPublish').addEventListener('click', () => openModal(publishModal));
document.querySelectorAll('.modal-overlay').forEach(overlay => {
  overlay.addEventListener('click', e => { if(e.target === overlay) closeModal(overlay); });
  overlay.querySelector('[data-close]').addEventListener('click', () => closeModal(overlay));
});
document.addEventListener('keydown', e => {
  if(e.key === 'Escape'){ closeModal(publishModal); closeModal(detailModal); }
});

document.getElementById('publishForm').addEventListener('submit', e => {
  e.preventDefault();
  const nombre = document.getElementById('f-nombre').value.trim() || "Skin sin nombre";
  const campeon = document.getElementById('f-campeon').value.trim() || "—";
  const rareza = document.getElementById('f-rareza').value;
  const operacion = document.querySelector('input[name="operacion"]:checked').value;
  const precio = document.getElementById('f-precio').value;
  const deseada = document.getElementById('f-deseada').value.trim();
  const desc = document.getElementById('f-desc').value.trim() || "Sin descripción.";
  const nextId = String(Math.max(...listings.map(l => parseInt(l.id))) + 1).padStart(4,'0');

  listings.unshift({
    id:nextId, skin:nombre, campeon, rareza, operacion,
    precio: precio ? parseInt(precio) : null,
    deseada: deseada || null,
    vendedor:"Vos", estado:"Activa", fecha:new Date().toISOString().slice(0,10),
    desc
  });

  renderGrid();
  closeModal(publishModal);
  e.target.reset();
});

// ---------- primer render (al final, cuando todo ya está declarado) ----------
renderGrid();
</script>

</body>
</html>
