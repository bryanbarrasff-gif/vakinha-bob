<title>Vakinha do Bob</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,600;12..96,800&family=Inter:wght@400;500;600&display=swap">
<style>
:root {
  --bg: #f2f6f4;
  --surface: #ffffff;
  --fg: #12231f;
  --muted: #55675f;
  --line: #d3ded9;
  --accent: #0b6b5d;
  --accent-fg: #ffffff;
  --fill: #f0b400;
  --font-display: "Bricolage Grotesque", "Inter", system-ui, sans-serif;
  --font-body: "Inter", system-ui, -apple-system, "Segoe UI", sans-serif;
}
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0e1816; --surface: #16231f; --fg: #e9f1ee; --muted: #9db0a8;
    --line: #29403a; --accent: #4fd1b9; --accent-fg: #06201b; --fill: #f5c33b;
    color-scheme: dark;
  }
}
* { box-sizing: border-box; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--fg);
  font-family: var(--font-body);
  font-size: 16px;
  line-height: 1.6;
  padding: 40px 16px 56px;
}
main { max-width: 560px; margin: 0 auto; display: flex; flex-direction: column; gap: 28px; }
.eyebrow { font-size: 13px; font-weight: 600; letter-spacing: 0.08em; text-transform: uppercase; color: var(--accent); margin: 0; }
h1 {
  font-family: var(--font-display);
  font-weight: 800;
  font-size: clamp(64px, 22vw, 120px);
  line-height: 0.95;
  letter-spacing: -0.03em;
  margin: 8px 0 0;
}
.lead { font-size: 18px; margin: 16px 0 0; max-width: 46ch; }
.card { background: var(--surface); border: 1px solid var(--line); border-radius: 14px; padding: 22px; }
.goal-row { display: flex; justify-content: space-between; align-items: baseline; gap: 12px; flex-wrap: wrap; }
.raised { font-family: var(--font-display); font-weight: 800; font-size: 34px; letter-spacing: -0.02em; }
.goal { color: var(--muted); font-size: 15px; }
.bar { height: 14px; border-radius: 7px; background: var(--line); overflow: hidden; margin-top: 14px; }
.bar > span { display: block; height: 100%; width: 0; background: var(--fill); border-radius: 7px; transition: width 0.6s ease; }
.bar-note { margin: 10px 0 0; font-size: 14px; color: var(--muted); }
h2 { font-family: var(--font-display); font-weight: 600; font-size: 22px; margin: 0 0 4px; letter-spacing: -0.01em; }
.sub { margin: 0 0 16px; color: var(--muted); font-size: 15px; }
.pix { display: flex; flex-direction: column; gap: 12px; }
.pix-key {
  font-family: ui-monospace, Menlo, Consolas, monospace;
  font-size: 16px;
  background: var(--bg);
  border: 1px dashed var(--line);
  border-radius: 10px;
  padding: 14px;
  word-break: break-all;
  user-select: all;
  -webkit-user-select: all;
}
.pix-meta { display: flex; justify-content: space-between; gap: 12px; flex-wrap: wrap; font-size: 13px; color: var(--muted); }
button.copy {
  appearance: none; border: 0; cursor: pointer;
  background: var(--accent); color: var(--accent-fg);
  font: 600 16px var(--font-body);
  padding: 15px 20px; border-radius: 10px; width: 100%;
}
.steps { margin: 0; padding-left: 20px; font-size: 15px; }
.steps li { margin-bottom: 6px; }
.share { font-size: 14px; color: var(--muted); margin: 0; }
</style>

<main>
  <header>
    <p class="eyebrow">Vakinha</p>
    <h1>Bob</h1>
    <p class="lead">Estou arrecadando para comprar ração para o Bob. Qualquer valor ajuda a encher a tigela dele.</p>
  </header>

  <section class="card">
    <div class="goal-row">
      <span class="raised" id="raised">R$ 0</span>
      <span class="goal">meta de <strong id="goal">R$ 100</strong></span>
    </div>
    <div class="bar"><span id="fill"></span></div>
    <p class="bar-note" id="note"></p>
  </section>

  <section class="card pix">
    <div>
      <h2>Doe por Pix</h2>
      <p class="sub">Copie a chave abaixo e cole no app do seu banco, na opção Pix.</p>
    </div>
    <div class="pix-key" id="pixkey">teste123@gmail.com</div>
    <div class="pix-meta"><span>Tipo: e-mail</span><span>Cai direto na conta do tutor</span></div>
    <button class="copy" id="copy" type="button">Copiar chave Pix</button>
  </section>

  <section class="card">
    <h2>Como doar</h2>
    <ol class="steps">
      <li>Toque em copiar chave Pix.</li>
      <li>Abra o app do seu banco e escolha Pix, depois Pix Copia e Cola ou Chave.</li>
      <li>Cole a chave, digite o valor que quiser e confirme.</li>
    </ol>
  </section>

  <p class="share">Obrigado por ajudar o Bob. Compartilhar esta página também ajuda.</p>
</main>

<script>
  // Ajuste aqui quando receber doações.
  var META = 100;
  var ARRECADADO = 0;

  function brl(v) { return "R$ " + v.toLocaleString("pt-BR", { minimumFractionDigits: v % 1 ? 2 : 0, maximumFractionDigits: 2 }); }

  var pct = Math.min(100, Math.round((ARRECADADO / META) * 100));
  document.getElementById("raised").textContent = brl(ARRECADADO);
  document.getElementById("goal").textContent = brl(META);
  document.getElementById("note").textContent = ARRECADADO >= META
    ? "Meta atingida. Obrigado a todos!"
    : "Ainda faltam " + brl(META - ARRECADADO) + " para chegar na meta.";
  requestAnimationFrame(function () { document.getElementById("fill").style.width = pct + "%"; });

  var btn = document.getElementById("copy");
  var key = document.getElementById("pixkey");
  function selectKey() {
    var r = document.createRange(); r.selectNodeContents(key);
    var s = window.getSelection(); s.removeAllRanges(); s.addRange(r);
  }
  btn.addEventListener("click", function () {
    var done = function () { btn.textContent = "Chave copiada!"; setTimeout(function () { btn.textContent = "Copiar chave Pix"; }, 2200); };
    var fail = function () { selectKey(); btn.textContent = "Selecionada: toque em copiar"; };
    try {
      navigator.clipboard.writeText(key.textContent.trim()).then(done, fail);
    } catch (e) { fail(); }
  });
</script>
