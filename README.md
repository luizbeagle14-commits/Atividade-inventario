<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Atividade Prática - Inventário e Acuracidade de Estoque</title>
<style>
  body {
    font-family: "Segoe UI", sans-serif;
    background: #f4f6f9;
    margin: 0;
    padding: 20px;
  }
  h1 { text-align: center; color: #1a237e; }
  h2 { color: #303f9f; margin-top: 30px; }
  .container {
    max-width: 950px;
    margin: 0 auto;
    background: white;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 0 15px rgba(0,0,0,0.1);
  }
  label { font-weight: bold; }
  input[type="text"], input[type="number"], select {
    padding: 6px;
    margin: 4px;
    border-radius: 6px;
    border: 1px solid #ccc;
    width: 100%;
  }
  button {
    background: #3949ab;
    color: white;
    border: none;
    padding: 10px 20px;
    margin: 8px 0;
    border-radius: 8px;
    cursor: pointer;
  }
  button:hover { background: #5c6bc0; }
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
  }
  th, td {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
  }
  th { background: #e8eaf6; }
  #ranking, #resultado, #medalha, #feedbackInventario, #feedbackDesafio {
    margin-top: 20px;
    text-align: center;
    font-weight: bold;
  }
  .medalha { font-size: 28px; }
  .fase2, .fase3 {
    background: #f1f8e9;
    padding: 15px;
    border-radius: 10px;
    margin-top: 25px;
  }
  .correto { color: green; font-weight: bold; }
  .errado { color: red; font-weight: bold; }
  .explicacao {
    font-size: 0.9em;
    background: #f9fbe7;
    border-left: 4px solid #9ccc65;
    padding: 8px;
    margin-top: 5px;
    border-radius: 6px;
  }
  /* Certificado */
  #certificado {
    display: none;
    text-align: center;
    border: 8px double #3949ab;
    padding: 40px;
    background: white;
    max-width: 800px;
    margin: 30px auto;
    border-radius: 20px;
    box-shadow: 0 0 25px rgba(0,0,0,0.15);
  }
  #certificado h1 { color: #1a237e; margin-bottom: 10px; }
  #certificado p { font-size: 18px; }
  #assinatura {
    margin-top: 40px;
    text-align: right;
    font-style: italic;
  }
</style>
</head>
<body>

