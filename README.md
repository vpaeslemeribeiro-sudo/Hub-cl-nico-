# Hub-cl-nico-
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hub Clínico Pediátrico & Neonatal - UTI e Enfermaria</title>
  <style>
    :root {
      --primary: #1d4ed8;
      --primary-dark: #1e3a8a;
      --primary-light: #3b82f6;
      --teal-primary: #0f766e;
      --purple-primary: #7e22ce;
      --bg: #f8fafc;
      --card-bg: #ffffff;
      --text: #0f172a;
      --text-muted: #64748b;
      --border: #e2e8f0;
      --border-dark: #cbd5e1;
      --success: #16a34a;
      --danger: #dc2626;
      --warning: #d97706;
      --accent-bg: #eff6ff;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
    body { background-color: var(--bg); color: var(--text); min-height: 100vh; display: flex; flex-direction: column; }

    header.hub-header {
      background: linear-gradient(135deg, #1e3a8a, #0f766e);
      color: #fff;
      padding: 16px 24px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 12px rgba(0,0,0,0.12);
      position: sticky;
      top: 0;
      z-index: 1000;
    }
    .hub-title-box { display: flex; align-items: center; gap: 12px; cursor: pointer; }
    .hub-title-box h1 { font-size: 1.25rem; font-weight: 700; letter-spacing: -0.02em; }
    .hub-title-box p { font-size: 0.78rem; color: #cbd5e1; }
    .hub-badge-offline { background: rgba(255,255,255,0.2); border: 1px solid rgba(255,255,255,0.35); padding: 3px 8px; border-radius: 9999px; font-size: 0.7rem; font-weight: 600; text-transform: uppercase; }

    .nav-bar {
      background: #ffffff;
      border-bottom: 1px solid var(--border);
      padding: 8px 16px;
      display: flex;
      gap: 8px;
      overflow-x: auto;
      align-items: center;
    }
    .nav-btn {
      background: transparent;
      border: 1px solid transparent;
      padding: 8px 14px;
      border-radius: 8px;
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--text-muted);
      cursor: pointer;
      white-space: nowrap;
      display: flex;
      align-items: center;
      gap: 6px;
      transition: all 0.2s;
    }
    .nav-btn:hover { background: #f1f5f9; color: var(--text); }
    .nav-btn.active { background: var(--accent-bg); color: var(--primary); border-color: #bfdbfe; }
    .nav-btn.special { color: var(--purple-primary); border-color: #f3e8ff; background: #faf5ff; }

    main.hub-container { flex: 1; max-width: 1200px; width: 100%; margin: 0 auto; padding: 20px 16px; }

    .view-section { display: none; }
    .view-section.active { display: block; animation: fadeIn 0.2s ease-in-out; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(4px); } to { opacity: 1; transform: translateY(0); } }

    .card { background: #fff; border-radius: 12px; border: 1px solid var(--border); box-shadow: 0 2px 8px rgba(0,0,0,0.04); padding: 20px; margin-bottom: 18px; }
    .card h2 { font-size: 1.15rem; color: var(--primary-dark); margin-bottom: 8px; font-weight: 700; }
    .card p.desc { font-size: 0.82rem; color: var(--text-muted); margin-bottom: 16px; }

    .dashboard-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 16px; margin-top: 14px; }
    .tool-tile {
      background: #fff;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 18px;
      cursor: pointer;
      transition: all 0.2s;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      box-shadow: 0 2px 4px rgba(0,0,0,0.02);
    }
    .tool-tile:hover { border-color: var(--primary-light); transform: translateY(-2px); box-shadow: 0 8px 16px rgba(0,0,0,0.06); }
    .tool-cat { font-size: 0.7rem; font-weight: 700; text-transform: uppercase; color: var(--teal-primary); margin-bottom: 4px; }
    .tool-cat.gem { color: var(--purple-primary); }
    .tool-name { font-size: 1.05rem; font-weight: 700; color: #0f172a; margin-bottom: 6px; }
    .tool-desc { font-size: 0.8rem; color: var(--text-muted); line-height: 1.4; margin-bottom: 12px; }
    .tool-action { font-size: 0.8rem; font-weight: 700; color: var(--primary); display: flex; align-items: center; gap: 4px; }

    .grid-2 { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
    .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; }
    .form-group { margin-bottom: 12px; display: flex; flex-direction: column; }
    label { font-size: 0.82rem; font-weight: 600; color: #334155; margin-bottom: 4px; }
    input[type="text"], input[type="number"], select, textarea {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid var(--border-dark);
      border-radius: 6px;
      font-size: 0.92rem;
      background: #fff;
      outline: none;
      transition: border-color 0.2s;
    }
    input:focus, select:focus, textarea:focus { border-color: var(--primary-light); box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.15); }
    input[readonly] { background-color: #f1f5f9; color: #64748b; font-weight: 600; cursor: not-allowed; }

    .btn {
      padding: 10px 16px;
      border-radius: 6px;
      border: none;
      font-weight: 600;
      font-size: 0.88rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: background 0.2s, transform 0.1s;
    }
    .btn:active { transform: scale(0.99); }
    .btn-primary { background: var(--primary); color: #fff; }
    .btn-primary:hover { background: var(--primary-dark); }
    .btn-teal { background: var(--teal-primary); color: #fff; }
    .btn-teal:hover { background: #115e59; }
    .btn-purple { background: var(--purple-primary); color: #fff; }
    .btn-purple:hover { background: #6b21a8; }
    .btn-outline { background: #fff; border: 1px solid var(--border-dark); color: var(--text); }
    .btn-outline:hover { background: #f8fafc; }

    .result-box { background: var(--accent-bg); border: 1px solid #bfdbfe; border-radius: 8px; padding: 16px; margin-top: 14px; }
    .result-box.success { background: #f0fdf4; border-color: #bbf7d0; }
    .result-box.warn { background: #fffbeb; border-color: #fde68a; }
    .alert-box { background: #fef2f2; border-left: 4px solid var(--danger); padding: 12px 14px; border-radius: 6px; font-size: 0.82rem; color: #991b1b; margin-top: 12px; }

    table { width: 100%; border-collapse: collapse; font-size: 0.82rem; }
    th { background: #f1f5f9; color: #334155; padding: 8px 10px; text-align: left; border-bottom: 2px solid var(--border-dark); }
    td { padding: 8px 10px; border-bottom: 1px solid var(--border); }
    tr:nth-child(even) { background: #f8fafc; }

    .toast-popup {
      position: fixed;
      bottom: 24px;
      right: 24px;
      background: #0f172a;
      color: #fff;
      padding: 10px 18px;
      border-radius: 8px;
      font-size: 0.85rem;
      font-weight: 600;
      display: none;
      box-shadow: 0 8px 20px rgba(0,0,0,0.25);
      z-index: 9999;
    }

    @media (max-width: 768px) {
      .grid-2, .grid-3 { grid-template-columns: 1fr; }
      header.hub-header { flex-direction: column; align-items: flex-start; gap: 8px; }
    }
  </style>
</head>
<body>

  <div id="hubToast" class="toast-popup">Copiado para a área de transferência!</div>

  <header class="hub-header">
    <div class="hub-title-box" onclick="navegarPara('dashboard')">
      <div style="font-size: 1.5rem;">🏥</div>
      <div>
        <h1>Central de Ferramentas Clínicas & Gems IA</h1>
        <p>Calculadoras Críticas • Extratores de Laudos • 100% Offline</p>
      </div>
    </div>
    <span class="hub-badge-offline">Modo Offline Pronto</span>
  </header>

  <nav class="nav-bar">
    <button class="nav-btn active" onclick="navegarPara('dashboard')">🏠 Painel</button>
    <button class="nav-btn special" onclick="navegarPara('gems')">✨ Gems & IA</button>
    <button class="nav-btn" onclick="navegarPara('exames')">🔬 Extrator de Exames</button>
    <button class="nav-btn" onclick="navegarPara('pim2')">📈 PIM 2</button>
    <button class="nav-btn" onclick="navegarPara('balanco')">💧 Balanço & SV</button>
    <button class="nav-btn" onclick="navegarPara('intergrowth')">👶 INTERGROWTH</button>
    <button class="nav-btn" onclick="navegarPara('tig')">🧪 TIG & Eletrólitos</button>
    <button class="nav-btn" onclick="navegarPara('cateter')">📏 Cateter Umbilical</button>
    <button class="nav-btn" onclick="navegarPara('diluicao')">💉 Diluição IV</button>
    <button class="nav-btn" onclick="navegarPara('infusao')">⚡ Infusão Contínua</button>
    <button class="nav-btn" onclick="navegarPara('drogas')">💊 Intermitentes</button>
  </nav>

  <main class="hub-container">

    <!-- 0. DASHBOARD -->
    <section id="view-dashboard" class="view-section active">
      <div class="card">
        <h2>Selecione uma Ferramenta de Trabalho</h2>
        <p class="desc">Acesse rapidamente as ferramentas de suporte clínico, assistentes de inteligência artificial e calculadoras pediátricas.</p>
        <div style="margin-bottom: 12px;">
          <input type="text" id="filtroHub" placeholder="🔍 Filtrar por nome ou funcionalidade..." oninput="filtrarCardsHub()">
        </div>

        <div class="dashboard-grid" id="gridCardsHub">
          <div class="tool-tile" onclick="navegarPara('gems')" data-tags="gem gems ia inteligencia artificial extrator laudos documentos">
            <div>
              <div class="tool-cat gem">Google Gems IA</div>
              <div class="tool-name">Meus Gems Clínicos</div>
              <div class="tool-desc">Atalhos rápidos para abrir os seus Gems personalizados no Gemini (Extrator de Exames, Condutas, Artigos).</div>
            </div>
            <div class="tool-action" style="color:var(--purple-primary);">Acessar Gems &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('exames')" data-tags="exames laboratoriais gasometria hemograma bioquimica urina liquor ureia cr eletrolitos laudo prontuario">
            <div>
              <div class="tool-cat gem">IA & Parsing Local Direto</div>
              <div class="tool-name">Extrator Rápido de Exames</div>
              <div class="tool-desc">Extrai qualquer exame em linha única separada por barras (/), sem títulos nem divisões, pronto para o prontuário.</div>
            </div>
            <div class="tool-action" style="color:var(--purple-primary);">Abrir extrator &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('pim2')" data-tags="pim 2 escore utip mortalidade gravidade terapia intensiva slater">
            <div>
              <div class="tool-cat">UTI Pediátrica</div>
              <div class="tool-name">Escore PIM 2</div>
              <div class="tool-desc">Paediatric Index of Mortality 2 canônico (Slater 2003) para admissões nas primeiras horas de UTIP.</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('balanco')" data-tags="balanço hidrico sinais vitais holliday segar diurese uti pam fc fr sat hgt">
            <div>
              <div class="tool-cat">UTI Pediátrica & Neonatal</div>
              <div class="tool-name">Balanço Hídrico & Sinais Vitais</div>
              <div class="tool-desc">Sinais vitais (PAM, FC, FR, SatO₂, Temp, HGT), fórmula de Holliday-Segar, diurese e laudo para prontuário[span_0](start_span)[span_0](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('intergrowth')" data-tags="intergrowth rn recem nascido antropometria peso comprimento perimetro cefalico pig aig gig fenton">
            <div>
              <div class="tool-cat">Neonatologia</div>
              <div class="tool-name">INTERGROWTH-21st (RN)</div>
              <div class="tool-desc">Classificação antropométrica de 33 a 42 semanas (Peso, Comprimento, PC, PIG/AIG/GIG e alerta de RCIU)[span_1](start_span)[span_1](end_span)[span_2](start_span)[span_2](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('tig')" data-tags="tig taxa infusao glicose eletrolitos sodio potassio cloro sbp neonatologia sg5 g50">
            <div>
              <div class="tool-cat">Neonatologia</div>
              <div class="tool-name">TIG & Eletrólitos Neonatais (SBP)</div>
              <div class="tool-desc">Cálculo de taxa de infusão de glicose (SG 5% + G 50%) e balanço de Na⁺, K⁺ e Cl⁻ conforme diretrizes SBP[span_3](start_span)[span_3](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('cateter')" data-tags="cateterismo umbilical venoso arterial alto baixo ombro umbigo pop neonatologia">
            <div>
              <div class="tool-cat">Neonatologia</div>
              <div class="tool-name">Cateterismo Umbilical</div>
              <div class="tool-desc">Estimativas de inserção para Cateter Venoso e Arterial (Alto e Baixo) por Peso e distância Ombro-Umbigo (POP-PB)[span_4](start_span)[span_4](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('diluicao')" data-tags="diluicao intravenosa antibioticos sedativos estabilidade reconstituicao ampicilina ceftriaxona vancomicina">
            <div>
              <div class="tool-cat">Farmacologia Clínica</div>
              <div class="tool-name">Guia & Diluição IV (55+ Drogas)</div>
              <div class="tool-desc">Concentração usual, volume mínimo de restrição hídrica, reconstituição, estabilidade e infusão segura[span_5](start_span)[span_5](end_span)[span_6](start_span)[span_6](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('infusao')" data-tags="infusao continua vasoativos adrenalina noradrenalina dobutamina fentanil midazolam precedex vazao bomba">
            <div>
              <div class="tool-cat">Farmacologia & UTI</div>
              <div class="tool-name">Dose de Infusão Contínua</div>
              <div class="tool-desc">Conversão automática para mcg/kg/min, mcg/kg/h e mg/kg/h a partir de vazão (mL/h) e diluição personalizada[span_7](start_span)[span_7](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>

          <div class="tool-tile" onclick="navegarPara('drogas')" data-tags="doses intermitentes ampicilina cefazolina dipirona furosemida meropenem ajuste neonatal prontuario">
            <div>
              <div class="tool-cat">Prescrição Pediátrica</div>
              <div class="tool-name">Doses Intermitentes & Prescrição</div>
              <div class="tool-desc">Doses por peso com checagem de limite máximo absoluto, ajuste neonatal de prematuridade e gerador de texto[span_8](start_span)[span_8](end_span).</div>
            </div>
            <div class="tool-action">Abrir calculadora &rarr;</div>
          </div>
        </div>
      </div>
    </section>

    <!-- SECÇÃO ESPECIAL: GEMS IA -->
    <section id="view-gems" class="view-section">
      <div class="card">
        <h2>✨ Meus Gems Clínicos (Gemini)</h2>
        <p class="desc">Acesso direto aos seus assistentes personalizados criados no Gemini para tarefas complexas com fotos, PDFs e textos de laudos.</p>

        <div class="grid-2">
          <div style="background:#faf5ff; border:1px solid #e9d5ff; border-radius:10px; padding:16px;">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
              <span style="font-size:0.75rem; font-weight:700; color:var(--purple-primary); text-transform:uppercase;">Gem Especializado</span>
              <span style="font-size:1.2rem;">🔬</span>
            </div>
            <h3 style="color:#581c87; font-size:1.05rem; margin-bottom:6px;">Extrator de Exames Clínicos</h3>
            <p style="font-size:0.8rem; color:#6b21a8; line-height:1.4; margin-bottom:12px;">
              Envia fotografias de laudos impressos, telas de prontuários eletrônicos ou arquivos PDF para transcrição e estruturação automática de parâmetros clínicos.
            </p>
            <div style="display:flex; gap:8px;">
              <a href="https://gemini.google.com" target="_blank" class="btn btn-purple" style="font-size:0.8rem; text-decoration:none;">Abrir Gem no Gemini ↗</a>
              <button class="btn btn-outline" style="font-size:0.8rem;" onclick="navegarPara('exames')">Usar Leitor Local (Offline)</button>
            </div>
          </div>

          <div style="background:#f8fafc; border:1px solid var(--border); border-radius:10px; padding:16px;">
            <div style="font-weight:700; font-size:0.88rem; color:#1e293b; margin-bottom:6px;">🔗 Como ligar o link direto do seu Gem:</div>
            <p style="font-size:0.8rem; color:var(--text-muted); line-height:1.4; margin-bottom:8px;">
              Cole o link exato do seu Gem criado no Gemini para abrir com 1 clique:
            </p>
            <input type="text" id="linkGemCustom" placeholder="https://gemini.google.com/gem/..." style="margin-bottom:8px; font-size:0.8rem;">
            <button class="btn btn-outline" style="font-size:0.8rem; width:100%;" onclick="salvarLinkGem()">Salvar Atalho Pessoal</button>
          </div>
        </div>
      </div>
    </section>

    <!-- SECÇÃO EXTRATOR DE EXAMES DIRETO (SEM SUB-TITULOS) -->
    <section id="view-exames" class="view-section">
      <div class="card">
        <div style="display:flex; justify-content:space-between; align-items:flex-start; flex-wrap:wrap; gap:8px; margin-bottom:6px;">
          <div>
            <h2>🔬 Extrator Direto de Exames</h2>
            <p class="desc" style="margin-bottom:0;">Cole o texto do laudo para gerar diretamente a linha única com barras (/), sem subdivisões ou títulos desnecessários.</p>
          </div>
          <button class="btn btn-outline" onclick="zerarExtratorExames()">🔄 Limpar / Novo Exame</button>
        </div>

        <div class="form-group" style="margin-top:12px;">
          <label for="textoLaudoBruto">Cole aqui o texto bruto dos exames:</label>
          <textarea id="textoLaudoBruto" rows="6" placeholder="Cole qualquer laudo ou texto aqui..."></textarea>
        </div>

        <div style="display:flex; gap:8px; flex-wrap:wrap;">
          <button class="btn btn-purple" onclick="processarExamesLocais()">⚡ Extrair em Linha Única</button>
          <button class="btn btn-outline" onclick="zerarExtratorExames()">🔄 Limpar</button>
        </div>

        <div id="resultadoExamesContainer" style="display:none; margin-top:18px;">
          <div class="result-box" style="margin-top:0; background:#f5f3ff; border-color:#ddd6fe;">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:6px;">
              <span style="font-weight:700; font-size:0.88rem; color:#5b21b6;">Resultado Extraído (Linha Direta):</span>
              <button class="btn btn-purple" style="padding:6px 12px; font-size:0.8rem;" onclick="copiarTexto('textoLinhaContinuaExames')">📋 Copiar Linha</button>
            </div>
            <textarea id="textoLinhaContinuaExames" rows="5" readonly style="font-family: monospace; font-size: 0.9rem; background:#fff; font-weight:600; color:#1e1b4b; line-height:1.5;"></textarea>
          </div>
        </div>
      </div>
    </section>

    <!-- 1. ESCORE PIM 2 -->
    <section id="view-pim2" class="view-section">
      <div class="card">
        <h2>Calculadora PIM 2 (Paediatric Index of Mortality 2)</h2>
        <p class="desc">Referência: Slater A, Shann F, Pearson G; Paediatric Index of Mortality (PIM) Study Group. Intensive Care Med. 2003.</p>

        <div class="grid-2">
          <div class="form-group">
            <label for="p2_sbp">Pressão Arterial Sistólica (PAS em mmHg)</label>
            <input type="number" id="p2_sbp" value="120" placeholder="120 se desconhecida ou parada" oninput="calcularPim2()">
            <span style="font-size:0.75rem; color:var(--text-muted);">0 em PCR; 30 se choque não mensurável; 120 se normal/não aferida.</span>
          </div>

          <div class="form-group">
            <label for="p2_pupils">Reação Pupilar à Luz Forte</label>
            <select id="p2_pupils" onchange="calcularPim2()">
              <option value="0">Normal / Desconhecida / Apenas 1 fixa (0)</option>
              <option value="1">Ambas fixas e &gt; 3 mm (+3.0791)</option>
            </select>
          </div>

          <div class="form-group">
            <label for="p2_pao2">PaO₂ (mmHg)</label>
            <input type="number" id="p2_pao2" value="0" placeholder="0 se não colhida" oninput="calcularPim2()">
          </div>

          <div class="form-group">
            <label for="p2_fio2">FiO₂ no momento da gasometria (%)</label>
            <input type="number" id="p2_fio2" value="21" min="21" max="100" oninput="calcularPim2()">
            <span style="font-size:0.75rem; color:var(--text-muted);">Se O₂ em TOT ou halo/tenda. Se PaO₂=0, razão é zerada.</span>
          </div>

          <div class="form-group">
            <label for="p2_be">Base Excess (mmol/L)</label>
            <input type="number" id="p2_be" value="0" step="0.1" placeholder="0 se desconhecido" oninput="calcularPim2()">
            <span style="font-size:0.75rem; color:var(--text-muted);">Sangue arterial ou capilar (usa |BE|).</span>
          </div>

          <div class="form-group">
            <label for="p2_vent">Ventilação Mecânica na 1ª hora na UTIP</label>
            <select id="p2_vent" onchange="calcularPim2()">
              <option value="0">Não (0)</option>
              <option value="1">Sim - Invasiva, CPAP ou BiPAP (+1.3352)</option>
            </select>
          </div>

          <div class="form-group">
            <label for="p2_elective">Admissão Eletiva na UTIP</label>
            <select id="p2_elective" onchange="calcularPim2()">
              <option value="0">Não (0)</option>
              <option value="1">Sim (-0.9282)</option>
            </select>
          </div>

          <div class="form-group">
            <label for="p2_surgery">Motivo principal é recuperação pós-cirúrgica</label>
            <select id="p2_surgery" onchange="calcularPim2()">
              <option value="0">Não (0)</option>
              <option value="1">Sim (-1.0244)</option>
            </select>
          </div>

          <div class="form-group">
            <label for="p2_bypass">Admitido pós-cirurgia com bypass cardíaco</label>
            <select id="p2_bypass" onchange="calcularPim2()">
              <option value="0">Não (0)</option>
              <option value="1">Sim (-0.3882)</option>
            </select>
          </div>

          <div class="form-group">
            <label for="p2_highrisk">Diagnóstico de Alto Risco</label>
            <select id="p2_highrisk" onchange="calcularPim2()">
              <option value="0">Nenhum (0)</option>
              <option value="1">PCR prévia à admissão (+1.6696)</option>
              <option value="2">Imunodeficiência combinada grave (+1.6696)</option>
              <option value="3">Leucemia/Linfoma pós-1ª indução (+1.6696)</option>
              <option value="4">Hemorragia cerebral espontânea (+1.6696)</option>
              <option value="5">Miocardiopatia ou miocardite (+1.6696)</option>
              <option value="6">Síndrome do coração esquerdo hipoplásico (+1.6696)</option>
              <option value="7">Infecção por HIV (+1.6696)</option>
              <option value="8">Insuficiência hepática como motivo principal (+1.6696)</option>
              <option value="9">Doença neurodegenerativa progressiva (+1.6696)</option>
            </select>
          </div>

          <div class="form-group full-width">
            <label for="p2_lowrisk">Diagnóstico de Baixo Risco</label>
            <select id="p2_lowrisk" onchange="calcularPim2()">
              <option value="0">Nenhum (0)</option>
              <option value="1">Asma como motivo principal (-1.5883)</option>
              <option value="2">Bronquiolite como motivo principal (-1.5883)</option>
              <option value="3">Crupe como motivo principal (-1.5883)</option>
              <option value="4">Apneia obstrutiva do sono pós-adenoamigdalectomia (-1.5883)</option>
              <option value="5">Cetoacidose diabética como motivo principal (-1.5883)</option>
            </select>
          </div>
        </div>

        <div class="result-box" id="p2_resultBox">
          <div style="display: flex; justify-content: space-between; align-items: baseline; flex-wrap: wrap;">
            <div>
              <div style="font-size:0.8rem; color:var(--text-muted); font-weight:600; text-transform:uppercase;">Risco Estimado de Mortalidade (PIM 2)</div>
              <div id="p2_resMortality" style="font-size:2.2rem; font-weight:800; color:var(--primary);">1.2%</div>
            </div>
            <div style="font-size: 0.9rem; color: #475569;">
              Logit Calculado: <strong id="p2_resLogit">-4.392</strong>
            </div>
          </div>
          <div style="margin-top: 14px;">
            <button class="btn btn-primary" onclick="copiarLaudoPim2()">📋 Copiar Laudo do PIM 2</button>
          </div>
        </div>
      </div>
    </section>

    <!-- 2. BALANÇO HÍDRICO & SINAIS VITAIS -->
    <section id="view-balanco" class="view-section">
      <div class="card">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px; flex-wrap:wrap; gap:8px;">
          <div>
            <h2>Balanço Hídrico & Sinais Vitais (UTIP & Neonatologia)</h2>
            <p class="desc" style="margin-bottom:0;">Sequência padrão de sinais vitais, cálculo de Holliday-Segar e balanço acumulado[span_9](start_span)[span_9](end_span).</p>
          </div>
          <button class="btn btn-outline" onclick="zerarCamposBH()">🔄 Limpar Tudo[span_10](start_span)[span_10](end_span)</button>
        </div>

        <div class="form-group">
          <label style="color:var(--primary); font-size:0.95rem;">1. Sinais Vitais (Mínimo e Máximo separados por espaço ou hífen)[span_11](start_span)[span_11](end_span)</label>
          <div class="grid-3" style="margin-top: 6px;">
            <div class="form-group"><label>1. PAM (mmHg)</label><input type="text" id="bh_pam" placeholder="Ex: 70 76" oninput="calcularBH()"></div>
            <div class="form-group"><label>2. FC (bpm)</label><input type="text" id="bh_fc" placeholder="Ex: 95 130" oninput="calcularBH()"></div>
            <div class="form-group"><label>3. FR (irpm)</label><input type="text" id="bh_fr" placeholder="Ex: 22 40" oninput="calcularBH()"></div>
            <div class="form-group"><label>4. SatO₂ (%)</label><input type="text" id="bh_sat" placeholder="Ex: 92 98" oninput="calcularBH()"></div>
            <div class="form-group"><label>5. Temp (ºC)</label><input type="text" id="bh_temp" placeholder="Ex: 36.5 37.2" oninput="calcularBH()"></div>
            <div class="form-group"><label>6. HGT (mg/dL)</label><input type="text" id="bh_hgt" placeholder="Ex: 85 110" oninput="calcularBH()"></div>
          </div>
        </div>

        <div class="form-group" style="margin-top: 10px;">
          <label style="color:var(--primary); font-size:0.95rem;">2. Dados do Paciente e Intervalo[span_12](start_span)[span_12](end_span)</label>
          <div class="grid-3" style="margin-top:6px;">
            <div class="form-group">
              <label>Peso Corporal (kg)</label>
              <input type="number" id="bh_peso" step="any" placeholder="Ex: 12.5" oninput="calcularBH()">
            </div>
            <div class="form-group">
              <label>Peso Calórico (Holliday-Segar)</label>
              <input type="text" id="bh_pesoCal" readonly placeholder="Auto para > 10 kg">
            </div>
            <div class="form-group">
              <label>Período de Balanço</label>
              <select id="bh_horas" onchange="calcularBH()">
                <option value="24" selected>24 Horas</option>
                <option value="12">12 Horas</option>
                <option value="6">6 Horas</option>
              </select>
            </div>
          </div>
        </div>

        <div class="grid-2" style="margin-top: 10px;">
          <div style="background:#f8fafc; padding:12px; border-radius:8px; border:1px solid var(--border);">
            <div style="font-weight:700; font-size:0.85rem; color:#1e3a8a; margin-bottom:8px;">📥 Entradas (mL) — [Enter acumula][span_13](start_span)[span_13](end_span)</div>
            <div class="form-group">
              <label>Volume Endovenoso (EV)</label>
              <input type="text" id="bh_ev" placeholder="0" onkeydown="handleBhKey(event, this)">
            </div>
            <div class="form-group">
              <label>Oral / SNG / SNE</label>
              <input type="text" id="bh_vo" placeholder="0" onkeydown="handleBhKey(event, this)">
            </div>
          </div>

          <div style="background:#f8fafc; padding:12px; border-radius:8px; border:1px solid var(--border);">
            <div style="font-weight:700; font-size:0.85rem; color:#991b1b; margin-bottom:8px;">📤 Saídas / Perdas (mL) — [Enter acumula][span_14](start_span)[span_14](end_span)</div>
            <div class="form-group">
              <label>Diurese (mL)</label>
              <input type="text" id="bh_diurese" placeholder="0" onkeydown="handleBhKey(event, this)">
            </div>
            <div class="form-group">
              <label>Drenos (mL)</label>
              <input type="text" id="bh_drenos" placeholder="0" onkeydown="handleBhKey(event, this)">
            </div>
            <div class="form-group">
              <label>Vômitos / Outras Perdas (mL)</label>
              <input type="text" id="bh_vomitos" placeholder="0" onkeydown="handleBhKey(event, this)">
            </div>
          </div>
        </div>

        <div class="result-box" style="margin-top: 16px;">
          <div style="display:flex; justify-content:space-between; align-items:center;">
            <div>
              <div style="font-size:0.8rem; text-transform:uppercase; color:var(--text-muted); font-weight:600;">Balanço Hídrico Acumulado[span_15](start_span)[span_15](end_span)</div>
              <div id="bh_displayVal" style="font-size:1.8rem; font-weight:800; color:var(--text);">0,0 mL</div>
            </div>
            <div id="bh_taxaDiurese" style="font-size:0.95rem; font-weight:600; color:var(--text-muted); text-align:right;">Diurese: -- mL/kg/h</div>
          </div>

          <div style="margin-top: 14px;">
            <label>Texto formatado para cópia no prontuário:</label>
            <textarea id="bh_textoProntuario" rows="7" readonly style="font-family: monospace; font-size: 0.82rem; margin-top: 4px;"></textarea>
            <button class="btn btn-primary" style="margin-top: 8px; width: 100%;" onclick="copiarProntuarioBH()">📋 Copiar para Prontuário[span_16](start_span)[span_16](end_span)</button>
          </div>
        </div>
      </div>
    </section>

    <!-- 3. INTERGROWTH-21st (RN) -->
    <section id="view-intergrowth" class="view-section">
      <div class="card">
        <h2>Classificação Antropométrica do Recém-Nascido</h2>
        <p class="desc">Padrões INTERGROWTH-21st (Villar et al., Lancet 2014) — Validação para 33+0 a 42+6 semanas de IG[span_17](start_span)[span_17](end_span)[span_18](start_span)[span_18](end_span).</p>

        <div class="grid-2">
          <div class="form-group">
            <label>Sexo do Neonato</label>
            <select id="ig_sexo" onchange="calcularIntergrowth()">
              <option value="M">Masculino[span_19](start_span)[span_19](end_span)[span_20](start_span)[span_20](end_span)</option>
              <option value="F">Feminino[span_21](start_span)[span_21](end_span)[span_22](start_span)[span_22](end_span)</option>
            </select>
          </div>

          <div class="form-group">
            <label>Idade Gestacional (Semanas + Dias)</label>
            <div style="display: flex; gap: 8px; align-items: center;">
              <input type="number" id="ig_sem" min="20" max="45" value="38" style="width: 50%;" oninput="calcularIntergrowth()">
              <span>sem +</span>
              <input type="number" id="ig_dias" min="0" max="6" value="0" style="width: 50%;" oninput="calcularIntergrowth()">
              <span>d</span>
            </div>
          </div>
        </div>

        <div class="grid-3" style="margin-top: 6px;">
          <div class="form-group">
            <label>Peso de Nascimento (g)</label>
            <input type="number" id="ig_peso" placeholder="Ex: 3150" oninput="calcularIntergrowth()">
          </div>
          <div class="form-group">
            <label>Comprimento (cm)</label>
            <input type="number" id="ig_comp" step="0.1" placeholder="Ex: 49.0" oninput="calcularIntergrowth()">
          </div>
          <div class="form-group">
            <label>Perímetro Cefálico (cm)</label>
            <input type="number" id="ig_pc" step="0.1" placeholder="Ex: 34.5" oninput="calcularIntergrowth()">
          </div>
        </div>

        <div id="ig_resultadoContainer" style="display: none; margin-top: 14px;">
          <div id="ig_gaBanner" class="result-box" style="margin-bottom: 12px; background: #f8fafc; border-color: #cbd5e1;"></div>
          <div id="ig_cardsList" style="display: flex; flex-direction: column; gap: 10px;"></div>
          <div id="ig_iugrBox" style="margin-top: 12px;"></div>
          
          <div class="result-box" style="margin-top: 14px;">
            <div style="font-weight: 700; margin-bottom: 6px; font-size: 0.9rem;">Laudo Antropométrico do RN</div>
            <textarea id="ig_resumoTexto" rows="6" readonly style="font-family: monospace; font-size: 0.82rem;"></textarea>
            <button class="btn btn-teal" style="margin-top: 8px; width: 100%;" onclick="copiarTexto('ig_resumoTexto')">📋 Copiar Laudo do Neonato</button>
          </div>
        </div>
      </div>
    </section>

    <!-- 4. TIG & ELETRÓLITOS NEONATAIS -->
    <section id="view-tig" class="view-section">
      <div class="card">
        <h2>Calculadora de TIG e Eletrólitos Neonatais (SBP)</h2>
        <p class="desc">Taxa de infusão de glicose com Roseta de SG 5% + G 50% e balanço eletrolítico conforme peso e dia de vida[span_23](start_span)[span_23](end_span).</p>

        <div class="grid-2">
          <div class="form-group">
            <label for="tig_peso">Peso do Recém-Nascido (kg)</label>
            <input type="number" id="tig_peso" step="0.001" placeholder="Ex: 1.350" oninput="calcularTig()">
          </div>
          <div class="form-group">
            <label for="tig_dia">Idade / Dia de Vida</label>
            <select id="tig_dia" onchange="calcularTig()">
              <option value="1">1º dia (Fase 1)[span_24](start_span)[span_24](end_span)</option>
              <option value="2">2º dia (Fase 1)[span_25](start_span)[span_25](end_span)</option>
              <option value="3">3º dia (Fase 1)[span_26](start_span)[span_26](end_span)</option>
              <option value="4">4º dia (Fase 1)[span_27](start_span)[span_27](end_span)</option>
              <option value="5">5º dia (Fase 1)[span_28](start_span)[span_28](end_span)</option>
              <option value="6">Fase 2 (&gt; 5 dias de vida)[span_29](start_span)[span_29](end_span)</option>
            </select>
          </div>
        </div>

        <div class="grid-2">
          <div class="form-group">
            <label for="tig_desejada">TIG Desejada (mg/kg/min)</label>
            <input type="number" id="tig_desejada" step="0.1" value="4.0" oninput="calcularTig()">
          </div>
          <div class="form-group">
            <label for="tig_tipo">Perfil Neonatal</label>
            <select id="tig_tipo" onchange="calcularTig()">
              <option value="auto">Prematuro / Baseado no Peso[span_30](start_span)[span_30](end_span)</option>
              <option value="termo">Recém-Nascido a Termo[span_31](start_span)[span_31](end_span)</option>
            </select>
          </div>
        </div>

        <div style="background:#f1f5f9; padding:12px; border-radius:8px; margin: 8px 0;">
          <div id="tig_sugestaoSBP" style="font-size:0.8rem; color:#475569; margin-bottom:8px;">💡 Sugestão SBP para este perfil: --</div>
          <div class="grid-2">
            <div class="form-group">
              <label for="tig_taxaHidrica">Taxa Hídrica Alvo (mL/kg/dia)</label>
              <input type="number" id="tig_taxaHidrica" value="80" oninput="atualizarTigPorTaxa()">
            </div>
            <div class="form-group">
              <label for="tig_volTotal">Volume Total (mL/24h)</label>
              <input type="number" id="tig_volTotal" placeholder="Automático" oninput="calcularTig(true)">
            </div>
          </div>
        </div>

        <div class="grid-2" style="margin-top: 14px;">
          <div class="result-box" style="margin-top:0;">
            <div style="font-weight:700; color:var(--primary); margin-bottom:8px; font-size:0.9rem;">💧 Solução Glicosada (24 horas)[span_32](start_span)[span_32](end_span)</div>
            <div style="display:flex; justify-content:space-between; margin-bottom:4px; font-size:0.88rem;">
              <span>Soro Glicosado 5%:</span><strong id="tig_resSg5">0.0 mL</strong>
            </div>
            <div style="display:flex; justify-content:space-between; margin-bottom:4px; font-size:0.88rem;">
              <span>Glicose 50%:</span><strong id="tig_resG50">0.0 mL</strong>
            </div>
            <div style="border-top:1px dashed #cbd5e1; margin:8px 0;"></div>
            <div style="display:flex; justify-content:space-between; font-size:0.8rem; color:var(--text-muted);">
              <span>Volume Total:</span><span id="tig_resVt">0.0 mL</span>
            </div>
            <div style="display:flex; justify-content:space-between; font-size:0.8rem; color:var(--text-muted);">
              <span>Concentração Final:</span><span id="tig_resCg">0.0 %</span>
            </div>
          </div>

          <div class="result-box success" style="margin-top:0;">
            <div style="font-weight:700; color:var(--success); margin-bottom:8px; font-size:0.9rem;">🧪 Balanço de Eletrólitos (24h)[span_33](start_span)[span_33](end_span)</div>
            <div style="font-size:0.82rem; margin-bottom:6px;">
              <strong>Sódio (Na⁺):</strong> <span id="tig_alvoNa">0.0 mmol/kg</span> &rarr; <strong id="tig_absNa">0.0 mmol</strong>
            </div>
            <div style="font-size:0.82rem; margin-bottom:6px;">
              <strong>Potássio (K⁺):</strong> <span id="tig_alvoK">0.0 mmol/kg</span> &rarr; <strong id="tig_absK">0.0 mmol</strong>
            </div>
            <div style="font-size:0.82rem;">
              <strong>Cloro (Cl⁻):</strong> <span id="tig_alvoCl">0.0 mmol/kg</span> &rarr; <strong id="tig_absCl">0.0 mmol</strong>
            </div>
          </div>
        </div>

        <div class="alert-box">
          * Concentrações de glicose em via venosa periférica não devem ultrapassar 12.5%[span_34](start_span)[span_34](end_span). Use as faixas de eletrólitos para orientar a adição das ampolas de NaCl e KCl disponíveis no setor[span_35](start_span)[span_35](end_span).
        </div>
      </div>
    </section>

    <!-- 5. CATETERISMO UMBILICAL -->
    <section id="view-cateter" class="view-section">
      <div class="card">
        <h2>Calculadora de Cateterismo Umbilical Neonatal</h2>
        <p class="desc">Suporte à inserção de cateteres venoso e arterial por Peso e distância Ombro-Umbigo (POP-PB)[span_36](start_span)[span_36](end_span).</p>

        <div class="grid-2">
          <div class="form-group">
            <label for="cat_peso">Peso do RN (kg) — Cálculo por Fórmula[span_37](start_span)[span_37](end_span)</label>
            <input type="number" id="cat_peso" step="0.001" min="0.3" max="6.0" placeholder="Ex: 2.300" oninput="calcularCateterPeso()">
            <span style="font-size:0.75rem; color:var(--text-muted);">Fórmula: Comprimento = ((3 &times; Peso) + 9) / 2 + 1[span_38](start_span)[span_38](end_span)</span>
          </div>

          <div class="form-group">
            <label for="cat_ombro">Ou Distância Ombro-Umbigo (cm)[span_39](start_span)[span_39](end_span)</label>
            <select id="cat_ombro" onchange="calcularCateterOmbro()">
              <option value="">Selecione a medição...[span_40](start_span)[span_40](end_span)</option>
              <option value="9">9 cm[span_41](start_span)[span_41](end_span)</option>
              <option value="10">10 cm[span_42](start_span)[span_42](end_span)</option>
              <option value="11">11 cm[span_43](start_span)[span_43](end_span)</option>
              <option value="12">12 cm[span_44](start_span)[span_44](end_span)</option>
              <option value="13">13 cm[span_45](start_span)[span_45](end_span)</option>
              <option value="14">14 cm[span_46](start_span)[span_46](end_span)</option>
              <option value="15">15 cm[span_47](start_span)[span_47](end_span)</option>
              <option value="16">16 cm[span_48](start_span)[span_48](end_span)</option>
              <option value="17">17 cm[span_49](start_span)[span_49](end_span)</option>
            </select>
          </div>
        </div>

        <div class="result-box" style="margin-top: 14px;">
          <div style="font-size: 0.85rem; font-weight: 700; color: var(--primary-dark); margin-bottom: 10px;">Profundidade Recomendada de Inserção:</div>
          <div class="grid-3">
            <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; text-align:center;">
              <div style="font-size:0.75rem; text-transform:uppercase; color:var(--text-muted); font-weight:700;">Cateter Venoso[span_50](start_span)[span_50](end_span)</div>
              <div id="cat_resVenoso" style="font-size:1.4rem; font-weight:800; color:var(--primary); margin-top:4px;">-- cm</div>
            </div>
            <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; text-align:center;">
              <div style="font-size:0.75rem; text-transform:uppercase; color:var(--text-muted); font-weight:700;">Arterial Alto (T6-T9)[span_51](start_span)[span_51](end_span)</div>
              <div id="cat_resArtAlto" style="font-size:1.4rem; font-weight:800; color:#991b1b; margin-top:4px;">-- cm</div>
            </div>
            <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; text-align:center;">
              <div style="font-size:0.75rem; text-transform:uppercase; color:var(--text-muted); font-weight:700;">Arterial Baixo (L3-L5)[span_52](start_span)[span_52](end_span)</div>
              <div id="cat_resArtBaixo" style="font-size:1.4rem; font-weight:800; color:#b45309; margin-top:4px;">-- cm</div>
            </div>
          </div>
        </div>

        <div class="alert-box">
          ⚠️ <strong>Obrigatório:</strong> Realizar controle radiográfico de tórax e abdome após inserção e antes da infusão de soluções para confirmação anatômica da ponta[span_53](start_span)[span_53](end_span). Monitore a perfusão de membros inferiores[span_54](start_span)[span_54](end_span).
        </div>
      </div>
    </section>

    <!-- 6. GUIA DE DILUIÇÃO IV PEDIÁTRICA -->
    <section id="view-diluicao" class="view-section">
      <div class="card">
        <h2>Guia & Calculadora de Diluição IV Pediátrica (55+ Medicamentos)</h2>
        <p class="desc">Reconstituição, estabilidade, concentrações usuais e volume mínimo seguro para restrição hídrica[span_55](start_span)[span_55](end_span).</p>

        <div style="margin-bottom: 12px;">
          <input type="text" id="filtroDiluicao" placeholder="🔍 Buscar medicamento no guia (ex: Meropenem, Ceftriaxona, Fentanil)..." oninput="filtrarTabelaDiluicao()">
        </div>

        <div style="max-height: 480px; overflow-y: auto; border: 1px solid var(--border); border-radius: 8px;">
          <table>
            <thead>
              <tr>
                <th>Fármaco</th>
                <th>Reconstituição</th>
                <th>Diluentes</th>
                <th>Conc. Usual</th>
                <th>Conc. Máxima</th>
                <th>Velocidade</th>
                <th>Ação</th>
              </tr>
            </thead>
            <tbody id="corpoTabelaDiluicao"></tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- 7. INFUSÃO CONTÍNUA -->
    <section id="view-infusao" class="view-section">
      <div class="card">
        <h2>Calculadora de Dose de Infusão Contínua</h2>
        <p class="desc">Cálculo contínuo de soluções vasoativas e sedativas para bomba de infusão[span_56](start_span)[span_56](end_span).</p>

        <div class="form-group">
          <label for="inf_droga">Medicamento</label>
          <select id="inf_droga" onchange="aoTrocarDrogaInfusao()">
            <option value="adrenalina">Adrenalina (1 mg/mL)[span_57](start_span)[span_57](end_span)</option>
            <option value="noradrenalina">Noradrenalina (1 mg/mL)[span_58](start_span)[span_58](end_span)</option>
            <option value="dobutamina">Dobutamina (12,5 mg/mL)[span_59](start_span)[span_59](end_span)</option>
            <option value="dopamina">Dopamina (5 mg/mL)[span_60](start_span)[span_60](end_span)</option>
            <option value="fentanil">Fentanil (0,05 mg/mL = 50 mcg/mL)[span_61](start_span)[span_61](end_span)</option>
            <option value="midazolam">Midazolam (5 mg/mL)[span_62](start_span)[span_62](end_span)</option>
            <option value="cetamina">Cetamina (50 mg/mL)[span_63](start_span)[span_63](end_span)</option>
            <option value="milrinona">Milrinona (1 mg/mL)[span_64](start_span)[span_64](end_span)</option>
            <option value="precedex">Precedex / Dexmedetomidina (0,1 mg/mL)[span_65](start_span)[span_65](end_span)</option>
            <option value="custom">Outro Personalizado...[span_66](start_span)[span_66](end_span)</option>
          </select>
        </div>

        <div id="inf_customBox" style="display:none; background:#f8fafc; padding:12px; border-radius:8px; border:1px dashed var(--border); margin-bottom:12px;">
          <div class="grid-2">
            <div class="form-group"><label>Nome da Medicação</label><input type="text" id="inf_customNome" placeholder="Ex: Propofol"></div>
            <div class="form-group"><label>Concentração do Estoque (mg/mL)</label><input type="number" id="inf_customConc" step="any" placeholder="Ex: 10"></div>
          </div>
        </div>

        <div class="grid-2">
          <div class="form-group">
            <label>Peso do Paciente (kg)</label>
            <input type="number" id="inf_peso" step="any" value="10" oninput="calcularInfusao()">
          </div>
          <div class="form-group">
            <label>Vazão Atual na Bomba (mL/h)</label>
            <input type="number" id="inf_vazao" step="any" value="1" oninput="calcularInfusao()">
          </div>
          <div class="form-group">
            <label>Volume do Fármaco (mL)</label>
            <input type="number" id="inf_volDroga" step="any" value="1.44" oninput="calcularInfusao()">
          </div>
          <div class="form-group">
            <label>Volume do Diluente (mL)</label>
            <input type="number" id="inf_volDiluente" step="any" value="22.56" oninput="calcularInfusao()">
          </div>
        </div>

        <div class="result-box">
          <div style="font-size:0.8rem; text-transform:uppercase; color:var(--text-muted); font-weight:700; margin-bottom:10px;">Doses Infundidas no Momento:[span_67](start_span)[span_67](end_span)</div>
          <div class="grid-3">
            <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; text-align:center;">
              <div style="font-size:0.75rem; color:var(--text-muted); font-weight:700;">mcg/kg/min[span_68](start_span)[span_68](end_span)</div>
              <div id="inf_resMcgKgMin" style="font-size:1.3rem; font-weight:800; color:var(--primary); margin-top:4px;">0.100</div>
            </div>
            <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; text-align:center;">
              <div style="font-size:0.75rem; color:var(--text-muted); font-weight:700;">mcg/kg/h[span_69](start_span)[span_69](end_span)</div>
              <div id="inf_resMcgKgH" style="font-size:1.3rem; font-weight:800; color:var(--primary); margin-top:4px;">6.000</div>
            </div>
            <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; text-align:center;">
              <div style="font-size:0.75rem; color:var(--text-muted); font-weight:700;">mg/kg/h[span_70](start_span)[span_70](end_span)</div>
              <div id="inf_resMgKgH" style="font-size:1.3rem; font-weight:800; color:var(--primary); margin-top:4px;">0.006</div>
            </div>
          </div>
          <div id="inf_resDetalhes" style="font-size:0.8rem; color:var(--text-muted); margin-top:10px; text-align:right;"></div>
        </div>
      </div>
    </section>

    <!-- 8. DOSES INTERMITENTES -->
    <section id="view-drogas" class="view-section">
      <div class="card">
        <h2>Calculadora de Doses Intermitentes & Prescrição Pediátrica</h2>
        <p class="desc">Apoio a antibióticos, analgésicos e anticonvulsivantes com checagem de dose máxima e ajuste para neonatos[span_71](start_span)[span_71](end_span).</p>

        <div class="grid-2">
          <div>
            <label>Selecione o Medicamento:</label>
            <input type="text" id="drg_busca" placeholder="🔍 Filtrar medicamento..." oninput="filtrarDrogasIntermitentes()" style="margin-bottom: 6px;">
            <div id="drg_lista" style="max-height: 240px; overflow-y: auto; border: 1px solid var(--border); border-radius: 6px;"></div>
          </div>

          <div>
            <div class="grid-2">
              <div class="form-group"><label>Peso (kg)</label><input type="number" id="drg_peso" step="any" placeholder="Ex: 14"></div>
              <div class="form-group">
                <label>Idade</label>
                <div style="display: flex; gap: 4px;">
                  <input type="number" id="drg_idadeVal" placeholder="Ex: 5" style="width: 55%;">
                  <select id="drg_idadeUnid" style="width: 45%;">
                    <option value="dias">dias[span_72](start_span)[span_72](end_span)</option>
                    <option value="meses">meses[span_73](start_span)[span_73](end_span)</option>
                    <option value="anos" selected>anos[span_74](start_span)[span_74](end_span)</option>
                  </select>
                </div>
              </div>
            </div>

            <div class="form-group">
              <label>Idade Gestacional em semanas (apenas prematuros)[span_75](start_span)[span_75](end_span)</label>
              <input type="number" id="drg_ig" placeholder="Ex: 34 (opcional)">
            </div>

            <div class="form-group">
              <label>Volume Diluente adicional (mL)</label>
              <input type="number" id="drg_diluente" placeholder="Conforme volume desejado">
            </div>

            <button class="btn btn-primary" style="width: 100%;" onclick="calcularDrogasIntermitentes()">Calcular Dose & Prescrição</button>
          </div>
        </div>

        <div id="drg_resultadoBox" class="result-box" style="display: none; margin-top: 14px;">
          <div id="drg_calcDetalhes" style="font-size: 0.9rem; margin-bottom: 8px;"></div>
          <div style="font-weight: 700; margin-top: 10px; font-size: 0.85rem; color: var(--primary);">Texto pronto para prescrição / prontuário:</div>
          <textarea id="drg_textoPrescricao" rows="4" readonly style="font-family: monospace; font-size: 0.82rem; margin-top: 4px;"></textarea>
          <button class="btn btn-teal" style="margin-top: 8px;" onclick="copiarTexto('drg_textoPrescricao')">📋 Copiar Prescrição</button>
        </div>
      </div>
    </section>

  </main>

  <script>
    function navegarPara(viewId) {
      document.querySelectorAll('.view-section').forEach(s => s.classList.remove('active'));
      document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));

      const target = document.getElementById(`view-${viewId}`);
      if (target) target.classList.add('active');

      const btn = Array.from(document.querySelectorAll('.nav-btn')).find(b => b.getAttribute('onclick') && b.getAttribute('onclick').includes(viewId));
      if (btn) btn.classList.add('active');

      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function mostrarToast(msg = 'Copiado para a área de transferência!') {
      const toast = document.getElementById('hubToast');
      toast.innerText = msg;
      toast.style.display = 'block';
      setTimeout(() => { toast.style.display = 'none'; }, 2400);
    }

    function copiarTexto(elementId) {
      const el = document.getElementById(elementId);
      if (!el) return;
      el.select();
      el.setSelectionRange(0, 99999);
      if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(el.value || el.innerText).then(() => mostrarToast());
      } else {
        document.execCommand('copy');
        mostrarToast();
      }
    }

    function filtrarCardsHub() {
      const q = document.getElementById('filtroHub').value.toLowerCase().trim();
      document.querySelectorAll('#gridCardsHub .tool-tile').forEach(card => {
        const text = (card.innerText + ' ' + card.getAttribute('data-tags')).toLowerCase();
        card.style.display = text.includes(q) ? 'flex' : 'none';
      });
    }

    function salvarLinkGem() {
      const link = document.getElementById('linkGemCustom').value.trim();
      if (link) {
        localStorage.setItem('hub_gem_link', link);
        mostrarToast('Link do Gem salvo!');
      }
    }

    /* =========================================================================
       EXTRATOR DE EXAMES - LINHA DIRETA SEM CABEÇALHOS
       ========================================================================= */
    function zerarExtratorExames() {
      document.getElementById('textoLaudoBruto').value = '';
      document.getElementById('textoLinhaContinuaExames').value = '';
      document.getElementById('resultadoExamesContainer').style.display = 'none';
      document.getElementById('textoLaudoBruto').focus();
      mostrarToast('Campos limpos!');
    }

    function processarExamesLocais() {
      const raw = document.getElementById('textoLaudoBruto').value;
      if (!raw.trim()) return;

      // Base com expressões regulares robustas e captura prioritária
      const EXAM_DEF = [
        // Série Vermelha
        { label: 'Hb', reg: /(?:\bhb\b|\bhemoglobina\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Ht', reg: /(?:\bht\b|\bhemat[oó]crito\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Erit', reg: /(?:\berit\b|\beritr[oó]citos\b|\bhem[aá]cias(?!\s*ur)\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Leuco', reg: /(?:\bleuco\b|\bleuc[oó]citos(?!\s*ur)\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Plaq', reg: /(?:\bplaq\b|\bplaquetas\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'VCM', reg: /(?:\bvcm\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'HCM', reg: /(?:\bhcm\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'CHCM', reg: /(?:\bchcm\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'RDW', reg: /(?:\brdw\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Diferencial Leucocitário
        { label: 'Bast', reg: /(?:\bbast\b|\bbastonetes?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Seg', reg: /(?:\bseg\b|\bsegmentados?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Neut', reg: /(?:\bneut\b|\bneutr[oó]filos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Blast', reg: /(?:\bblast\b|\bblastos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Promiel', reg: /(?:\bpromiel\b|\bpromiel[oó]citos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Miel', reg: /(?:\bmiel\b|\bmiel[oó]citos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Metamiel', reg: /(?:\bmetamiel\b|\bmetamiel[oó]citos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Linf Atíp', reg: /(?:\blinf\s*at[ií]p\b|\blinf[oó]citos?\s*at[ií]picos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Linf Tot', reg: /(?:\blinf\s*tot\b|\blinf[oó]citos?\s*totais?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Linf', reg: /(?:\blinf(?!\s*tot|\s*at[ií]p)\b|\blinf[oó]citos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Monoc', reg: /(?:\bmonoc\b|\bmon[oó]citos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Eos', reg: /(?:\beos\b|\beosin[oó]filos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Basof', reg: /(?:\bbasof\b|\bbas[oó]filos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Gasometria
        { label: 'pH', reg: /(?:\bph\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'pO2', reg: /(?:\bpo2\b|\bpao2\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'pCO2', reg: /(?:\bpco2\b|\bpaco2\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'HCO3', reg: /(?:\bhco3\b|\bbicarbonato\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'BE', reg: /(?:\bbe\b|\bbase\s*excess\b)[\s:=]+([-+]?[0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'SatO2', reg: /(?:\bsato2\b|\bsatura[cç][aã]o\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Lactato', reg: /(?:\blact\b|\blactato\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Função Renal e Metabólica (com Ureia reforçada)
        { label: 'Ureia', reg: /(?:\bureia\b|\bur[eé]ia\b|\bur\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Cr', reg: /(?:\bcr\b|\bcreatinina\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Proteínas
        { label: 'Albumina', reg: /(?:\balb\b|\balbumina\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Prot Tot', reg: /(?:\bprot\s*tot\b|\bprote[ií]nas\s*totais?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Globulina', reg: /(?:\bglob\b|\bglobulina\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Relação A/G', reg: /(?:\brela[cç][aã]o\s*a\/g\b|\ba\/g\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Eletrólitos
        { label: 'Na', reg: /(?:\bna\b|\bs[oó]dio\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'K', reg: /(?:\bk\b|\bpot[aá]ssio\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'CaI', reg: /(?:\bcai\b|\bca\s*i[oô]nico\b|\bc[aá]lcio\s*i[oô]nico\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'CaT', reg: /(?:\bcat\b|\bca\s*total\b|\bc[aá]lcio\s*total\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Mg', reg: /(?:\bmg\b|\bmagn[eé]sio\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'P', reg: /(?:\bp\b|\bf[oó]sforo\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Cl', reg: /(?:\bcl\b|\bcloro\b|\bcloretos?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Hepatograma
        { label: 'TGO', reg: /(?:\btgo\b|\bast\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'TGP', reg: /(?:\btgp\b|\balt\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'GGT', reg: /(?:\bggt\b|\bgama\s*gt\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'FA', reg: /(?:\bfa\b|\bfosfatase\s*alcalina\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'BT', reg: /(?:\bbt\b|\bbilirrubina\s*total\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'BD', reg: /(?:\bbd\b|\bbilirrubina\s*direta\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'BI', reg: /(?:\bbi\b|\bbilirrubina\s*indireta\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Inflamação & Coagulação
        { label: 'PCR', reg: /(?:\bpcr\b|\bprote[ií]na\s*c\s*reativa\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Procalc', reg: /(?:\bprocalc\b|\bprocalcitonina\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'VHS', reg: /(?:\bvhs\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'INR', reg: /(?:\binr\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'TAP', reg: /(?:\btap\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'TTPA', reg: /(?:\bttpa\b|\bktpa\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Fibrinogênio', reg: /(?:\bfibrinog[eê]nio\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'D-Dímero', reg: /(?:\bd-d[ií]mero\b|\bd\s*d[ií]mero\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },

        // Urina / EAS
        { label: 'Densidade', reg: /(?:\bdensidade\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'pH Ur', reg: /(?:\bph\s*ur(?:ina)?\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Leuco Ur', reg: /(?:\bleuco(?:\s*ur|\s*urina)\b|\bleuc[oó]citos\s*(?:na\s*)?urina\b|\bpi[oó]citos\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Hemácias Ur', reg: /(?:\bhem[aá]cias(?:\s*ur|\s*urina)\b|\bhem\s*ur\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i },
        { label: 'Bactérias', reg: /(?:\bbact[eé]rias\b)[\s:=]+([0-9]+(?:[.,][0-9]+)?)/i }
      ];

      const encontrados = [];

      EXAM_DEF.forEach(item => {
        const match = raw.match(item.reg);
        if (match && match[1]) {
          // Mantém vírgula decimal como no padrão médico
          const valFormatado = match[1].replace('.', ',');
          encontrados.push(`${item.label} ${valFormatado}`);
        }
      });

      if (encontrados.length === 0) {
        alert("Nenhum exame identificado. Verifique se colou os nomes dos exames com seus respectivos valores numéricos.");
        return;
      }

      // Gera a linha única sem prefixos ou quebras
      const linhaFinal = encontrados.join(' / ');
      document.getElementById('textoLinhaContinuaExames').value = linhaFinal;
      document.getElementById('resultadoExamesContainer').style.display = 'block';
    }

    /* =========================================================================
       1. ESCORE PIM 2
       ========================================================================= */
    function calcularPim2() {
      const sbp = parseFloat(document.getElementById('p2_sbp').value) || 120;
      const pupils = parseInt(document.getElementById('p2_pupils').value) || 0;
      const pao2 = parseFloat(document.getElementById('p2_pao2').value) || 0;
      const fio2 = parseFloat(document.getElementById('p2_fio2').value) || 21;
      const be = parseFloat(document.getElementById('p2_be').value) || 0;
      const vent = parseInt(document.getElementById('p2_vent').value) || 0;
      const elective = parseInt(document.getElementById('p2_elective').value) || 0;
      const surgery = parseInt(document.getElementById('p2_surgery').value) || 0;
      const bypass = parseInt(document.getElementById('p2_bypass').value) || 0;
      const highrisk = parseInt(document.getElementById('p2_highrisk').value) || 0;
      const lowrisk = parseInt(document.getElementById('p2_lowrisk').value) || 0;

      let sbpVal = Math.abs(sbp - 120);
      let o2Ratio = (pao2 > 0) ? ((100 * (fio2 / 100)) / pao2) : 0;
      let beVal = Math.abs(be);

      let logit = -4.8841;
      logit += 0.01395 * sbpVal;
      if (pupils === 1) logit += 3.0791;
      logit += 0.2888 * o2Ratio;
      logit += 0.1040 * beVal;
      if (vent === 1) logit += 1.3352;
      if (elective === 1) logit -= 0.9282;
      if (surgery === 1) logit -= 1.0244;
      if (bypass === 1) logit -= 0.3882;
      if (highrisk > 0) logit += 1.6696;
      if (lowrisk > 0) logit -= 1.5883;

      let prob = Math.exp(logit) / (1 + Math.exp(logit));
      let pct = prob * 100;

      document.getElementById('p2_resLogit').innerText = logit.toFixed(4);
      document.getElementById('p2_resMortality').innerText = `${pct.toFixed(2)}%`;
    }

    function copiarLaudoPim2() {
      const mort = document.getElementById('p2_resMortality').innerText;
      const logit = document.getElementById('p2_resLogit').innerText;
      const sbp = document.getElementById('p2_sbp').value;
      const be = document.getElementById('p2_be').value;

      const txt = `ESCORE PIM 2 (Paediatric Index of Mortality 2):\n` +
                  `- Risco de Mortalidade Estimado: ${mort} (Logit: ${logit})\n` +
                  `- PAS: ${sbp} mmHg | Base Excess: ${be} mmol/L\n` +
                  `- Coletado nas primeiras horas de admissão na UTIP (Slater et al., 2003).`;
      
      navigator.clipboard ? navigator.clipboard.writeText(txt).then(() => mostrarToast('Laudo do PIM 2 copiado!')) : mostrarToast();
    }

    /* =========================================================================
       2. BALANÇO HÍDRICO & SINAIS VITAIS
       ========================================================================= */
    let acumuladosBH = { ev: 0, vo: 0, diurese: 0, drenos: 0, vomitos: 0 };

    function parseBH(val) {
      if (!val) return 0;
      return parseFloat(val.toString().replace(',', '.')) || 0;
    }
    function formatBH(n, d = 1) {
      return (isNaN(n) ? 0 : n).toFixed(d).replace('.', ',');
    }
    function formatVitalBH(str) {
      if (!str) return '';
      let partes = str.trim().split(/[\s\-–—/]+/);
      return partes.length >= 2 ? `${partes[0]}-${partes[1]}` : (partes[0] || '');
    }

    function handleBhKey(e, el) {
      if (e.key === 'Enter') {
        e.preventDefault();
        acumuladosBH[el.id.replace('bh_', '')] += parseBH(el.value);
        el.value = formatBH(acumuladosBH[el.id.replace('bh_', '')], 1);
        setTimeout(() => { el.focus(); el.select(); }, 10);
        calcularBH();
      } else if (e.key === 'Backspace' || e.key === 'Delete') {
        if (el.selectionStart === 0 && el.selectionEnd === el.value.length) {
          acumuladosBH[el.id.replace('bh_', '')] = 0;
          el.value = '';
          calcularBH();
        }
      }
    }

    function zerarCamposBH() {
      ['bh_pam', 'bh_fc', 'bh_fr', 'bh_sat', 'bh_temp', 'bh_hgt', 'bh_peso', 'bh_ev', 'bh_vo', 'bh_diurese', 'bh_drenos', 'bh_vomitos'].forEach(id => {
        const el = document.getElementById(id);
        if (el) el.value = '';
      });
      acumuladosBH = { ev: 0, vo: 0, diurese: 0, drenos: 0, vomitos: 0 };
      calcularBH();
    }

    function calcHolliday(peso) {
      if (peso <= 10) return peso * 100;
      if (peso <= 20) return 1000 + (peso - 10) * 50;
      return Math.min(1500 + (peso - 20) * 20, 2400);
    }

    function calcularBH() {
      const peso = parseBH(document.getElementById('bh_peso').value);
      const horas = parseInt(document.getElementById('bh_horas').value) || 24;

      const ev = acumuladosBH.ev;
      const vo = acumuladosBH.vo;
      const diurese = acumuladosBH.diurese;
      const drenos = acumuladosBH.drenos;
      const vomitos = acumuladosBH.vomitos;

      let calUnidades = 0;
      let calTotal = 0;
      if (peso > 10) {
        calTotal = calcHolliday(peso);
        calUnidades = calTotal / 100;
        document.getElementById('bh_pesoCal').value = `${formatBH(calUnidades, 2)} Cal (${calTotal} kcal)`;
      } else {
        document.getElementById('bh_pesoCal').value = '';
      }

      const totalEntradas = ev + vo;
      const totalSaidas = diurese + drenos + vomitos;
      const balanco = totalEntradas - totalSaidas;

      const sinal = balanco > 0 ? '+' : '';
      const disp = document.getElementById('bh_displayVal');
      disp.innerText = `${sinal}${formatBH(balanco, 1)} mL`;
      disp.style.color = (balanco > 0) ? 'var(--success)' : (balanco < 0 ? 'var(--danger)' : 'var(--text)');

      let diureseStr = '--';
      if (peso > 0) {
        const tx = diurese / peso / horas;
        diureseStr = `${formatBH(tx, 2)} mL/kg/h`;
        if (peso >= 30) diureseStr += ` (${formatBH(diurese / horas, 1)} mL/h)`;
      }
      document.getElementById('bh_taxaDiurese').innerText = `Diurese: ${diureseStr}`;

      const pam = formatVitalBH(document.getElementById('bh_pam').value);
      const fc = formatVitalBH(document.getElementById('bh_fc').value);
      const fr = formatVitalBH(document.getElementById('bh_fr').value);
      const sat = formatVitalBH(document.getElementById('bh_sat').value);
      const temp = formatVitalBH(document.getElementById('bh_temp').value);
      const hgt = formatVitalBH(document.getElementById('bh_hgt').value);

      let sv = [];
      if (pam) sv.push(`PAM: ${pam} mmHg`);
      if (fc) sv.push(`FC: ${fc} bpm`);
      if (fr) sv.push(`FR: ${fr} irpm`);
      if (sat) sv.push(`SatO2: ${sat}%`);
      if (temp) sv.push(`Temp: ${temp} ºC`);
      if (hgt) sv.push(`HGT: ${hgt} mg/dl`);

      let txt = `SINAIS VITAIS E BALANÇO HÍDRICO (${horas} HORAS):\n`;
      if (sv.length > 0) txt += sv.join('    ') + '\n\n';

      if (peso > 0) {
        txt += `- Peso: ${formatBH(peso, 2)} kg\n`;
        if (peso > 10) txt += `- Peso Calórico (Holliday): ${formatBH(calUnidades, 2)} Cal (${calTotal} kcal)\n`;
      }

      txt += `- Entradas: Total = ${formatBH(totalEntradas, 1)} mL (EV: ${formatBH(ev, 1)} mL | VO: ${formatBH(vo, 1)} mL)\n`;
      txt += `- Saídas: Total = ${formatBH(totalSaidas, 1)} mL (Diurese: ${formatBH(diurese, 1)} mL | Drenos: ${formatBH(drenos, 1)} mL | Outros: ${formatBH(vomitos, 1)} mL)\n`;

      if (peso > 0) {
        const ofr = (peso <= 10) ? (totalEntradas / peso) : (totalEntradas / calUnidades);
        const unidOfr = (peso <= 10) ? 'mL/kg' : 'mL/Kcal';
        txt += `- Oferta Hídrica: ${formatBH(ofr, 1)} ${unidOfr}/${horas}h\n`;
        txt += `- Diurese: ${diureseStr}\n`;
      }
      txt += `- BH Final (${horas}h): ${sinal}${formatBH(balanco, 1)} mL`;

      document.getElementById('bh_textoProntuario').value = txt;
    }

    function copiarProntuarioBH() {
      copiarTexto('bh_textoProntuario');
    }

    /* =========================================================================
       3. INTERGROWTH-21st (RN)
       ========================================================================= */
    const IG_P = [3, 5, 10, 50, 90, 95, 97];
    const IG_DATA = {
      weight: {
        M: { 33:[1.18,1.28,1.43,1.95,2.52,2.70,2.82], 34:[1.45,1.55,1.71,2.22,2.79,2.96,3.08], 35:[1.70,1.80,1.95,2.47,3.03,3.20,3.32], 36:[1.93,2.03,2.18,2.69,3.25,3.42,3.54], 37:[2.13,2.24,2.38,2.89,3.45,3.62,3.74], 38:[2.32,2.42,2.57,3.07,3.63,3.80,3.92], 39:[2.49,2.59,2.73,3.24,3.79,3.96,4.08], 40:[2.63,2.73,2.88,3.38,3.94,4.11,4.22], 41:[2.76,2.86,3.01,3.51,4.06,4.23,4.35], 42:[2.88,2.98,3.12,3.62,4.17,4.34,4.46] },
        F: { 33:[1.20,1.29,1.41,1.86,2.35,2.51,2.61], 34:[1.47,1.55,1.68,2.13,2.64,2.79,2.90], 35:[1.71,1.79,1.92,2.38,2.89,3.05,3.16], 36:[1.92,2.01,2.14,2.60,3.12,3.28,3.39], 37:[2.11,2.20,2.33,2.80,3.32,3.49,3.60], 38:[2.28,2.37,2.50,2.97,3.51,3.67,3.78], 39:[2.42,2.51,2.65,3.13,3.66,3.83,3.94], 40:[2.55,2.64,2.78,3.26,3.80,3.97,4.08], 41:[2.65,2.75,2.89,3.37,3.92,4.09,4.20], 42:[2.74,2.84,2.98,3.46,4.01,4.19,4.30] }
      },
      length: {
        M: { 33:[39.7,40.3,41.1,43.8,46.6,47.4,48.0], 34:[41.1,41.6,42.4,45.0,47.6,48.4,48.9], 35:[42.3,42.8,43.5,46.0,48.5,49.3,49.8], 36:[43.4,43.9,44.6,47.0,49.4,50.1,50.6], 37:[44.3,44.8,45.5,47.8,50.1,50.9,51.3], 38:[45.2,45.7,46.4,48.6,50.8,51.5,52.0], 39:[46.0,46.5,47.1,49.3,51.5,52.1,52.6], 40:[46.8,47.2,47.8,49.9,52.0,52.7,53.1], 41:[47.4,47.8,48.5,50.5,52.6,53.2,53.6], 42:[48.0,48.4,49.0,51.0,53.0,53.7,54.1] },
        F: { 33:[39.8,40.3,41.0,43.4,45.7,46.4,46.9], 34:[41.0,41.5,42.2,44.6,46.8,47.5,47.9], 35:[42.1,42.6,43.3,45.6,47.8,48.4,48.9], 36:[43.1,43.6,44.3,46.5,48.6,49.3,49.7], 37:[44.0,44.5,45.1,47.3,49.4,50.0,50.4], 38:[44.8,45.2,45.9,48.0,50.1,50.7,51.1], 39:[45.5,45.9,46.6,48.7,50.7,51.3,51.7], 40:[46.1,46.5,47.2,49.2,51.2,51.8,52.2], 41:[46.7,47.1,47.7,49.8,51.7,52.3,52.7], 42:[47.2,47.6,48.2,50.2,52.2,52.7,53.1] }
      },
      hc: {
        M: { 33:[28.2,28.6,29.1,30.9,32.7,33.3,33.6], 34:[28.9,29.3,29.8,31.5,33.2,33.8,34.1], 35:[29.6,29.9,30.4,32.0,33.7,34.2,34.6], 36:[30.2,30.5,30.9,32.5,34.2,34.7,35.0], 37:[30.7,31.0,31.5,33.0,34.6,35.1,35.4], 38:[31.2,31.5,32.0,33.5,35.0,35.5,35.8], 39:[31.7,32.0,32.4,33.9,35.4,35.9,36.2], 40:[32.2,32.4,32.9,34.3,35.8,36.3,36.6], 41:[32.6,32.9,33.3,34.7,36.2,36.6,36.9], 42:[33.0,33.3,33.7,35.1,36.5,37.0,37.2] },
        F: { 33:[27.92,28.26,28.76,30.46,32.24,32.78,33.14], 34:[28.64,28.96,29.44,31.08,32.78,33.30,33.65], 35:[29.28,29.59,30.06,31.64,33.28,33.78,34.12], 36:[29.87,30.17,30.62,32.14,33.74,34.22,34.55], 37:[30.40,30.69,31.13,32.61,34.15,34.62,34.94], 38:[30.88,31.16,31.59,33.03,34.53,34.99,35.30], 39:[31.32,31.59,32.01,33.41,34.88,35.32,35.62], 40:[31.72,31.99,32.39,33.76,35.19,35.63,35.92], 41:[32.08,32.34,32.74,34.08,35.48,35.91,36.19], 42:[32.41,32.67,33.06,34.37,35.74,36.16,36.44] }
      }
    };

    function igInterpRow(tbl, sex, ga) {
      const gaClamp = Math.min(42.999, Math.max(33, ga));
      const wL = Math.min(42, Math.max(33, Math.floor(gaClamp)));
      const wH = Math.min(42, wL + 1);
      const frac = (wH === wL) ? 0 : (gaClamp - wL);
      const rL = tbl[sex][wL];
      const rH = tbl[sex][wH];
      return rL.map((v, i) => v + (rH[i] - v) * frac);
    }

    function igEstimatePct(row, val) {
      if (val <= row[0]) {
        const slope = (row[1] - row[0]) / (IG_P[1] - IG_P[0]);
        return { pct: Math.max(0.1, IG_P[0] - (row[0] - val) / (slope || 0.0001)), belowMin: true };
      }
      if (val >= row[row.length - 1]) {
        const slope = (row[row.length - 1] - row[row.length - 2]) / (IG_P[IG_P.length - 1] - IG_P[IG_P.length - 2]);
        return { pct: Math.min(99.9, IG_P[IG_P.length - 1] + (val - row[row.length - 1]) / (slope || 0.0001)), aboveMax: true };
      }
      for (let i = 0; i < row.length - 1; i++) {
        if (val >= row[i] && val <= row[i + 1]) {
          const frac = (val - row[i]) / (row[i + 1] - row[i] || 0.0001);
          return { pct: IG_P[i] + frac * (IG_P[i + 1] - IG_P[i]), belowMin: false, aboveMax: false };
        }
      }
      return { pct: 50, belowMin: false, aboveMax: false };
    }

    function igClassifyGA(w, d) {
      const tot = Math.round(w * 7 + (d || 0));
      if (tot < 196) return { label: "Pré-termo extremo", range: "< 28 semanas" };
      if (tot <= 223) return { label: "Muito pré-termo", range: "28 a 31 semanas e 6 dias" };
      if (tot <= 237) return { label: "Pré-termo moderado", range: "32 a 33 semanas e 6 dias" };
      if (tot <= 258) return { label: "Pré-termo tardio", range: "34 a 36 semanas e 6 dias" };
      if (tot <= 272) return { label: "A termo precoce", range: "37 a 38 semanas e 6 dias" };
      if (tot <= 286) return { label: "A termo completo", range: "39 a 40 semanas e 6 dias" };
      if (tot <= 293) return { label: "A termo tardio", range: "41 a 41 semanas e 6 dias" };
      return { label: "Pós-termo", range: "≥ 42 semanas" };
    }

    function calcularIntergrowth() {
      const sex = document.getElementById('ig_sexo').value;
      const w = parseFloat(document.getElementById('ig_sem').value) || 0;
      const d = parseFloat(document.getElementById('ig_dias').value) || 0;
      const pesoG = parseFloat(document.getElementById('ig_peso').value) || 0;
      const comp = parseFloat(document.getElementById('ig_comp').value) || 0;
      const pc = parseFloat(document.getElementById('ig_pc').value) || 0;

      const cont = document.getElementById('ig_resultadoContainer');
      if (w < 20) { cont.style.display = 'none'; return; }
      cont.style.display = 'block';

      const gaDec = w + d / 7;
      const inRange = (gaDec >= 33 && gaDec <= 42.999);
      const gaCat = igClassifyGA(w, d);

      document.getElementById('ig_gaBanner').innerHTML = `
        <div style="font-size:0.8rem; color:var(--text-muted); text-transform:uppercase; font-weight:700;">Classificação pela Idade Gestacional</div>
        <div style="font-size:1.15rem; font-weight:800; color:#1e293b;">${gaCat.label} (${gaCat.range})</div>
        ${!inRange ? '<div style="color:#b91c1c; font-size:0.8rem; margin-top:4px;">⚠️ Curvas INTERGROWTH-21st são validadas de 33+0 a 42+6 sem. Para &lt;33 sem, utilize Fenton 2013.</div>' : ''}
      `;

      let cardsHtml = '';
      let resPeso = null, resComp = null, resPc = null;

      function fmtP(est) {
        if (est.belowMin) return '< P3';
        if (est.aboveMax) return '> P97';
        return `≈ P${est.pct.toFixed(0)}`;
      }

      if (inRange && pesoG > 0) {
        const row = igInterpRow(IG_DATA.weight, sex, gaDec);
        const est = igEstimatePct(row, pesoG / 1000);
        const cls = est.pct < 10 ? 'PIG' : (est.pct > 90 ? 'GIG' : 'AIG');
        resPeso = { est, cls, val: pesoG };
        cardsHtml += `
          <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; display:flex; justify-content:space-between; align-items:center;">
            <div><div style="font-size:0.75rem; color:var(--text-muted);">PESO AO NASCER</div><div style="font-size:1.1rem; font-weight:800;">${pesoG} g</div></div>
            <div style="text-align:right;"><span style="background:#f1f5f9; padding:3px 8px; border-radius:99px; font-weight:700;">${fmtP(est)}</span><div style="font-size:0.8rem; margin-top:2px;">${cls === 'PIG' ? 'Pequeno (PIG)' : (cls === 'GIG' ? 'Grande (GIG)' : 'Adequado (AIG)')}</div></div>
          </div>`;
      }

      if (inRange && comp > 0) {
        const row = igInterpRow(IG_DATA.length, sex, gaDec);
        const est = igEstimatePct(row, comp);
        const cls = est.pct < 10 ? 'Curto' : (est.pct > 90 ? 'Comprido' : 'Adequado');
        resComp = { est, cls, val: comp };
        cardsHtml += `
          <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; display:flex; justify-content:space-between; align-items:center;">
            <div><div style="font-size:0.75rem; color:var(--text-muted);">COMPRIMENTO</div><div style="font-size:1.1rem; font-weight:800;">${comp} cm</div></div>
            <div style="text-align:right;"><span style="background:#f1f5f9; padding:3px 8px; border-radius:99px; font-weight:700;">${fmtP(est)}</span><div style="font-size:0.8rem; margin-top:2px;">${cls} para IG</div></div>
          </div>`;
      }

      if (inRange && pc > 0) {
        const row = igInterpRow(IG_DATA.hc, sex, gaDec);
        const est = igEstimatePct(row, pc);
        const cls = est.pct < 10 ? 'Pequeno' : (est.pct > 90 ? 'Grande' : 'Adequado');
        resPc = { est, cls, val: pc };
        cardsHtml += `
          <div style="background:#fff; border:1px solid var(--border); border-radius:8px; padding:12px; display:flex; justify-content:space-between; align-items:center;">
            <div><div style="font-size:0.75rem; color:var(--text-muted);">PERÍMETRO CEFÁLICO</div><div style="font-size:1.1rem; font-weight:800;">${pc} cm</div></div>
            <div style="text-align:right;"><span style="background:#f1f5f9; padding:3px 8px; border-radius:99px; font-weight:700;">${fmtP(est)}</span><div style="font-size:0.8rem; margin-top:2px;">${cls} para IG</div></div>
          </div>`;
      }

      document.getElementById('ig_cardsList').innerHTML = cardsHtml;

      let iugrHtml = '';
      if (resPeso && resPeso.est.pct < 10) {
        let pattern = '';
        if (resPc) {
          if (resPc.est.pct - resPeso.est.pct > 25) pattern = 'Padrão Assimétrico (PC poupado em relação ao peso) — provável início tardio.';
          else if (resPc.est.pct < 10) pattern = 'Padrão Simétrico (Peso e PC reduzidos) — início precoce / causas genéticas ou constitucionais.';
        }
        iugrHtml = `
          <div class="alert-box">
            <strong>⚠️ Alerta para Restrição de Crescimento Intrauterino (RCIU) — ${resPeso.est.pct < 3 ? 'Grave' : 'Leve a Moderada'}</strong><br>
            Peso abaixo do P10 para IG (compatível com PIG). ${pattern}
          </div>`;
      }
      document.getElementById('ig_iugrBox').innerHTML = iugrHtml;

      let laudo = `LAUDO ANTROPOMÉTRICO NEONATAL (INTERGROWTH-21st):\n`;
      laudo += `- Sexo: ${sex === 'M' ? 'Masculino' : 'Feminino'} | IG: ${w} sem + ${d} dias (${gaCat.label})\n`;
      if (resPeso) laudo += `- Peso: ${resPeso.val} g [${fmtP(resPeso.est)}] -> ${resPeso.cls}\n`;
      if (resComp) laudo += `- Comprimento: ${resComp.val} cm [${fmtP(resComp.est)}] -> ${resComp.cls}\n`;
      if (resPc) laudo += `- Perímetro Cefálico: ${resPc.val} cm [${fmtP(resPc.est)}] -> ${resPc.cls}\n`;
      if (resPeso && resPeso.est.pct < 10) laudo += `- RCIU: Suspeita clínica ativa (${resPeso.est.pct < 3 ? 'Grave < P3' : 'P3-P10'}).\n`;

      document.getElementById('ig_resumoTexto').value = laudo;
    }

    /* =========================================================================
       4. TIG & ELETRÓLITOS NEONATAIS (SBP)
       ========================================================================= */
    function obterFaixaFluidoSBP(peso, dia, tipo) {
      if (tipo === 'termo') {
        if (dia == 1) return [40, 60];
        if (dia == 2) return [50, 70];
        if (dia == 3) return [60, 80];
        if (dia == 4) return [60, 100];
        if (dia == 5) return [100, 140];
        return [140, 160];
      }
      if (peso > 1.5) {
        if (dia == 1) return [60, 80];
        if (dia == 2) return [80, 100];
        if (dia == 3) return [100, 120];
        if (dia == 4) return [120, 140];
        if (dia == 5) return [140, 160];
        return [140, 160];
      } else {
        if (dia == 1) return [70, 90];
        if (dia == 2) return [90, 110];
        if (dia == 3) return [110, 130];
        if (dia == 4) return [130, 150];
        return [140, 160];
      }
    }

    function obterLimitesEletrolitosSBP(peso, dia) {
      if (dia <= 5) {
        if (dia <= 2) return { naMin: 0, naMax: 2, kMin: 0, kMax: 3, clMin: 0, clMax: 3 };
        if (dia == 3) return { naMin: 0, naMax: (peso < 1.5 ? 5 : 3), kMin: 0, kMax: 3, clMin: 0, clMax: 3 };
        return { naMin: 2, naMax: 5, kMin: 2, kMax: 3, clMin: 2, clMax: 5 };
      }
      return { naMin: 2, naMax: 5, kMin: 1, kMax: 3, clMin: 2, clMax: 5 };
    }

    function atualizarTigPorTaxa() {
      const peso = parseFloat(document.getElementById('tig_peso').value) || 0;
      const taxa = parseFloat(document.getElementById('tig_taxaHidrica').value) || 0;
      if (peso > 0 && taxa > 0) {
        document.getElementById('tig_volTotal').value = (peso * taxa).toFixed(1);
      }
      calcularTig();
    }

    function calcularTig(manualVolume = false) {
      const peso = parseFloat(document.getElementById('tig_peso').value) || 0;
      const dia = parseInt(document.getElementById('tig_dia').value) || 1;
      const tig = parseFloat(document.getElementById('tig_desejada').value) || 0;
      const tipo = document.getElementById('tig_tipo').value;

      if (peso > 0) {
        const faixa = obterFaixaFluidoSBP(peso, dia, tipo);
        document.getElementById('tig_sugestaoSBP').innerHTML = `💡 Sugestão SBP para este perfil: <strong>${faixa[0]} a ${faixa[1]} mL/kg/dia</strong>`;
      } else {
        document.getElementById('tig_sugestaoSBP').innerText = '💡 Sugestão SBP: Informe o peso do recém-nascido.';
      }

      let taxa = parseFloat(document.getElementById('tig_taxaHidrica').value) || 0;
      let vt = 0;
      if (manualVolume) {
        vt = parseFloat(document.getElementById('tig_volTotal').value) || 0;
        if (peso > 0 && vt > 0) {
          document.getElementById('tig_taxaHidrica').value = (vt / peso).toFixed(1);
        }
      } else {
        vt = peso * taxa;
        if (vt > 0) document.getElementById('tig_volTotal').value = vt.toFixed(1);
      }

      if (peso <= 0 || tig <= 0 || vt <= 0) {
        document.getElementById('tig_resSg5').innerText = '0.0 mL';
        document.getElementById('tig_resG50').innerText = '0.0 mL';
        document.getElementById('tig_resVt').innerText = '0.0 mL';
        document.getElementById('tig_resCg').innerText = '0.0 %';
        return;
      }

      const glicoseTotal = tig * peso * 1.44;
      const glicoseSg5Base = vt * 0.05;
      let vG50 = (glicoseTotal - glicoseSg5Base) / 0.45;
      let vSg5 = vt - vG50;

      if (vG50 < 0) {
        document.getElementById('tig_resSg5').innerText = 'TIG muito baixa';
        document.getElementById('tig_resG50').innerText = '0.0 mL';
        document.getElementById('tig_resCg').innerText = 'N/A';
      } else if (vSg5 < 0) {
        document.getElementById('tig_resSg5').innerText = '0.0 mL';
        document.getElementById('tig_resG50').innerText = 'TIG alta demais';
        document.getElementById('tig_resCg').innerText = 'N/A';
      } else {
        const cg = (glicoseTotal / vt) * 100;
        document.getElementById('tig_resSg5').innerText = `${vSg5.toFixed(1)} mL`;
        document.getElementById('tig_resG50').innerText = `${vG50.toFixed(1)} mL`;
        document.getElementById('tig_resVt').innerText = `${vt.toFixed(1)} mL`;
        document.getElementById('tig_resCg').innerText = `${cg.toFixed(1)} %`;
      }

      const lim = obterLimitesEletrolitosSBP(peso, dia);
      document.getElementById('tig_alvoNa').innerText = `${lim.naMin.toFixed(1)} - ${lim.naMax.toFixed(1)} mmol/kg`;
      document.getElementById('tig_absNa').innerText = `${(lim.naMin * peso).toFixed(2)} - ${(lim.naMax * peso).toFixed(2)} mmol`;

      document.getElementById('tig_alvoK').innerText = `${lim.kMin.toFixed(1)} - ${lim.kMax.toFixed(1)} mmol/kg`;
      document.getElementById('tig_absK').innerText = `${(lim.kMin * peso).toFixed(2)} - ${(lim.kMax * peso).toFixed(2)} mmol`;

      document.getElementById('tig_alvoCl').innerText = `${lim.clMin.toFixed(1)} - ${lim.clMax.toFixed(1)} mmol/kg`;
      document.getElementById('tig_absCl').innerText = `${(lim.clMin * peso).toFixed(2)} - ${(lim.clMax * peso).toFixed(2)} mmol`;
    }

    /* =========================================================================
       5. CATETERISMO UMBILICAL (POP-PB)
       ========================================================================= */
    const POP_CATETER = {
      9:  { baixo: 5.0, alto: 9.0,  venoso: 5.7 },
      10: { baixo: 5.5, alto: 10.5, venoso: 6.5 },
      11: { baixo: 6.3, alto: 11.5, venoso: 7.2 },
      12: { baixo: 7.0, alto: 13.0, venoso: 8.0 },
      13: { baixo: 7.8, alto: 14.0, venoso: 8.5 },
      14: { baixo: 8.5, alto: 15.0, venoso: 9.5 },
      15: { baixo: 9.3, alto: 16.5, venoso: 10.0 },
      16: { baixo: 10.0, alto: 17.5, venoso: 10.5 },
      17: { baixo: 11.0, alto: 19.0, venoso: 11.5 }
    };

    function calcularCateterPeso() {
      const peso = parseFloat(document.getElementById('cat_peso').value) || 0;
      if (peso <= 0) {
        document.getElementById('cat_resVenoso').innerText = '-- cm';
        document.getElementById('cat_resArtAlto').innerText = '-- cm';
        document.getElementById('cat_resArtBaixo').innerText = '-- cm';
        return;
      }
      const comp = ((3 * peso) + 9) / 2 + 1;
      const ombroEst = Math.round(comp * 0.295);
      const chave = Math.max(9, Math.min(17, ombroEst));
      const d = POP_CATETER[chave];

      document.getElementById('cat_resVenoso').innerText = `${d.venoso.toFixed(1)} cm*`;
      document.getElementById('cat_resArtAlto').innerText = `${d.alto.toFixed(1)} cm*`;
      document.getElementById('cat_resArtBaixo').innerText = `${d.baixo.toFixed(1)} cm*`;
    }

    function calcularCateterOmbro() {
      const cm = parseInt(document.getElementById('cat_ombro').value);
      if (!cm || !POP_CATETER[cm]) {
        document.getElementById('cat_resVenoso').innerText = '-- cm';
        document.getElementById('cat_resArtAlto').innerText = '-- cm';
        document.getElementById('cat_resArtBaixo').innerText = '-- cm';
        return;
      }
      const d = POP_CATETER[cm];
      document.getElementById('cat_resVenoso').innerText = `${d.venoso.toFixed(1)} cm`;
      document.getElementById('cat_resArtAlto').innerText = `${d.alto.toFixed(1)} cm`;
      document.getElementById('cat_resArtBaixo').innerText = `${d.baixo.toFixed(1)} cm`;
    }

    /* =========================================================================
       6. GUIA DE DILUIÇÃO IV (BASE COMPLETA)
       ========================================================================= */
    const BANCO_DILUICAO = [
      { nome: "Acetilcisteína", comercial: "Flucistein® 10% (100mg/ml)", rec: "-", dil: "SG 5%", cU: "250 mL*", cM: "100 mL*", vel: "Infusão 1h", nU: null, nM: null, un: "mg" },
      { nome: "Aciclovir", comercial: "Zovirax® 250mg FAP", rec: "10 mL AD", dil: "SF, SG 5%", cU: "4 mg/mL", cM: "7 mg/mL", vel: "60 min", nU: 4, nM: 7, un: "mg" },
      { nome: "Amicacina", comercial: "Amicacina 500mg/2mL", rec: "-", dil: "SF, SG 5%", cU: "5 mg/mL", cM: "10 mg/mL", vel: "60 - 120 min", nU: 5, nM: 10, un: "mg" },
      { nome: "Aminofilina", comercial: "Aminofilina 24mg/mL", rec: "-", dil: "SF, SG 5%", cU: "1 mg/mL", cM: "25 mg/mL", vel: "Infusão 1h", nU: 1, nM: 25, un: "mg" },
      { nome: "Amiodarona", comercial: "Atlansil® 150mg/3mL", rec: "-", dil: "SG 5% exclusivo", cU: "2 mg/mL", cM: "6 mg/mL (CVC)", vel: "IVD 3 min ou >60 min", nU: 2, nM: 6, un: "mg" },
      { nome: "Ampicilina", comercial: "Amplacilina® 500/1000mg", rec: "2-3 mL AD", dil: "SF 0,9%", cU: "10 mg/mL", cM: "30 mg/mL", vel: "15 - 30 min", nU: 10, nM: 30, un: "mg" },
      { nome: "Ampicilina + Sulbactam", comercial: "Unasyn® 1,5g FAP", rec: "3,2 mL AD", dil: "SF, SG 5%", cU: "15 mg/mL", cM: "45 mg/mL", vel: "15 - 30 min", nU: 15, nM: 45, un: "mg" },
      { nome: "Caspofungina", comercial: "Cancidas® 50mg", rec: "10,5 mL AD", dil: "SF 0,9%", cU: "0,2 mg/mL", cM: "0,5 mg/mL", vel: "60 min", nU: 0.2, nM: 0.5, un: "mg" },
      { nome: "Cefazolina", comercial: "Kefazol® 1g FAP", rec: "10 mL AD", dil: "SF, SG 5%", cU: "20 mg/mL", cM: "138 mg/mL", vel: "10 - 60 min", nU: 20, nM: 138, un: "mg" },
      { nome: "Cefepima", comercial: "Maxcef® 1g FAP", rec: "10 mL AD", dil: "SF, SG 5%", cU: "10 mg/mL", cM: "40 mg/mL", vel: "30 min", nU: 10, nM: 40, un: "mg" },
      { nome: "Ceftazidima", comercial: "Fortaz® 1g FAP", rec: "10 mL AD", dil: "SF, SG 5%", cU: "10 mg/mL", cM: "40 mg/mL", vel: "15 - 30 min", nU: 10, nM: 40, un: "mg" },
      { nome: "Ceftriaxona", comercial: "Rocefin® 500mg/1g", rec: "5-10 mL AD", dil: "SF, SG 5%", cU: "10 mg/mL", cM: "40 mg/mL", vel: "10 - 30 min", nU: 10, nM: 40, un: "mg" },
      { nome: "Ciprofloxacina", comercial: "Cipro® 200mg/100mL", rec: "-", dil: "Bolsa pronta", cU: "2 mg/mL", cM: "2 mg/mL", vel: "60 min", nU: 2, nM: 2, un: "mg" },
      { nome: "Clindamicina", comercial: "Dalacin® 300mg/2mL", rec: "-", dil: "SF, SG 5%", cU: "6 mg/mL", cM: "18 mg/mL", vel: "10 - 60 min", nU: 6, nM: 18, un: "mg" },
      { nome: "Cloreto de Potássio 19,1%", comercial: "KCl 19,1% (2,56 mEq/mL)", rec: "-", dil: "SF, SG 5%", cU: "0,08 mEq/mL", cM: "0,15 mEq/mL", vel: "0,3-0,5 mEq/kg/h", nU: 0.08, nM: 0.15, un: "mEq" },
      { nome: "Dexametasona", comercial: "Decadron® 4mg/mL", rec: "-", dil: "SF, SG 5%", cU: "50 mL*", cM: "20 mL*", vel: "IVD 1-4 min ou 15 min", nU: null, nM: null, un: "mg" },
      { nome: "Dipirona", comercial: "Novalgina® 500mg/mL", rec: "-", dil: "SF, SG 5%", cU: "25 mg/mL", cM: "50 mg/mL", vel: "10 - 20 min", nU: 25, nM: 50, un: "mg" },
      { nome: "Dobutamina", comercial: "Dobutrex® 250mg/20mL", rec: "-", dil: "SF, SG 5%", cU: "1 mg/mL", cM: "5 mg/mL", vel: "Contínua", nU: 1, nM: 5, un: "mg" },
      { nome: "Dopamina", comercial: "Revivan® 50mg/10mL", rec: "-", dil: "SF, SG 5%", cU: "1,6 mg/mL", cM: "3,2 mg/mL", vel: "Contínua", nU: 1.6, nM: 3.2, un: "mg" },
      { nome: "Fentanila", comercial: "Fentanil® 50mcg/mL", rec: "-", dil: "SF, SG 5%", cU: "10 mcg/mL", cM: "50 mcg/mL", vel: "IVD 3-5 min ou contínua", nU: 10, nM: 50, un: "mcg" },
      { nome: "Fluconazol", comercial: "Zoltec® 2mg/mL", rec: "-", dil: "Bolsa pronta", cU: "2 mg/mL", cM: "2 mg/mL", vel: "1 - 2 horas", nU: 2, nM: 2, un: "mg" },
      { nome: "Furosemida", comercial: "Lasix® 20mg/2mL", rec: "-", dil: "SF 0,9%", cU: "1 mg/mL", cM: "2 mg/mL", vel: "IVD 0,5 mg/kg/min", nU: 1, nM: 2, un: "mg" },
      { nome: "Gentamicina", comercial: "Garamicina® 40mg/mL", rec: "-", dil: "SF, SG 5%", cU: "5 mg/mL", cM: "10 mg/mL", vel: "30 - 120 min", nU: 5, nM: 10, un: "mg" },
      { nome: "Hidrocortisona", comercial: "Cortisonal® 100mg", rec: "2 mL AD", dil: "SF, SG 5%", cU: "1 mg/mL", cM: "5 mg/mL", vel: "20 - 30 min", nU: 1, nM: 5, un: "mg" },
      { nome: "Meropenem", comercial: "Meronem® 1g FAP", rec: "20 mL AD", dil: "SF, SG 5%", cU: "1 mg/mL", cM: "20 mg/mL", vel: "15 - 30 min", nU: 1, nM: 20, un: "mg" },
      { nome: "Midazolam", comercial: "Dormonid® 5mg/mL", rec: "-", dil: "SF, SG 5%", cU: "1 mg/mL", cM: "5 mg/mL", vel: "IVD 2-5 min", nU: 1, nM: 5, un: "mg" },
      { nome: "Milrinona", comercial: "Primacor® 1mg/mL", rec: "-", dil: "SF, SG 5%", cU: "0,2 mg/mL", cM: "0,5 mg/mL", vel: "Contínua", nU: 0.2, nM: 0.5, un: "mg" },
      { nome: "Morfina", comercial: "Dimorf® 10mg/mL", rec: "-", dil: "SF, SG 5%", cU: "0,5 mg/mL", cM: "5 mg/mL", vel: "15 - 30 min", nU: 0.5, nM: 5, un: "mg" },
      { nome: "Noradrenalina", comercial: "Levophed® 1mg/mL", rec: "-", dil: "SG 5%", cU: "4 mcg/mL", cM: "16 mcg/mL", vel: "Contínua", nU: 4, nM: 16, un: "mcg" },
      { nome: "Ondansetrona", comercial: "Nausedron® 2mg/mL", rec: "-", dil: "SF, SG 5%", cU: "0,5 mg/mL", cM: "1 mg/mL", vel: "15 min", nU: 0.5, nM: 1, un: "mg" },
      { nome: "Oxacilina", comercial: "Staficilin® 500mg", rec: "5 mL AD", dil: "SF, SG 5%", cU: "10 mg/mL", cM: "40 mg/mL (CVC)", vel: "15 - 30 min", nU: 10, nM: 40, un: "mg" },
      { nome: "Piperacilina + Tazobactam", comercial: "Tazocin® 4,5g", rec: "20 mL AD", dil: "SF, SG 5%", cU: "20 mg/mL", cM: "200 mg/mL", vel: "30 min", nU: 20, nM: 200, un: "mg" },
      { nome: "Vancomicina", comercial: "Vancocina® 500mg", rec: "10 mL AD", dil: "SF, SG 5%", cU: "2,5 mg/mL", cM: "5 mg/mL", vel: "Mínimo 60 min", nU: 2.5, nM: 5, un: "mg" }
    ];

    function renderTabelaDiluicao(lista) {
      const tbody = document.getElementById('corpoTabelaDiluicao');
      tbody.innerHTML = '';
      lista.forEach(m => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td><strong>${m.nome}</strong><br><span style="font-size:0.75rem; color:var(--text-muted);">${m.comercial}</span></td>
          <td>${m.rec}</td>
          <td>${m.dil}</td>
          <td><strong>${m.cU}</strong></td>
          <td style="color:#b91c1c;"><strong>${m.cM}</strong></td>
          <td>${m.vel}</td>
          <td><button class="btn btn-outline" style="padding:4px 8px; font-size:0.75rem;" onclick='abrirModalCalcDil(${JSON.stringify(m)})'>Calcular</button></td>
        `;
        tbody.appendChild(tr);
      });
    }

    function filtrarTabelaDiluicao() {
      const q = document.getElementById('filtroDiluicao').value.toLowerCase().trim();
      const filtrados = BANCO_DILUICAO.filter(m => (m.nome + ' ' + m.comercial).toLowerCase().includes(q));
      renderTabelaDiluicao(filtrados);
    }

    function abrirModalCalcDil(med) {
      const dose = prompt(`Digite a dose prescrita de ${med.nome} (${med.un}):`, "100");
      if (!dose) return;
      const val = parseFloat(dose);
      if (isNaN(val) || val <= 0) return;

      let msg = `CÁLCULO DE DILUIÇÃO: ${med.nome} (Dose: ${val} ${med.un})\n\n`;
      if (med.nU) {
        msg += `• Volume Recomendado (Usual): ${(val / med.nU).toFixed(1)} mL (Conc: ${med.cU})\n`;
      }
      if (med.nM) {
        msg += `• Volume Mínimo Permitido (Restrição): ${(val / med.nM).toFixed(1)} mL (Conc: ${med.cM})\n`;
      }
      msg += `• Diluentes compatíveis: ${med.dil}\n• Velocidade recomendada: ${med.vel}`;
      alert(msg);
    }

    /* =========================================================================
       7. INFUSÃO CONTÍNUA
       ========================================================================= */
    const CONCS_INFUSAO = {
      'adrenalina': 1, 'noradrenalina': 1, 'dobutamina': 12.5, 'dopamina': 5,
      'fentanil': 0.05, 'midazolam': 5, 'cetamina': 50, 'milrinona': 1, 'precedex': 0.1
    };

    function aoTrocarDrogaInfusao() {
      const sel = document.getElementById('inf_droga').value;
      document.getElementById('inf_customBox').style.display = (sel === 'custom') ? 'block' : 'none';
      calcularInfusao();
    }

    function calcularInfusao() {
      const peso = parseFloat(document.getElementById('inf_peso').value) || 0;
      const vazao = parseFloat(document.getElementById('inf_vazao').value) || 0;
      const volDroga = parseFloat(document.getElementById('inf_volDroga').value) || 0;
      const volDil = parseFloat(document.getElementById('inf_volDiluente').value) || 0;
      const sel = document.getElementById('inf_droga').value;

      let concEstoque = (sel === 'custom') ? (parseFloat(document.getElementById('inf_customConc').value) || 0) : CONCS_INFUSAO[sel];

      if (peso <= 0 || vazao <= 0 || (volDroga + volDil) <= 0 || concEstoque <= 0) {
        document.getElementById('inf_resMcgKgMin').innerText = '--';
        document.getElementById('inf_resMcgKgH').innerText = '--';
        document.getElementById('inf_resMgKgH').innerText = '--';
        return;
      }

      const volTotal = volDroga + volDil;
      const totalMg = volDroga * concEstoque;
      const concFinalMgMl = totalMg / volTotal;

      const mgH = vazao * concFinalMgMl;
      const mgKgH = mgH / peso;
      const mcgKgH = mgKgH * 1000;
      const mcgKgMin = mcgKgH / 60;

      document.getElementById('inf_resMcgKgMin').innerText = mcgKgMin.toFixed(3);
      document.getElementById('inf_resMcgKgH').innerText = mcgKgH.toFixed(3);
      document.getElementById('inf_resMgKgH').innerText = mgKgH.toFixed(4);
      document.getElementById('inf_resDetalhes').innerText = `Solução: ${volTotal.toFixed(1)} mL | Concentração: ${concFinalMgMl.toFixed(3)} mg/mL`;
    }

    /* =========================================================================
       8. DOSES INTERMITENTES
       ========================================================================= */
    const BANCO_INTERMITENTE = [
      { n:"Aciclovir", d:10, i:"8/8h", m:800, v:"EV", dil:"SF 0,9% (≤5 mg/mL)", t:"60 min", o:"Hidratar; monitorar creatinina", dRN:20, iRN:"8/8h" },
      { n:"Amicacina", d:15, i:"24/24h", m:1000, v:"EV", dil:"SF ou SG 5%", t:"30–60 min", o:"Nefro e ototoxicidade", dRN:15, iRN:"conforme IG" },
      { n:"Ampicilina", d:50, i:"6/6h", m:2000, v:"EV", dil:"SF 0,9%", t:"15–30 min", o:"Meningite: 100 mg/kg/dose", dRN:50, iRN:"12/12h (<7d) ou 8/8h" },
      { n:"Cefazolina", d:25, i:"8/8h", m:2000, v:"EV", dil:"SF 0,9%", t:"15–30 min", o:"Profilaxia e infecções de pele" },
      { n:"Ceftriaxona", d:75, i:"24/24h", m:2000, v:"EV", dil:"SF ou SG 5%", t:"15–30 min", o:"Contraindicado com cálcio em RN" },
      { n:"Dipirona", d:15, i:"6/6h", m:1000, v:"EV", dil:"SF 0,9%", t:"10–15 min", o:"Infundir lentamente (risco hipotensão)" },
      { n:"Furosemida", d:1, i:"8/8h ou 12/12h", m:20, v:"EV", dil:"SF 0,9%", t:"5–10 min", o:"Monitorar potássio" },
      { n:"Gentamicina", d:7.5, i:"24/24h", m:500, v:"EV", dil:"SF ou SG 5%", t:"30–60 min", o:"Monitorar função renal", dRN:4, iRN:"24/24h" },
      { n:"Meropenem", d:20, i:"8/8h", m:2000, v:"EV", dil:"SF 0,9%", t:"15–30 min", o:"Meningite: 40 mg/kg/dose" },
      { n:"Midazolam", d:0.075, i:"2/2h a 4/4h", m:5, v:"EV", dil:"SF 0,9%", t:"2–5 min", o:"Alta vigilância; depressão respiratória" },
      { n:"Morfina", d:0.075, i:"3/3h a 4/4h", m:10, v:"EV", dil:"SF 0,9%", t:"5 min", o:"Alta vigilância" },
      { n:"Ondansetrona", d:0.15, i:"8/8h", m:8, v:"EV", dil:"SF 0,9%", t:"15 min", o:"Antiémetico" },
      { n:"Oxacilina", d:50, i:"6/6h", m:2000, v:"EV", dil:"SF 0,9%", t:"15–30 min", o:"Estafilococo oxa-sensível" },
      { n:"Piperacilina + Tazobactam", d:75, i:"6/6h", m:4000, v:"EV", dil:"SF 0,9%", t:"30 min", o:"Ajustar se insuficiência renal" },
      { n:"Vancomicina", d:15, i:"6/6h", m:1000, v:"EV", dil:"SF 0,9% (≤5 mg/mL)", t:"≥60 min", o:"Risco Síndrome Homem Vermelho", dRN:10, iRN:"conforme IG" }
    ];

    let drogaIntermitenteSel = null;

    function renderListaIntermitente(lista) {
      const box = document.getElementById('drg_lista');
      box.innerHTML = '';
      lista.forEach(d => {
        const item = document.createElement('div');
        item.style.cssText = 'padding:6px 10px; cursor:pointer; font-size:0.82rem; border-bottom:1px solid #f1f5f9;';
        item.innerText = `${d.n} (${d.d} mg/kg)`;
        item.onclick = () => {
          drogaIntermitenteSel = d;
          document.querySelectorAll('#drg_lista div').forEach(el => el.style.background = '#fff');
          item.style.background = '#eff6ff';
          item.style.fontWeight = '700';
        };
        box.appendChild(item);
      });
    }

    function filtrarDrogasIntermitentes() {
      const q = document.getElementById('drg_busca').value.toLowerCase().trim();
      renderListaIntermitente(BANCO_INTERMITENTE.filter(d => d.n.toLowerCase().includes(q)));
    }

    function calcularDrogasIntermitentes() {
      if (!drogaIntermitenteSel) { alert('Selecione um medicamento da lista.'); return; }
      const peso = parseFloat(document.getElementById('drg_peso').value);
      if (isNaN(peso) || peso <= 0) { alert('Informe o peso do paciente.'); return; }

      const idVal = parseFloat(document.getElementById('drg_idadeVal').value);
      const idUnid = document.getElementById('drg_idadeUnid').value;
      const ig = parseFloat(document.getElementById('drg_ig').value);
      const dil = parseFloat(document.getElementById('drg_diluente').value);

      const d = drogaIntermitenteSel;
      const ehRN = (!isNaN(idVal) && idUnid === 'dias' && idVal <= 28) || !isNaN(ig);
      const doseMgKg = (ehRN && d.dRN) ? d.dRN : d.d;
      const intervalo = (ehRN && d.iRN) ? d.iRN : d.i;

      const doseTotal = peso * doseMgKg;
      const acimaMax = (d.m && doseTotal > d.m);

      document.getElementById('drg_calcDetalhes').innerHTML = `
        <strong>${d.n}</strong> — Dose Calculada: <strong>${doseTotal.toFixed(1)} mg</strong> (${doseMgKg} mg/kg &times; ${peso} kg)<br>
        Intervalo: <strong>${intervalo}</strong> | Via: <strong>${d.v}</strong> | Tempo: <strong>${d.t}</strong><br>
        ${d.m ? `Dose Máxima de Referência: ${d.m} mg ` + (acimaMax ? '<span style="color:#b91c1c; font-weight:700;">(⚠️ ACIMA DO LIMITE MÁXIMO)</span>' : '✅') : ''}
        ${ehRN && d.dRN ? '<br><span style="color:#b45309; font-size:0.8rem;">⚠️ Ajuste neonatal aplicado conforme IG/idade pós-natal.</span>' : ''}
      `;

      let presc = `${d.n} ${doseTotal.toFixed(1)} mg EV ${intervalo}. `;
      if (!isNaN(dil) && dil > 0) presc += `Diluir em ${dil} mL de ${d.dil} e infundir em ${d.t}. `;
      else presc += `Diluir em ${d.dil} e correr em ${d.t}. `;
      presc += `[Dose: ${doseMgKg} mg/kg/dose, Peso: ${peso} kg].`;

      document.getElementById('drg_textoPrescricao').value = presc;
      document.getElementById('drg_resultadoBox').style.display = 'block';
    }

    window.addEventListener('DOMContentLoaded', () => {
      calcularPim2();
      calcularBH();
      calcularIntergrowth();
      calcularTig();
      calcularCateterPeso();
      renderTabelaDiluicao(BANCO_DILUICAO);
      calcularInfusao();
      renderListaIntermitente(BANCO_INTERMITENTE);

      const saved = localStorage.getItem('hub_gem_link');
      if (saved) {
        document.getElementById('linkGemCustom').value = saved;
      }
    });
  </script>
</body>
</html>
