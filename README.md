<!DOCTYPE html>
<html lang="ca">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculadora de preus - Oficina de Farmàcia</title>
  <style>
    :root {
      --bg: #f4f7f8;
      --card: #ffffff;
      --ink: #1f2937;
      --muted: #6b7280;
      --line: #d1d5db;
      --primary: #1f7a6d;
      --primary-soft: #dff3ef;
      --accent: #1c64f2;
      --danger: #b42318;
      --warning: #b54708;
      --shadow: 0 10px 25px rgba(15, 23, 42, 0.08);
      --radius: 18px;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      background: linear-gradient(180deg, #eef5f4 0%, var(--bg) 100%);
      color: var(--ink);
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 24px;
    }

    .hero {
      background: linear-gradient(135deg, #e1f3ef, #eef4ff);
      border: 1px solid #d7e6e2;
      border-radius: 24px;
      padding: 28px;
      box-shadow: var(--shadow);
      margin-bottom: 20px;
    }

    .hero h1 {
      margin: 0 0 10px;
      font-size: 2rem;
    }

    .hero p {
      margin: 0;
      color: var(--muted);
      line-height: 1.5;
    }

    .grid {
      display: grid;
      gap: 18px;
    }

    .grid-2 {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .grid-3 {
      grid-template-columns: repeat(3, minmax(0, 1fr));
    }

    .card {
      background: var(--card);
      border: 1px solid #e5e7eb;
      border-radius: var(--radius);
      padding: 22px;
      box-shadow: var(--shadow);
    }

    .card h2, .card h3 {
      margin-top: 0;
      margin-bottom: 12px;
    }

    .muted { color: var(--muted); }
    .small { font-size: 0.92rem; }

    .field {
      display: flex;
      flex-direction: column;
      gap: 8px;
      margin-bottom: 14px;
    }

    label {
      font-weight: 700;
      font-size: 0.95rem;
    }

    input, select, button, textarea {
      font: inherit;
      border-radius: 12px;
      border: 1px solid var(--line);
      padding: 12px 14px;
      background: #fff;
      color: var(--ink);
    }

    input:focus, select:focus, textarea:focus {
      outline: 3px solid rgba(28, 100, 242, 0.15);
      border-color: var(--accent);
    }

    button {
      background: var(--primary);
      color: white;
      border: none;
      cursor: pointer;
      font-weight: 700;
      transition: transform 0.12s ease, opacity 0.12s ease;
    }

    button:hover { opacity: 0.96; }
    button:active { transform: translateY(1px); }

    .secondary-btn {
      background: #eaf2ff;
      color: #153e9f;
      border: 1px solid #c7dafc;
    }

    .tabs {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin: 12px 0 18px;
    }

    .tab-btn {
      background: #edf2f7;
      color: #334155;
      border: 1px solid #dbe3ea;
      padding: 12px 18px;
    }

    .tab-btn.active {
      background: var(--primary);
      color: white;
      border-color: var(--primary);
    }

    .tab-panel { display: none; }
    .tab-panel.active { display: block; }

    .result {
      background: #f8fafc;
      border: 1px solid #e2e8f0;
      border-radius: 16px;
      padding: 16px;
      margin-top: 12px;
      line-height: 1.6;
    }

    .summary-box {
      background: var(--primary-soft);
      border: 1px solid #b5e0d6;
      border-radius: 16px;
      padding: 16px;
    }

    .warning-box {
      background: #fff7ed;
      border: 1px solid #fed7aa;
      color: var(--warning);
      border-radius: 14px;
      padding: 12px 14px;
      margin-top: 12px;
    }

    .danger-box {
      background: #fef3f2;
      border: 1px solid #fecdca;
      color: var(--danger);
      border-radius: 14px;
      padding: 12px 14px;
      margin-top: 12px;
    }

    .inline-actions {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      align-items: center;
    }

    .pill {
      display: inline-block;
      padding: 6px 10px;
      border-radius: 999px;
      background: #eef2ff;
      color: #3730a3;
      font-size: 0.85rem;
      font-weight: 700;
      margin: 2px 6px 2px 0;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }

    th, td {
      text-align: left;
      padding: 10px 8px;
      border-bottom: 1px solid #e5e7eb;
      font-size: 0.95rem;
    }

    .footer-note {
      margin-top: 18px;
      color: var(--muted);
      font-size: 0.9rem;
    }

    @media (max-width: 900px) {
      .grid-2, .grid-3 {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <section class="hero">
      <h1>Calculadora de preus, marges i condicions comercials</h1>
      <p>Recurs didàctic per a alumnat del CFGM de Farmàcia i Parafarmàcia. Inclou classificació inicial pel codi nacional, càlcul de marges, condicions comercials i aplicació d'IVA i recàrrec d'equivalència.</p>
    </section>

    <section class="card">
      <h2>1. Identificació inicial del producte</h2>
      <div class="grid grid-3">
        <div class="field">
          <label for="productName">Nom del producte</label>
          <input id="productName" type="text" placeholder="Ex.: Paracetamol 500 mg" />
        </div>
        <div class="field">
          <label for="nationalCode">Codi nacional</label>
          <input id="nationalCode" type="text" inputmode="numeric" placeholder="Ex.: 712345" />
        </div>
        <div class="field">
          <label>&nbsp;</label>
          <div class="inline-actions">
            <button id="classifyBtn">Classificar producte</button>
            <button id="resetBtn" class="secondary-btn" type="button">Reiniciar</button>
          </div>
        </div>
      </div>

      <div class="grid grid-3">
        <div class="field">
          <label for="category">Categoria detectada</label>
          <input id="category" type="text" readonly />
        </div>
        <div class="field">
          <label for="ivaRate">IVA aplicable (%)</label>
          <select id="ivaRate">
            <option value="4">4%</option>
            <option value="10">10%</option>
            <option value="21" selected>21%</option>
          </select>
        </div>
        <div class="field">
          <label for="reRate">Recàrrec d'equivalència (%)</label>
          <input id="reRate" type="number" min="0" step="0.01" value="5.2" />
        </div>
      </div>

      <div class="inline-actions">
        <span class="pill">IVA i RE es poden modificar manualment</span>
        <button id="syncReBtn" class="secondary-btn" type="button">Restablir RE segons IVA</button>
      </div>

      <div id="classificationResult" class="result">
        Encara no s'ha classificat cap producte. Per defecte, la calculadora treballa amb IVA del 21% i RE del 5,2%.
      </div>
    </section>

    <div class="tabs" aria-label="Pestanyes de càlcul">
      <button class="tab-btn active" data-tab="tab1">1. Marges i cadena de preus</button>
      <button class="tab-btn" data-tab="tab2">2. Condicions comercials</button>
      <button class="tab-btn" data-tab="tab3">3. IVA i RE</button>
    </div>

    <section id="tab1" class="tab-panel active">
      <div class="grid grid-2">
        <article class="card">
          <h2>Cadena PVL → PVM → PVP</h2>
          <p class="muted small">El marge del distribuïdor està configurat per defecte al 7,6% i el de l'oficina de farmàcia al 27,9%, però es poden adaptar per treballar altres supòsits.</p>

          <div class="field">
            <label for="knownPriceType">Preu conegut</label>
            <select id="knownPriceType">
              <option value="PVL">PVL</option>
              <option value="PVM">PVM</option>
              <option value="PVP">PVP</option>
            </select>
          </div>
          <div class="field">
            <label for="knownPriceValue">Import conegut (€)</label>
            <input id="knownPriceValue" type="number" min="0" step="0.01" placeholder="Ex.: 15.00" />
          </div>
          <div class="grid grid-2">
            <div class="field">
              <label for="distMargin">Marge distribuïdor (%)</label>
              <input id="distMargin" type="number" min="0" step="0.01" value="7.6" />
            </div>
            <div class="field">
              <label for="pharmMargin">Marge oficina de farmàcia (%)</label>
              <input id="pharmMargin" type="number" min="0" step="0.01" value="27.9" />
            </div>
          </div>
          <button id="chainBtn">Calcular cadena de preus</button>
          <div id="chainResult" class="result">Introdueix un preu conegut per obtenir la resta de valors.</div>
        </article>

        <article class="card">
          <h2>Marge comercial a partir de cost i preu final</h2>
          <div class="summary-box small">
            Fórmula emprada per al percentatge de marge: <strong>(Preu final − cost) / Preu final × 100</strong>.
          </div>

          <div class="grid grid-2">
            <div>
              <h3>Calcular marge</h3>
              <div class="field">
                <label for="costConcept">Concepte del preu inicial</label>
                <select id="costConcept">
                  <option value="PVL">PVL — Preu de venda de laboratori</option>
                  <option value="PVM" selected>PVM — Preu de venda de magatzem</option>
                  <option value="PVP">PVP — Preu de venda al públic</option>
                </select>
              </div>
              <div class="field">
                <label for="costPrice" id="costPriceLabel">Valor del PVM — Preu de venda de magatzem (€)</label>
                <input id="costPrice" type="number" min="0" step="0.01" />
              </div>
              <div class="field">
                <label for="saleConcept">Concepte del preu final</label>
                <select id="saleConcept">
                  <option value="PVL">PVL — Preu de venda de laboratori</option>
                  <option value="PVM">PVM — Preu de venda de magatzem</option>
                  <option value="PVP" selected>PVP — Preu de venda al públic</option>
                </select>
              </div>
              <div class="field">
                <label for="salePrice" id="salePriceLabel">Valor del PVP — Preu de venda al públic (€)</label>
                <input id="salePrice" type="number" min="0" step="0.01" />
              </div>
              <button id="marginBtn">Calcular marge</button>
              <div id="marginResult" class="result">Aquí veuràs el marge en euros i en percentatge.</div>
            </div>

            <div>
              <h3>Fixar un preu final desitjat</h3>
              <div class="field">
                <label for="targetCostConcept">Concepte del preu inicial</label>
                <select id="targetCostConcept">
                  <option value="PVL">PVL — Preu de venda de laboratori</option>
                  <option value="PVM" selected>PVM — Preu de venda de magatzem</option>
                  <option value="PVP">PVP — Preu de venda al públic</option>
                </select>
              </div>
              <div class="field">
                <label for="costForTarget" id="costForTargetLabel">Valor del PVM — Preu de venda de magatzem (€)</label>
                <input id="costForTarget" type="number" min="0" step="0.01" />
              </div>
              <div class="field">
                <label for="targetSaleConcept">Concepte del preu final</label>
                <select id="targetSaleConcept">
                  <option value="PVL">PVL — Preu de venda de laboratori</option>
                  <option value="PVM">PVM — Preu de venda de magatzem</option>
                  <option value="PVP" selected>PVP — Preu de venda al públic</option>
                </select>
              </div>
              <div class="field">
                <label for="targetMargin">Marge desitjat (%)</label>
                <input id="targetMargin" type="number" min="0" max="99.99" step="0.01" placeholder="Ex.: 30" />
              </div>
              <button id="targetPriceBtn">Calcular preu final</button>
              <div id="targetPriceResult" class="result">Aquí veuràs quin preu final caldria fixar.</div>
            </div>
          </div>
        </article>
      </div>
    </section>

    <section id="tab2" class="tab-panel">
      <div class="grid grid-3">
        <article class="card">
          <h2>Descompte comercial</h2>
          <div class="field">
            <label for="discUnitPrice">Preu unitari base (€)</label>
            <input id="discUnitPrice" type="number" min="0" step="0.01" />
          </div>
          <div class="field">
            <label for="discUnits">Unitats</label>
            <input id="discUnits" type="number" min="1" step="1" value="1" />
          </div>
          <div class="field">
            <label for="discountRate">Descompte (%)</label>
            <input id="discountRate" type="number" min="0" step="0.01" />
          </div>
          <button id="discountBtn">Aplicar descompte</button>
          <div id="discountResult" class="result">Calcula l'import base, el descompte, el subtotal i el total amb IVA + RE.</div>
        </article>

        <article class="card">
          <h2>Bonificació</h2>
          <div class="field">
            <label for="bonusUnitPrice">Preu unitari facturat (€)</label>
            <input id="bonusUnitPrice" type="number" min="0" step="0.01" />
          </div>
          <div class="grid grid-2">
            <div class="field">
              <label for="bonusPaid">Unitats pagades</label>
              <input id="bonusPaid" type="number" min="1" step="1" value="10" />
            </div>
            <div class="field">
              <label for="bonusFree">Unitats bonificades</label>
              <input id="bonusFree" type="number" min="0" step="1" value="2" />
            </div>
          </div>
          <button id="bonusBtn">Calcular bonificació</button>
          <div id="bonusResult" class="result">Veuràs el cost total, les unitats totals rebudes i el cost efectiu per unitat.</div>
        </article>

        <article class="card">
          <h2>Cas combinat: recàrrec i descompte</h2>
          <div class="field">
            <label for="comboUnitPrice">Preu unitari base (€)</label>
            <input id="comboUnitPrice" type="number" min="0" step="0.01" />
          </div>
          <div class="field">
            <label for="comboUnits">Unitats</label>
            <input id="comboUnits" type="number" min="1" step="1" value="1" />
          </div>
          <div class="grid grid-2">
            <div class="field">
              <label for="surchargeRate">Recàrrec comercial (%)</label>
              <input id="surchargeRate" type="number" min="0" step="0.01" value="0" />
            </div>
            <div class="field">
              <label for="comboDiscountRate">Descompte posterior (%)</label>
              <input id="comboDiscountRate" type="number" min="0" step="0.01" value="0" />
            </div>
          </div>
          <button id="comboBtn">Calcular cas combinat</button>
          <div id="comboResult" class="result">Calcula primer el recàrrec, després el descompte i finalment el cost amb IVA + RE.</div>
        </article>
      </div>
    </section>

    <section id="tab3" class="tab-panel">
      <div class="grid grid-2">
        <article class="card">
          <h2>Aplicar IVA i recàrrec d'equivalència</h2>
          <div class="field">
            <label for="taxScenario">Escenari</label>
            <select id="taxScenario">
              <option value="lab">Compra de la farmàcia al laboratori (PVL + IVA + RE)</option>
              <option value="wholesaler">Compra de la farmàcia al majorista (PVM + IVA + RE)</option>
              <option value="public">Venda al públic (PVP + IVA)</option>
            </select>
          </div>
          <div class="field">
            <label for="taxBasePrice">Preu base unitari (€)</label>
            <input id="taxBasePrice" type="number" min="0" step="0.01" />
          </div>
          <div class="field">
            <label for="taxUnits">Unitats</label>
            <input id="taxUnits" type="number" min="1" step="1" value="1" />
          </div>
          <button id="taxBtn">Calcular imposts</button>
          <div id="taxResult" class="result">S'hi mostrarà el desglossament de base, IVA, RE i total.</div>
        </article>

        <article class="card">
          <h2>Paràmetres fiscals actius</h2>
          <div id="activeTaxSummary" class="result">IVA actiu: 21% · RE actiu: 5,2%</div>
          <div class="warning-box small">
            Quan un producte és una excepció, pots modificar manualment l'IVA i el RE a la part superior. La pestanya 3 sempre treballa amb els valors que tinguis actius en aquell moment.
          </div>
          <div class="footer-note">
            Suggeriment didàctic: prova el mateix producte en els tres escenaris per observar que el RE només s'aplica quan la farmàcia compra al laboratori o al majorista.
          </div>
        </article>
      </div>
    </section>

    <p class="footer-note">Aquesta calculadora és un recurs docent. Les fórmules i classificacions s'han preparat a partir del temari del Tema 5 sobre aprovisionament, preus de venda, impostos, marge comercial i condicions comercials.</p>
  </div>

  <script>
    const byId = (id) => document.getElementById(id);

    const state = {
      iva: 21,
      re: 5.2,
      category: '',
      note: ''
    };

    const formatEUR = (value) => {
      if (!Number.isFinite(value)) return '-';
      return new Intl.NumberFormat('ca-ES', { style: 'currency', currency: 'EUR' }).format(value);
    };

    const formatPct = (value) => {
      if (!Number.isFinite(value)) return '-';
      return new Intl.NumberFormat('ca-ES', { minimumFractionDigits: 2, maximumFractionDigits: 2 }).format(value) + '%';
    };

    const n = (value) => Number(String(value).replace(',', '.'));

    function syncReFromIva() {
      const iva = n(byId('ivaRate').value);
      let re = 5.2;
      if (iva === 4) re = 0.5;
      if (iva === 10) re = 1.4;
      if (iva === 21) re = 5.2;
      byId('reRate').value = re;
      syncMarginConceptLabels();
    updateTaxState();
    }

    function updateTaxState() {
      state.iva = n(byId('ivaRate').value) || 0;
      state.re = n(byId('reRate').value) || 0;
      byId('activeTaxSummary').innerHTML = `IVA actiu: <strong>${formatPct(state.iva)}</strong> · RE actiu: <strong>${formatPct(state.re)}</strong>`;
    }

    function classifyNationalCode() {
      const codeRaw = byId('nationalCode').value.trim();
      const code = parseInt(codeRaw.replace(/\D/g, ''), 10);
      const name = byId('productName').value.trim();

      let category = 'Codi no vàlid';
      let iva = 21;
      let re = 5.2;
      let note = 'Introdueix un codi nacional numèric vàlid.';

      if (Number.isFinite(code)) {
        if (code >= 0 && code <= 149999) {
          category = 'Codi intern del proveïdor / producte sense codi nacional';
          iva = 21;
          re = 5.2;
          note = 'Per defecte s\'ha assignat IVA general i RE general. Es pot modificar si el producte és una excepció.';
        } else if (code >= 150000 && code <= 399999) {
          category = 'Parafarmàcia';
          iva = 21;
          re = 5.2;
          note = 'En general, la parafarmàcia treballa amb IVA del 21% i RE del 5,2%.';
        } else if (code >= 400000 && code <= 499999) {
          category = 'Efectes i accessoris finançats';
          iva = 10;
          re = 1.4;
          note = 'Aquest tram pot presentar casos al 10% o al 21%. S\'ha fixat 10% per defecte, però cal revisar si el producte és una excepció.';
        } else if (code >= 500000 && code <= 599999) {
          category = 'Medicaments veterinaris i altres';
          iva = 10;
          re = 1.4;
          note = 'Per defecte: IVA reduït del 10% i RE de l\'1,4%.';
        } else if (code >= 600000 && code <= 650000) {
          category = 'Medicaments en envàs clínic';
          iva = 4;
          re = 0.5;
          note = 'Per defecte: IVA superreduït del 4% i RE del 0,5%.';
        } else if (code >= 650001 && code <= 999999) {
          category = 'Medicaments d\'ús humà';
          iva = 4;
          re = 0.5;
          note = 'Per defecte: IVA superreduït del 4% i RE del 0,5%.';
        } else {
          category = 'Fora dels trams previstos';
          iva = 21;
          re = 5.2;
          note = 'Aquest codi no entra en els trams del recurs docent. Revisa\'l o ajusta manualment IVA i RE.';
        }
      }

      byId('category').value = category;
      byId('ivaRate').value = String(iva);
      byId('reRate').value = re;
      state.category = category;
      state.note = note;
      updateTaxState();

      byId('classificationResult').innerHTML = `
        <strong>Producte:</strong> ${name || 'Sense nom indicat'}<br>
        <strong>Codi nacional:</strong> ${codeRaw || '-'}<br>
        <strong>Categoria detectada:</strong> ${category}<br>
        <strong>IVA proposat:</strong> ${formatPct(iva)} · <strong>RE proposat:</strong> ${formatPct(re)}<br>
        <span class="muted">${note}</span>
      `;
    }

    function calculateChain() {
      const type = byId('knownPriceType').value;
      const value = n(byId('knownPriceValue').value);
      const distMargin = n(byId('distMargin').value) / 100;
      const pharmMargin = n(byId('pharmMargin').value) / 100;

      if (!(value > 0)) {
        byId('chainResult').innerHTML = '<div class="danger-box">Introdueix un import conegut superior a 0.</div>';
        return;
      }
      if (distMargin >= 1 || pharmMargin >= 1) {
        byId('chainResult').innerHTML = '<div class="danger-box">Els marges han de ser inferiors al 100%.</div>';
        return;
      }

      let pvl, pvm, pvp;
      if (type === 'PVL') {
        pvl = value;
        pvm = pvl / (1 - distMargin);
        pvp = pvm / (1 - pharmMargin);
      } else if (type === 'PVM') {
        pvm = value;
        pvl = pvm * (1 - distMargin);
        pvp = pvm / (1 - pharmMargin);
      } else {
        pvp = value;
        pvm = pvp * (1 - pharmMargin);
        pvl = pvm * (1 - distMargin);
      }

      const pvpWithIva = pvp * (1 + state.iva / 100);
      const labToPharmacy = pvl * (1 + state.iva / 100 + state.re / 100);
      const wholesalerToPharmacy = pvm * (1 + state.iva / 100 + state.re / 100);
      const distMarginEuro = pvm - pvl;
      const pharmacyMarginEuro = pvp - pvm;

      byId('chainResult').innerHTML = `
        <table>
          <tr><th>Valor</th><th>Resultat</th></tr>
          <tr><td>PVL</td><td>${formatEUR(pvl)}</td></tr>
          <tr><td>PVM</td><td>${formatEUR(pvm)}</td></tr>
          <tr><td>PVP</td><td>${formatEUR(pvp)}</td></tr>
          <tr><td>PVP + IVA</td><td>${formatEUR(pvpWithIva)}</td></tr>
          <tr><td>Compra farmàcia al laboratori (PVL + IVA + RE)</td><td>${formatEUR(labToPharmacy)}</td></tr>
          <tr><td>Compra farmàcia al majorista (PVM + IVA + RE)</td><td>${formatEUR(wholesalerToPharmacy)}</td></tr>
          <tr><td>Marge del distribuïdor en €</td><td>${formatEUR(distMarginEuro)}</td></tr>
          <tr><td>Marge de l'oficina de farmàcia en €</td><td>${formatEUR(pharmacyMarginEuro)}</td></tr>
        </table>
        <div class="footer-note">Paràmetres fiscals utilitzats: IVA ${formatPct(state.iva)} i RE ${formatPct(state.re)}.</div>
      `;
    }

    function getConceptLabel(selectId) {
      const select = byId(selectId);
      return select.options[select.selectedIndex].text;
    }

    function syncMarginConceptLabels() {
      byId('costPriceLabel').textContent = `Valor del ${getConceptLabel('costConcept')} (€)`;
      byId('salePriceLabel').textContent = `Valor del ${getConceptLabel('saleConcept')} (€)`;
      byId('costForTargetLabel').textContent = `Valor del ${getConceptLabel('targetCostConcept')} (€)`;
    }

    function calculateMargin() {
      const cost = n(byId('costPrice').value);
      const sale = n(byId('salePrice').value);
      const costLabel = getConceptLabel('costConcept');
      const saleLabel = getConceptLabel('saleConcept');
      if (!(cost >= 0) || !(sale > 0) || sale < cost) {
        byId('marginResult').innerHTML = `<div class="danger-box">Introdueix valors vàlids. El ${saleLabel} ha de ser superior o igual al ${costLabel}.</div>`;
        return;
      }
      const marginEuro = sale - cost;
      const marginPct = (marginEuro / sale) * 100;
      byId('marginResult').innerHTML = `
        <strong>${costLabel}:</strong> ${formatEUR(cost)}<br>
        <strong>${saleLabel}:</strong> ${formatEUR(sale)}<br>
        <strong>Marge en euros:</strong> ${formatEUR(marginEuro)}<br>
        <strong>Marge en percentatge:</strong> ${formatPct(marginPct)}
      `;
    }

    function calculateTargetPrice() {
      const cost = n(byId('costForTarget').value);
      const targetMargin = n(byId('targetMargin').value);
      const costLabel = getConceptLabel('targetCostConcept');
      const saleLabel = getConceptLabel('targetSaleConcept');
      if (!(cost >= 0) || !(targetMargin >= 0) || targetMargin >= 100) {
        byId('targetPriceResult').innerHTML = '<div class="danger-box">Introdueix un cost vàlid i un marge entre 0% i 99,99%.</div>';
        return;
      }
      const sale = cost / (1 - targetMargin / 100);
      const marginEuro = sale - cost;
      byId('targetPriceResult').innerHTML = `
        <strong>${costLabel}:</strong> ${formatEUR(cost)}<br>
        <strong>${saleLabel} necessari:</strong> ${formatEUR(sale)}<br>
        <strong>Marge esperat:</strong> ${formatEUR(marginEuro)} (${formatPct(targetMargin)})
      `;
    }

    function taxesFromBase(base, includeRE = true) {
      const ivaAmount = base * state.iva / 100;
      const reAmount = includeRE ? base * state.re / 100 : 0;
      return {
        ivaAmount,
        reAmount,
        total: base + ivaAmount + reAmount
      };
    }

    function calculateDiscount() {
      const unitPrice = n(byId('discUnitPrice').value);
      const units = n(byId('discUnits').value);
      const discountRate = n(byId('discountRate').value);
      if (!(unitPrice >= 0) || !(units > 0) || !(discountRate >= 0)) {
        byId('discountResult').innerHTML = '<div class="danger-box">Revisa preu, unitats i percentatge de descompte.</div>';
        return;
      }
      const base = unitPrice * units;
      const discountAmount = base * discountRate / 100;
      const subtotal = base - discountAmount;
      const tax = taxesFromBase(subtotal, true);
      byId('discountResult').innerHTML = `
        <strong>Import base:</strong> ${formatEUR(base)}<br>
        <strong>Descompte:</strong> -${formatEUR(discountAmount)}<br>
        <strong>Subtotal després del descompte:</strong> ${formatEUR(subtotal)}<br>
        <strong>IVA:</strong> ${formatEUR(tax.ivaAmount)}<br>
        <strong>RE:</strong> ${formatEUR(tax.reAmount)}<br>
        <strong>Total amb IVA + RE:</strong> ${formatEUR(tax.total)}
      `;
    }

    function calculateBonus() {
      const unitPrice = n(byId('bonusUnitPrice').value);
      const paid = n(byId('bonusPaid').value);
      const free = n(byId('bonusFree').value);
      if (!(unitPrice >= 0) || !(paid > 0) || !(free >= 0)) {
        byId('bonusResult').innerHTML = '<div class="danger-box">Revisa preu unitari i unitats.</div>';
        return;
      }
      const totalUnits = paid + free;
      const base = unitPrice * paid;
      const tax = taxesFromBase(base, true);
      const effectiveUnitCostNet = totalUnits > 0 ? base / totalUnits : 0;
      const effectiveUnitCostGross = totalUnits > 0 ? tax.total / totalUnits : 0;
      const bonusPct = totalUnits > 0 ? (free / totalUnits) * 100 : 0;
      byId('bonusResult').innerHTML = `
        <strong>Unitats totals rebudes:</strong> ${totalUnits}<br>
        <strong>Import facturat (sense impostos):</strong> ${formatEUR(base)}<br>
        <strong>Total amb IVA + RE:</strong> ${formatEUR(tax.total)}<br>
        <strong>Cost efectiu per unitat (sense impostos):</strong> ${formatEUR(effectiveUnitCostNet)}<br>
        <strong>Cost efectiu per unitat (amb impostos):</strong> ${formatEUR(effectiveUnitCostGross)}<br>
        <strong>Percentatge de bonificació sobre el total rebut:</strong> ${formatPct(bonusPct)}
      `;
    }

    function calculateCombo() {
      const unitPrice = n(byId('comboUnitPrice').value);
      const units = n(byId('comboUnits').value);
      const surchargeRate = n(byId('surchargeRate').value);
      const discountRate = n(byId('comboDiscountRate').value);
      if (!(unitPrice >= 0) || !(units > 0) || !(surchargeRate >= 0) || !(discountRate >= 0)) {
        byId('comboResult').innerHTML = '<div class="danger-box">Revisa els valors introduïts.</div>';
        return;
      }
      const base = unitPrice * units;
      const surcharge = base * surchargeRate / 100;
      const afterSurcharge = base + surcharge;
      const discount = afterSurcharge * discountRate / 100;
      const subtotal = afterSurcharge - discount;
      const tax = taxesFromBase(subtotal, true);
      byId('comboResult').innerHTML = `
        <strong>Import base:</strong> ${formatEUR(base)}<br>
        <strong>Recàrrec comercial:</strong> +${formatEUR(surcharge)}<br>
        <strong>Import després del recàrrec:</strong> ${formatEUR(afterSurcharge)}<br>
        <strong>Descompte posterior:</strong> -${formatEUR(discount)}<br>
        <strong>Subtotal:</strong> ${formatEUR(subtotal)}<br>
        <strong>Total amb IVA + RE:</strong> ${formatEUR(tax.total)}
      `;
    }

    function calculateTaxes() {
      const scenario = byId('taxScenario').value;
      const unitPrice = n(byId('taxBasePrice').value);
      const units = n(byId('taxUnits').value);
      if (!(unitPrice >= 0) || !(units > 0)) {
        byId('taxResult').innerHTML = '<div class="danger-box">Introdueix un preu base i un nombre d\'unitats vàlids.</div>';
        return;
      }
      const base = unitPrice * units;
      const includeRE = scenario !== 'public';
      const tax = taxesFromBase(base, includeRE);
      const scenarioLabel = {
        lab: 'Compra de la farmàcia al laboratori',
        wholesaler: 'Compra de la farmàcia al majorista',
        public: 'Venda al públic'
      }[scenario];

      byId('taxResult').innerHTML = `
        <strong>Escenari:</strong> ${scenarioLabel}<br>
        <strong>Base imposable:</strong> ${formatEUR(base)}<br>
        <strong>IVA (${formatPct(state.iva)}):</strong> ${formatEUR(tax.ivaAmount)}<br>
        <strong>RE ${includeRE ? '(' + formatPct(state.re) + ')' : '(no s\'aplica)'}:</strong> ${formatEUR(tax.reAmount)}<br>
        <strong>Total final:</strong> ${formatEUR(tax.total)}
      `;
    }

    function resetAll() {
      document.querySelectorAll('input').forEach((input) => {
        if (input.type === 'number') {
          input.value = input.defaultValue || '';
        } else {
          input.value = '';
        }
      });
      byId('ivaRate').value = '21';
      byId('reRate').value = '5.2';
      byId('knownPriceType').value = 'PVL';
      byId('taxScenario').value = 'lab';
      byId('category').value = '';
      byId('classificationResult').textContent = 'Encara no s\'ha classificat cap producte. Per defecte, la calculadora treballa amb IVA del 21% i RE del 5,2%.';
      byId('chainResult').textContent = 'Introdueix un preu conegut per obtenir la resta de valors.';
      byId('marginResult').textContent = 'Aquí veuràs el marge en euros i en percentatge.';
      byId('targetPriceResult').textContent = 'Aquí veuràs quin preu final caldria fixar.';
      byId('discountResult').textContent = 'Calcula l\'import base, el descompte, el subtotal i el total amb IVA + RE.';
      byId('bonusResult').textContent = 'Veuràs el cost total, les unitats totals rebudes i el cost efectiu per unitat.';
      byId('comboResult').textContent = 'Calcula primer el recàrrec, després el descompte i finalment el cost amb IVA + RE.';
      byId('taxResult').textContent = 'S\'hi mostrarà el desglossament de base, IVA, RE i total.';
      updateTaxState();
    }

    document.querySelectorAll('.tab-btn').forEach((btn) => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.tab-btn').forEach((b) => b.classList.remove('active'));
        document.querySelectorAll('.tab-panel').forEach((panel) => panel.classList.remove('active'));
        btn.classList.add('active');
        byId(btn.dataset.tab).classList.add('active');
      });
    });

    byId('classifyBtn').addEventListener('click', classifyNationalCode);
    byId('resetBtn').addEventListener('click', resetAll);
    byId('syncReBtn').addEventListener('click', syncReFromIva);
    byId('ivaRate').addEventListener('change', syncReFromIva);
    byId('reRate').addEventListener('input', updateTaxState);

    byId('chainBtn').addEventListener('click', calculateChain);
    byId('marginBtn').addEventListener('click', calculateMargin);
    byId('targetPriceBtn').addEventListener('click', calculateTargetPrice);
    ['costConcept', 'saleConcept', 'targetCostConcept', 'targetSaleConcept'].forEach(id => byId(id).addEventListener('change', syncMarginConceptLabels));
    byId('discountBtn').addEventListener('click', calculateDiscount);
    byId('bonusBtn').addEventListener('click', calculateBonus);
    byId('comboBtn').addEventListener('click', calculateCombo);
    byId('taxBtn').addEventListener('click', calculateTaxes);

    syncMarginConceptLabels();
    updateTaxState();
  </script>
</body>
</html>