<div class="container">
  <h1>Atividade Prática: Inventário e Acuracidade de Estoque</h1>
  <p><strong>Professor:</strong> Luiz Eduardo Peixoto</p>

  <label>Nome do participante:</label>
  <input type="text" id="nomeAluno" placeholder="Digite seu nome">

  <div id="ranking">
    <h3>🏅 Ranking Local</h3>
    <ol id="listaRanking"></ol>
  </div>

  <div id="cronometro">⏱ Tempo: <span id="tempo">0</span> s</div>
  <button id="iniciarBtn" onclick="iniciarAtividade()">Iniciar Atividade</button>
  <button id="finalizarBtn" onclick="finalizarAtividade()" disabled>Finalizar Atividade</button>

  <!-- Fase 1 -->
  <h2>🧮 Fase 1 - Cálculo de Acuracidade</h2>
  <p>Preencha a quantidade física e veja a acuracidade calculada automaticamente.</p>

  <table id="tabelaInventario">
    <thead>
      <tr>
        <th>Produto</th>
        <th>Qtd. no Sistema</th>
        <th>Qtd. Física</th>
        <th>Acuracidade (%)</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Parafuso 4x20</td><td>120</td><td><input type="number" min="0" onchange="calcularAcuracidade(this)"></td><td class="resultado"></td></tr>
      <tr><td>Porca M6</td><td>200</td><td><input type="number" min="0" onchange="calcularAcuracidade(this)"></td><td class="resultado"></td></tr>
      <tr><td>Arruela Lisa 8mm</td><td>150</td><td><input type="number" min="0" onchange="calcularAcuracidade(this)"></td><td class="resultado"></td></tr>
      <tr><td>Chave Allen 6mm</td><td>80</td><td><input type="number" min="0" onchange="calcularAcuracidade(this)"></td><td class="resultado"></td></tr>
    </tbody>
  </table>

  <div id="resultado"></div>
  <div id="medalha" class="medalha"></div>

  <!-- Fase 2 -->
  <div class="fase2">
    <h2>📋 Fase 2 - Tipos de Inventário</h2>
    <p>Escolha o tipo de inventário em cada caso e veja o feedback didático.</p>

    <div>
      <p><strong>1️⃣</strong> Contagem total feita apenas em dezembro para o fechamento fiscal.</p>
      <select id="inv1">
        <option value="">Selecione</option>
        <option value="anual">Anual</option>
        <option value="rotativo">Rotativo</option>
        <option value="cíclico">Cíclico</option>
        <option value="dinâmico">Dinâmico</option>
      </select>
      <div id="exp1" class="explicacao"></div>
    </div>

    <div>
      <p><strong>2️⃣</strong> Contagem semanal por setor, para manter acuracidade constante.</p>
      <select id="inv2">
        <option value="">Selecione</option>
        <option value="anual">Anual</option>
        <option value="rotativo">Rotativo</option>
        <option value="cíclico">Cíclico</option>
        <option value="dinâmico">Dinâmico</option>
      </select>
      <div id="exp2" class="explicacao"></div>
    </div>

    <div>
      <p><strong>3️⃣</strong> Varejo realiza inventários rápidos alternando setores diariamente.</p>
      <select id="inv3">
        <option value="">Selecione</option>
        <option value="anual">Anual</option>
        <option value="rotativo">Rotativo</option>
        <option value="cíclico">Cíclico</option>
        <option value="dinâmico">Dinâmico</option>
      </select>
      <div id="exp3" class="explicacao"></div>
    </div>

    <div>
      <p><strong>4️⃣</strong> Distribuidora realiza levantamentos trimestrais.</p>
      <select id="inv4">
        <option value="">Selecione</option>
        <option value="anual">Anual</option>
        <option value="rotativo">Rotativo</option>
        <option value="cíclico">Cíclico</option>
        <option value="dinâmico">Dinâmico</option>
      </select>
      <div id="exp4" class="explicacao"></div>
    </div>

    <button onclick="verificarInventario()">Verificar Respostas</button>
    <div id="feedbackInventario"></div>
  </div>

  <!-- Fase 3 -->
  <div class="fase3">
    <h2>🏁 Fase 3 - Desafio Final</h2>
    <p>Uma empresa possui:</p>
    <ul>
      <li>Estoque no sistema: 5.000 unidades</li>
      <li>Estoque físico: 4.850 unidades</li>
    </ul>
    <p>Calcule a acuracidade total do estoque:</p>

    <input type="number" id="respostaDesafio" placeholder="Digite aqui (ex: 97)">
    <button onclick="verificarDesafio()">Verificar Resposta</button>
    <div id="feedbackDesafio"></div>
  </div>

  <div style="text-align:center; margin-top:30px;">
    <button onclick="gerarCertificado()">🎓 Gerar Certificado</button>
  </div>
</div>

<!-- Certificado -->
<div id="certificado">
  <h1>Certificado de Conclusão</h1>
  <p>Certificamos que <strong id="nomeCert"></strong></p>
  <p>concluiu com êxito a atividade prática:</p>
  <p><em>“Inventário e Acuracidade de Estoque”</em></p>
  <p id="medalhaCert" style="font-size:24px; margin-top:20px;"></p>
  <p><small>Emitido em: <span id="dataCert"></span></small></p>
  <div id="assinatura">
    ___________________________<br>
    <b>Prof. Luiz Eduardo Peixoto</b>
  </div>
</div>

<script>
let tempo = 0, cronometro, medalhaAtual = "";

function iniciarAtividade() {
  const nome = document.getElementById('nomeAluno').value.trim();
  if (!nome) return alert("Digite seu nome antes de começar!");
  document.getElementById('iniciarBtn').disabled = true;
  document.getElementById('finalizarBtn').disabled = false;
  cronometro = setInterval(() => document.getElementById('tempo').innerText = ++tempo, 1000);
}

function calcularAcuracidade(input) {
  const linha = input.parentElement.parentElement;
  const qtdSistema = parseFloat(linha.children[1].innerText);
  const qtdFisica = parseFloat(input.value);
  if (!isNaN(qtdFisica))
    linha.querySelector('.resultado').innerText = ((qtdFisica / qtdSistema) * 100).toFixed(1) + '%';
}

