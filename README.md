# C-digo_vivi
Jogos de desenvolvimento e construção 
<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<title>Código Vivo - Profissional com Skins</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<link rel="manifest" href="manifest.json">
<style>
body { font-family: Arial, sans-serif; background-color: #f0f8ff; text-align: center; margin:0; padding:0; }
h1 { color: #0a0a0a; margin-top: 10px; font-size: 24px; }
#setores { margin: 20px auto; width: 95%; max-width: 800px; display: flex; flex-wrap: wrap; justify-content: center; }
.setor { width: 18%; min-width: 60px; height: 60px; display: flex; justify-content:center; align-items:center; margin:5px; font-weight:bold; color:white; background-color:#555; border-radius:10px; transition:0.3s; font-size:16px; }
.aceso { background-color:#4CAF50 !important; }
.bloco { display:inline-block; padding:8px 12px; margin:5px; background-color:#2196F3; color:white; border-radius:5px; cursor:pointer; user-select:none; font-size:14px; }
.bloco-loop { background-color:#FF9800; }
.bloco-func { background-color:#9C27B0; }
#areaCodigo { min-height:150px; border:2px dashed #333; margin:10px auto; width:90%; max-width:800px; padding:10px; background-color:#e6f2ff; border-radius:8px; text-align:left; }
button { padding:10px 20px; font-size:16px; margin-top:10px; border:none; border-radius:5px; background-color:#2196F3; color:white; cursor:pointer; }
button:hover { background-color:#1976D2; }
#mensagem { margin-top:15px; font-weight:bold; white-space:pre-line; }
#pontuacao { margin-top:10px; font-weight:bold; color:#333; }
#personagem { margin-top:15px; font-weight:bold; color:#0a0a0a; }
#idiomaSelect { margin-top:10px; font-size:16px; padding:5px; border-radius:5px; border:1px solid #333; }
#skinsMenu { margin:10px auto; width:90%; max-width:800px; }
</style>
</head>
<body>

<h1>Código Vivo - Profissional com Skins</h1>

<select id="idiomaSelect" onchange="trocarIdioma()">
  <option value="pt">Português</option>
  <option value="en">English</option>
  <option value="es">Español</option>
  <option value="fr">Français</option>
</select>

<p id="nivelDescricao"></p>

<div id="setores">
  <div id="setor1" class="setor">1</div>
  <div id="setor2" class="setor">2</div>
  <div id="setor3" class="setor">3</div>
  <div id="setor4" class="setor">4</div>
  <div id="setor5" class="setor">5</div>
</div>

<h3 id="blocosTitulo">Blocos de código:</h3>
<div id="blocos"></div>

<h3 id="areaTitulo">Área de código:</h3>
<div id="areaCodigo"></div>
<button onclick="executarCodigo()" id="executarBtn">Executar Código</button>

<div id="mensagem"></div>
<div id="pontuacao"></div>
<div id="personagem"></div>

<h3>Menu de Skins</h3>
<div id="skinsMenu"></div>

<script>
// Idiomas
const textos = {
  pt: {blocos:"Blocos de código:", area:"Área de código:", executar:"Executar Código", personagem:"Personagem:"},
  en: {blocos:"Code Blocks:", area:"Code Area:", executar:"Run Code", personagem:"Character:"},
  es: {blocos:"Bloques de código:", area:"Área de código:", executar:"Ejecutar código", personagem:"Personaje:"},
  fr: {blocos:"Blocs de code:", area:"Zone de code:", executar:"Exécuter le code", personagem:"Personnage:"}
};
let idioma="pt";
function trocarIdioma(){ idioma = document.getElementById("idiomaSelect").value; atualizarTexto(); }
function atualizarTexto(){
  document.getElementById("blocosTitulo").textContent = textos[idioma].blocos;
  document.getElementById("areaTitulo").textContent = textos[idioma].area;
  document.getElementById("executarBtn").textContent = textos[idioma].executar;
  document.getElementById("personagem").textContent = textos[idioma].personagem + " " + personagemAtual;
}

// Níveis e narrativa
const niveis = [
  {descricao:{pt:"Nível 1: Acenda o Setor 1",en:"Level 1: Light Sector 1",es:"Nivel 1: Encender Sector 1",fr:"Niveau 1: Allumer Secteur 1"}, setores:[1], instrucoes:["se setor1 = 'apagado' então acender setor1"], personagem:"Loopus"},
  {descricao:{pt:"Nível 2: Acenda Setores 1 e 2",en:"Level 2: Light Sectors 1 and 2",es:"Nivel 2: Encender Sectores 1 y 2",fr:"Niveau 2: Allumer Secteurs 1 et 2"}, setores:[1,2], instrucoes:["se setor1 = 'apagado' então acender setor1","se setor2 = 'apagado' então acender setor2"], personagem:"Condy"},
  {descricao:{pt:"Nível 3: Acenda Setores 1 a 3 com loop",en:"Level 3: Light Sectors 1-3 with loop",es:"Nivel 3: Encender Sectores 1-3 con loop",fr:"Niveau 3: Allumer Secteurs 1-3 avec boucle"}, setores:[1,2,3], instrucoes:["para cada setor se apagado então acender setor"], personagem:"Varis"},
  {descricao:{pt:"Nível 4: Acenda Setores 1 a 4 com função",en:"Level 4: Light Sectors 1-4 with function",es:"Nivel 4: Encender Sectores 1-4 con función",fr:"Niveau 4: Allumer Secteurs 1-4 avec fonction"}, setores:[1,2,3,4], instrucoes:["func acenderTodos() { para cada setor se apagado então acender setor }"], personagem:"Loopus"},
  {descricao:{pt:"Nível 5: Acenda todos os 5 setores e salve a cidade!",en:"Level 5: Light all 5 sectors and save city!",es:"Nivel 5: Encender los 5 sectores y salvar la ciudad!",fr:"Niveau 5: Allumer les 5 secteurs et sauver la ville!"}, setores:[1,2,3,4,5], instrucoes:["para cada setor se apagado então acender setor","salvar cidade"], personagem:"Condy"}
];

let nivelAtual = localStorage.getItem('nivelAtual') ? parseInt(localStorage.getItem('nivelAtual')) : 0;
let pontos = localStorage.getItem('pontos') ? parseInt(localStorage.getItem('pontos')) : 0;
let personagemAtual="";

// Skins
const skins = [
  {id:1, nome:"Verde Clássico", cor:"#4CAF50", preco:0},
  {id:2, nome:"Azul Neon", cor:"#2196F3", preco:0.99},
  {id:3, nome:"Vermelho Fogo", cor:"#F44336", preco:0.99},
  {id:4, nome:"Roxo Misterioso", cor:"#9C27B0", preco:1.99}
];
let skinsCompradas = JSON.parse(localStorage.getItem('skinsCompradas')) || [1];

function mostrarSkins(){
  const menu = document.getElementById('skinsMenu');
  menu.innerHTML = "";
  skins.forEach(skin=>{
    const div = document.createElement('div');
    div.style.display="inline-block";
    div.style.margin="5px";
    div.style.padding="5px 10px";
    div.style.border="1px solid #333";
    div.style.cursor="pointer";
    div.style.backgroundColor=skin.cor;
    div.textContent=skin.nome + (skinsCompradas.includes(skin.id)?" ✅":" 💰$"+skin.preco);
    div.onclick = ()=>{ aplicarSkin(skin) };
    menu.appendChild(div);
  });
}

function aplicarSkin(skin){
  if(!skinsCompradas.includes(skin.id)){
    if(confirm(`Comprar skin "${skin.nome}" por $${skin.preco}?`)){
      skinsCompradas.push(skin.id);
      localStorage.setItem('skinsCompradas', JSON.stringify(skinsCompradas));
      alert(`Skin "${skin.nome}" desbloqueada!`);
    } else return;
  }
  for(let i=1;i<=5;i++){
    const setor = document.getElementById("setor"+i);
    if(setor.classList.contains("aceso")){
      setor.style.backgroundColor=skin
