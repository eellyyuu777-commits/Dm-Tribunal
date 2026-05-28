<!DOCTYPE html>
<html lang="fr">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>DM Tribunal AI</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Inter,sans-serif;
}

body{
background:#06060a;
color:white;
overflow-x:hidden;
}

/* =========================================================
BACKGROUND
========================================================= */

body::before{
content:"";
position:fixed;
inset:0;
background:
radial-gradient(circle at top left,#ff2f92 0%,transparent 35%),
radial-gradient(circle at bottom right,#7b2fff 0%,transparent 35%);
opacity:0.16;
z-index:-2;
}

body::after{
content:"";
position:fixed;
inset:0;
backdrop-filter:blur(120px);
z-index:-1;
}

/* =========================================================
HEADER
========================================================= */

header{
position:fixed;
top:0;
left:0;
width:100%;
padding:24px 8%;
display:flex;
justify-content:space-between;
align-items:center;
z-index:999;
background:rgba(6,6,10,0.65);
backdrop-filter:blur(18px);
border-bottom:1px solid rgba(255,255,255,0.05);
}

.logo{
display:flex;
align-items:center;
gap:12px;
font-size:28px;
font-weight:700;
color:#ff5eb5;
}

.logo span{
font-size:32px;
color:#d7d7d7;
}

nav{
display:flex;
align-items:center;
gap:20px;
}

nav button{
background:none;
border:none;
color:#cfcfcf;
font-size:15px;
cursor:pointer;
transition:0.3s;
}

nav button:hover{
color:#ff5eb5;
}

.main-btn{
background:
linear-gradient(
90deg,
#ff4fa3,
#ff7ac8
);
border:none;
padding:14px 26px;
border-radius:40px;
color:white;
font-weight:700;
cursor:pointer;
transition:0.3s;
box-shadow:0 0 30px rgba(255,79,163,0.25);
}

.main-btn:hover{
transform:translateY(-2px);
}

/* =========================================================
HERO
========================================================= */

.hero{
min-height:100vh;
display:flex;
justify-content:space-between;
align-items:center;
padding:150px 8% 90px;
gap:70px;
position:relative;
}

/* FLOATING ORBS */

.orb{
position:absolute;
border-radius:50%;
filter:blur(70px);
opacity:0.3;
animation:float 8s infinite ease-in-out;
}

.orb1{
width:300px;
height:300px;
background:#ff2f92;
top:10%;
left:-100px;
}

.orb2{
width:280px;
height:280px;
background:#7b2fff;
bottom:10%;
right:-80px;
animation-delay:2s;
}

@keyframes float{

0%{
transform:translateY(0px);
}

50%{
transform:translateY(-30px);
}

100%{
transform:translateY(0px);
}

}

.left{
max-width:640px;
position:relative;
z-index:2;
}

.badges{
display:flex;
gap:12px;
flex-wrap:wrap;
margin-bottom:25px;
}

.badge{
background:rgba(255,255,255,0.07);
border:1px solid rgba(255,255,255,0.08);
padding:10px 16px;
border-radius:30px;
font-size:14px;
color:#ddd;
backdrop-filter:blur(10px);
}

.left h1{
font-size:88px;
line-height:0.92;
margin-bottom:25px;
font-weight:800;
}

.left h1 span{
background:linear-gradient(
90deg,
#ff4fa3,
#ff89d2
);
-webkit-background-clip:text;
-webkit-text-fill-color:transparent;
}

.left p{
font-size:18px;
line-height:1.8;
color:#b4b4b4;
margin-bottom:35px;
max-width:560px;
}

.stats{
display:flex;
gap:40px;
margin-top:35px;
flex-wrap:wrap;
}

.stat h2{
font-size:34px;
color:#ff73c7;
margin-bottom:5px;
}

.stat p{
font-size:14px;
color:#888;
}

/* =========================================================
ANALYZER PANEL
========================================================= */

.panel{
width:530px;
background:rgba(17,17,24,0.9);
border:1px solid rgba(255,255,255,0.08);
border-radius:35px;
padding:30px;
position:relative;
backdrop-filter:blur(20px);
box-shadow:
0 0 60px rgba(255,79,163,0.12);
z-index:2;
}

.panel h2{
margin-bottom:20px;
font-size:28px;
}

textarea{
width:100%;
height:240px;
background:#1b1b24;
border:none;
border-radius:24px;
padding:22px;
color:white;
resize:none;
font-size:15px;
margin-bottom:18px;
outline:none;
}

textarea::placeholder{
color:#7d7d86;
}

.upload{
background:#1b1b24;
padding:18px;
border-radius:24px;
margin-bottom:18px;
}

.upload p{
margin-bottom:12px;
color:#b8b8b8;
}

input{
width:100%;
padding:14px;
border:none;
border-radius:16px;
background:#242430;
color:white;
}

.preview{
width:100%;
border-radius:20px;
margin-top:15px;
display:none;
max-height:320px;
object-fit:cover;
}

.secondary-btn{
width:100%;
margin-top:12px;
background:transparent;
border:1px solid rgba(255,255,255,0.1);
padding:14px;
border-radius:18px;
color:#ccc;
cursor:pointer;
transition:0.3s;
}

.secondary-btn:hover{
background:rgba(255,255,255,0.05);
}

.loading{
display:none;
margin-top:16px;
color:#ff73c7;
font-weight:700;
}

.result{
margin-top:20px;
display:none;
background:rgba(255,255,255,0.04);
border:1px solid rgba(255,255,255,0.08);
padding:24px;
border-radius:24px;
animation:fade 0.4s ease;
}

@keyframes fade{

from{
opacity:0;
transform:translateY(10px);
}

to{
opacity:1;
transform:translateY(0);
}

}

/* =========================================================
SECTIONS
========================================================= */

.section{
padding:100px 8%;
}

.section h2{
font-size:52px;
margin-bottom:35px;
}

.cards{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
gap:20px;
}

.card{
background:rgba(255,255,255,0.04);
border:1px solid rgba(255,255,255,0.08);
padding:28px;
border-radius:28px;
backdrop-filter:blur(12px);
}

.card h3{
margin-bottom:15px;
color:#ff73c7;
}

/* =========================================================
AUTH
========================================================= */

.auth{
position:fixed;
inset:0;
background:rgba(0,0,0,0.82);
display:none;
justify-content:center;
align-items:center;
z-index:9999;
backdrop-filter:blur(10px);
}

.auth-box{
width:420px;
background:#111118;
padding:32px;
border-radius:30px;
border:1px solid rgba(255,255,255,0.08);
}

.auth-box h2{
margin-bottom:20px;
}

.auth-box input{
margin-bottom:15px;
}

.switch{
margin-top:15px;
text-align:center;
color:#8e8e99;
font-size:14px;
}

.switch span{
color:#ff73c7;
cursor:pointer;
}

/* =========================================================
FOOTER
========================================================= */

footer{
padding:60px;
text-align:center;
color:#7a7a84;
}

/* =========================================================
MOBILE
========================================================= */

@media(max-width:980px){

.hero{
flex-direction:column;
padding-top:140px;
}

.left h1{
font-size:62px;
}

.panel{
width:100%;
}

nav{
display:none;
}

}

</style>

</head>

<body>

<!-- =========================================================
HEADER
========================================================= -->

<header>

<div class="logo">
<span>⚖️</span>
DM Tribunal AI
</div>

<nav>

<button onclick="scrollToSection('home')">
Accueil
</button>

<button onclick="scrollToSection('examples')">
Exemples
</button>

<button onclick="scrollToSection('about')">
Comment ça marche
</button>

<button class="main-btn" onclick="openAuth()">
Connexion
</button>

</nav>

</header>

<!-- =========================================================
HERO
========================================================= -->

<section class="hero" id="home">

<div class="orb orb1"></div>
<div class="orb orb2"></div>

<div class="left">

<div class="badges">

<div class="badge">
🧠 Emotional AI
</div>

<div class="badge">
🚩 Red Flag Scanner
</div>

<div class="badge">
💘 Flirt Detection
</div>

<div class="badge">
📸 Screenshot Analysis
</div>

</div>

<h1>
Découvre ce qu’ils
<span>ressentent vraiment.</span>
</h1>

<p>
DM Tribunal AI analyse les conversations,
les intentions émotionnelles,
les red flags,
les green flags,
la chaleur émotionnelle,
la froideur,
le flirt,
le désintérêt
et les dynamiques relationnelles
grâce à une intelligence artificielle émotionnelle.
</p>

<button
class="main-btn"
onclick="scrollToAnalyzer()"
>
Analyser maintenant
</button>

<div class="stats">

<div class="stat">
<h2>2.3M+</h2>
<p>analyses émotionnelles</p>
</div>

<div class="stat">
<h2>94%</h2>
<p>précision émotionnelle</p>
</div>

<div class="stat">
<h2>42</h2>
<p>pays utilisateurs</p>
</div>

</div>

</div>

<!-- =========================================================
ANALYZER
========================================================= -->

<div class="panel" id="analyzer">

<h2>
Nouvelle analyse
</h2>

<textarea
id="conversation"
placeholder="Colle ici une conversation..."
></textarea>

<div class="upload">

<p>
Ajouter une capture d’écran
</p>

<input
type="file"
accept="image/*"
onchange="previewImage(event)"
>

<img
id="preview"
class="preview"
>

</div>

<button
class="main-btn"
style="width:100%;"
onclick="analyzeConversation()"
>
Analyser la conversation
</button>

<button
class="secondary-btn"
onclick="resetConversation()"
>
Réinitialiser
</button>

<div class="loading" id="loading">
Analyse émotionnelle IA en cours...
</div>

<div class="result" id="result">

<h2 id="verdict"></h2>

<p id="analysis"></p>

</div>

</div>

</section>

<!-- =========================================================
EXAMPLES
========================================================= -->

<section class="section" id="examples">

<h2>
Exemples d’analyses
</h2>

<div class="cards">

<div class="card">

<h3>
🟢 ACQUITTÉ
</h3>

<p>
“Bonjour princesse ❤️”
<br><br>
Le tribunal détecte une énergie tendre,
affectueuse et émotionnellement chaleureuse.
</p>

</div>

<div class="card">

<h3>
🟠 COUPABLE
</h3>

<p>
“oe jsp”
<br><br>
Énergie émotionnelle floue,
intention difficile à lire.
</p>

</div>

<div class="card">

<h3>
🔴 CONDAMNÉ
</h3>

<p>
“vu.”
<br><br>
Très forte froideur émotionnelle détectée.
</p>

</div>

</div>

</section>

<!-- =========================================================
ABOUT
========================================================= -->

<section class="section" id="about">

<h2>
Comment fonctionne l’IA ?
</h2>

<div class="cards">

<div class="card">

<h3>
🧠 Analyse émotionnelle
</h3>

<p>
L’IA analyse la chaleur émotionnelle,
la douceur,
le flirt,
la froideur
et les intentions derrière les messages.
</p>

</div>

<div class="card">

<h3>
💘 Détection relationnelle
</h3>

<p>
Le système détecte automatiquement
les green flags,
red flags,
le ghosting,
le love bombing
et les dynamiques toxiques.
</p>

</div>

<div class="card">

<h3>
📸 Analyse de screenshots
</h3>

<p>
Ajoute des captures d’écran
pour obtenir une analyse émotionnelle complète.
</p>

</div>

</div>

</section>

<footer>
© 2026 — DM Tribunal AI
</footer>

<!-- =========================================================
AUTH
========================================================= -->

<div class="auth" id="auth">

<div class="auth-box">

<h2 id="authTitle">
Connexion
</h2>

<input
type="text"
id="username"
placeholder="Nom d'utilisateur"
>

<input
type="email"
id="email"
placeholder="Adresse mail"
style="display:none;"
>

<input
type="password"
id="password"
placeholder="Mot de passe"
>

<button
class="main-btn"
style="width:100%;"
onclick="submitAuth()"
id="authButton"
>
Se connecter
</button>

<div class="switch">

<span onclick="toggleAuthMode()">
Pas encore de compte ? Créer un compte
</span>

</div>

</div>

</div>

<script>

/* =========================================================
CONFIG
========================================================= */

let loginMode = true;

/* =========================================================
AUTH
========================================================= */

function openAuth(){

document.getElementById("auth").style.display =
"flex";

}

function closeAuth(){

document.getElementById("auth").style.display =
"none";

}

function toggleAuthMode(){

loginMode = !loginMode;

const title =
document.getElementById("authTitle");

const button =
document.getElementById("authButton");

const switchText =
document.querySelector(".switch span");

const emailField =
document.getElementById("email");

if(loginMode){

title.innerHTML = "Connexion";

button.innerHTML = "Se connecter";

switchText.innerHTML =
"Pas encore de compte ? Créer un compte";

emailField.style.display = "none";

}

else{

title.innerHTML = "Créer un compte";

button.innerHTML = "Créer le compte";

switchText.innerHTML =
"Déjà un compte ? Se connecter";

emailField.style.display = "block";

}

}

function submitAuth(){

const username =
document.getElementById("username").value;

const password =
document.getElementById("password").value;

if(username === "" || password === ""){

alert("Remplis tous les champs");

return;

}

alert("Connexion réussie ✅");

closeAuth();

}

/* =========================================================
PREVIEW IMAGE
========================================================= */

function previewImage(event){

const file = event.target.files[0];

if(!file) return;

const preview =
document.getElementById("preview");

preview.src =
URL.createObjectURL(file);

preview.style.display = "block";

}

/* =========================================================
RESET
========================================================= */

function resetConversation(){

document
.getElementById("conversation")
.value = "";

document
.getElementById("preview")
.style.display = "none";

document
.getElementById("result")
.style.display = "none";

}

/* =========================================================
IA ÉMOTIONNELLE
========================================================= */

async function analyzeConversation(){

const text =
document
.getElementById("conversation")
.value
.trim();

if(text === ""){

alert("Ajoute une conversation");

return;

}

const loading =
document.getElementById("loading");

const result =
document.getElementById("result");

const verdict =
document.getElementById("verdict");

const analysis =
document.getElementById("analysis");

loading.style.display = "block";
result.style.display = "none";

/* SIMULATION IA */

await new Promise(resolve =>
setTimeout(resolve,1600)
);

const lower = text.toLowerCase();

/* =========================================================
ANALYSE INTELLIGENTE
========================================================= */

let warmth = 0;
let affection = 0;
let coldness = 0;
let tension = 0;
let effort = 0;

/* =========================================================
LONGUEUR
========================================================= */

if(text.length > 40){

effort += 2;

}

if(text.length > 120){

effort += 3;

}

/* =========================================================
PONCTUATION
========================================================= */

const exclamations =
(text.match(/!/g) || []).length;

warmth += exclamations;

const questions =
(text.match(/\?/g) || []).length;

effort += questions;

/* =========================================================
EMOJIS
========================================================= */

const positiveEmojis =
(text.match(
/❤️|💕|💖|🥰|😍|😘|🫶|☺️|😊|😭|😩|😻/g
) || []).length;

affection += positiveEmojis * 2;

/* =========================================================
FORMULATIONS AFFECTUEUSES
========================================================= */

const affectionatePatterns = [

"princesse",
"mon coeur",
"mon cœur",
"bb",
"bébé",
"mon ange",
"bonne nuit",
"prends soin",
"tu me manques",
"jtm",
"je t'aime",
"love",
"cutie",
"babe"

];

affectionatePatterns.forEach(word=>{

if(lower.includes(word)){

affection += 8;
warmth += 5;

}

});

/* =========================================================
RIRE / EXPRESSIVITÉ
========================================================= */

if(
lower.includes("ahah") ||
lower.includes("mdrrrr") ||
lower.includes("ptddddr")
){

warmth += 4;

}

/* =========================================================
FROIDEUR
========================================================= */

const dryPatterns = [

"vu",
"ok.",
"cool.",
"oe",
"jsp",
"d'accord"

];

dryPatterns.forEach(word=>{

if(lower === word){

coldness += 7;

}

});

/* =========================================================
AGRESSIVITÉ
========================================================= */

const aggressivePatterns = [

"tg",
"ta gueule",
"ferme la",
"casse toi",
"arrête"

];

aggressivePatterns.forEach(word=>{

if(lower.includes(word)){

tension += 8;

}

});

/* =========================================================
ANALYSE CONTEXTUELLE
========================================================= */

if(
lower.includes("bonjour") &&
affection > 0
){

warmth += 6;

}

/* IMPORTANT :
Les petits messages affectueux
ne sont PLUS pénalisés.
*/

/* =========================================================
SCORE FINAL
========================================================= */

const finalScore =

(
warmth +
affection +
effort
)

-

(
coldness +
tension
);

/* =========================================================
VERDICTS
========================================================= */

loading.style.display = "none";
result.style.display = "block";

/* ACQUITTÉ */

if(finalScore >= 10){

verdict.innerHTML =
"🟢 TOTALEMENT ACQUITTÉ";

const positiveTexts = [

"Très forte chaleur émotionnelle détectée. Le message paraît sincère, tendre et affectueux.",

"L’IA détecte une énergie émotionnellement chaleureuse et investie.",

"Flirt, douceur et attention émotionnelle détectés.",

"La vibe générale paraît très positive et émotionnellement safe."

];

analysis.innerHTML =

positiveTexts[
Math.floor(
Math.random() *
positiveTexts.length
)
];

/* CONDAMNÉ */

}

else if(finalScore <= 0){

verdict.innerHTML =
"🔴 CONDAMNÉ";

const negativeTexts = [

"Très forte froideur émotionnelle détectée.",

"L’IA détecte une énergie émotionnelle distante ou sèche.",

"Le message paraît émotionnellement fermé ou tendu.",

"Red flags ou désintérêt émotionnel potentiels détectés."

];

analysis.innerHTML =

negativeTexts[
Math.floor(
Math.random() *
negativeTexts.length
)
];

/* COUPABLE */

}

else{

verdict.innerHTML =
"🟠 COUPABLE";

const neutralTexts = [

"L’énergie émotionnelle paraît mitigée ou difficile à lire.",

"Le message contient quelques efforts émotionnels mais reste ambigu.",

"La vibe générale paraît hésitante.",

"Intention émotionnelle difficile à déterminer."

];

analysis.innerHTML =

neutralTexts[
Math.floor(
Math.random() *
neutralTexts.length
)
];

}

/* =========================================================
DETAILS
========================================================= */

analysis.innerHTML +=

`

<br><br>

💕 Affection :
${Math.max(0,affection)}

<br>

🔥 Chaleur émotionnelle :
${Math.max(0,warmth)}

<br>

✨ Investissement :
${Math.max(0,effort)}

<br>

❄️ Froideur :
${Math.max(0,coldness)}

<br>

🌧️ Tension :
${Math.max(0,tension)}

`;

}

/* =========================================================
SCROLL
========================================================= */

function scrollToAnalyzer(){

document
.getElementById("analyzer")
.scrollIntoView({
behavior:"smooth"
});

}

function scrollToSection(id){

document
.getElementById(id)
.scrollIntoView({
behavior:"smooth"
});

}

/* =========================================================
CLICK OUTSIDE AUTH
========================================================= */

window.onclick = function(event){

const auth =
document.getElementById("auth");

if(event.target === auth){

closeAuth();

}

};

</script>

</body>
</html>