function finalizarAtividade() {
  clearInterval(cronometro);
  document.getElementById('finalizarBtn').disabled = true;
  const resultados = [...document.querySelectorAll('.resultado')].map(td => parseFloat(td.innerText) || 0);
  const media = resultados.reduce((a,b)=>a+b,0) / resultados.length;
  if (media >= 95) medalhaAtual = '🥇 Medalha de Ouro - Excelente Acuracidade!';
  else if (media >= 85) medalhaAtual = '🥈 Medalha de Prata - Boa Gestão!';
  else medalhaAtual = '🥉 Medalha de Bronze - Pode Melhorar!';
  document.getElementById('resultado').innerHTML = `<p>Acuracidade média: <strong>${media.toFixed(1)}%</strong></p>`;
  document.getElementById('medalha').innerText = medalhaAtual;
  atualizarRanking(document.getElementById('nomeAluno').value, media);
}

function verificarInventario() {
  const corretas = ['anual','rotativo','dinâmico','cíclico'];
  const explicacoes = {
    'anual': '📘 Anual: realizado 1x ao ano, normalmente no encerramento fiscal.',
    'rotativo': '🔄 Rotativo: ocorre semanalmente, alternando setores.',
    'cíclico': '📅 Cíclico: feito em períodos regulares, como trimestralmente.',
    'dinâmico': '⚙️ Dinâmico: contínuo e setorizado, típico de grandes varejos.'
  };
  let acertos = 0;
  for (let i = 1; i <= 4; i++) {
    const resposta = document.getElementById(`inv${i}`).value;
    const exp = document.getElementById(`exp${i}`);
    if (resposta === corretas[i-1]) {
      exp.innerHTML = `<span class='correto'>✅ Correto!</span> ${explicacoes[resposta]}`;
      acertos++;
    } else if (resposta) {
      exp.innerHTML = `<span class='errado'>❌ Errado.</span> ${explicacoes[resposta]}<br><b>Correto:</b> ${explicacoes[corretas[i-1]]}`;
    } else exp.innerHTML = `<span class='errado'>⚠️ Não respondido.</span>`;
  }
  document.getElementById('feedbackInventario').innerHTML =
    `<br>Você acertou ${acertos}/4 questões.<br>` +
    (acertos === 4 ? '🏆 Excelente domínio dos tipos de inventário!' :
     acertos >= 2 ? '💪 Bom desempenho! Revise os conceitos que faltaram.' :
     '📘 Estude novamente e tente outra vez!');
}

function verificarDesafio() {
  const resposta = parseFloat(document.getElementById('respostaDesafio').value);
  const correta = ((4850 / 5000) * 100).toFixed(1);
  const f = document.getElementById('feedbackDesafio');
  if (isNaN(resposta)) return f.innerHTML = "⚠️ Digite um valor numérico!";
  if (Math.abs(resposta - correta) <= 0.5)
    f.innerHTML = `✅ Correto! A acuracidade é <b>${correta}%</b>.<br><div class='explicacao'>(4850 ÷ 5000) × 100 = 97%</div>`;
  else
    f.innerHTML = `❌ Errado. A resposta certa é <b>${correta}%</b>.<br><div class='explicacao'>A acuracidade mede a fidelidade entre o estoque físico e o registrado no sistema.</div>`;
}

function gerarCertificado() {
  const nome = document.getElementById('nomeAluno').value.trim();
  if (!nome) return alert("Digite seu nome para gerar o certificado!");
  const data = new Date().toLocaleString('pt-BR');
  document.getElementById('nomeCert').innerText = nome;
  document.getElementById('medalhaCert').innerText = medalhaAtual || '🎖 Participante da Atividade';
  document.getElementById('dataCert').innerText = data;
  document.getElementById('certificado').style.display = "block";
  window.print();
}

function atualizarRanking(nome, media) {
  const ranking = JSON.parse(localStorage.getItem('rankingInventario') || '[]');
  ranking.push({ nome, media });
  ranking.sort((a,b)=>b.media - a.media);
  localStorage.setItem('rankingInventario', JSON.stringify(ranking));
  exibirRanking();
}

function exibirRanking() {
  const ranking = JSON.parse(localStorage.getItem('rankingInventario') || '[]');
  const lista = document.getElementById('listaRanking');
  lista.innerHTML = '';
  ranking.slice(0,5).forEach((r, i) => {
    const li = document.createElement('li');
    li.textContent = `${i+1}. ${r.nome} - ${r.media.toFixed(1)}%`;
    lista.appendChild(li);
  });
}

window.onload = exibirRanking;
</script>

</body>
</html>


