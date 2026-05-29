<!DOCTYPE html>
<html lang="fr">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>DM Tribunal AI</title>

<!-- OCR IA IMAGE -->
<script src="https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js"></script>

<style>

/* =========================================================
RESET
========================================================= */

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
background:rgba(6,6,10,0.7);
backdrop-filter:blur(20px);
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
color:#d8d8d8;
}

nav{
display:flex;
gap:20px;
align-items:center;
}

nav button{
background:none;
border:none;
color:#d0d0d0;
cursor:pointer;
font-size:15px;
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

.orb{
position:absolute;
border-radius:50%;
filter:blur(80px);
opacity:0.3;
animation:float 8s infinite ease-in-out;
}

.orb1{
width:320px;
height:320px;
background:#ff2f92;
top:10%;
left:-100px;
}

.orb2{
width:300px;
height:300px;
background:#7b2fff;
bottom:5%;
right:-100px;
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
max-width:650px;
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
transform:translateY(0px);
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

<div class="badge">🧠 Emotional AI</div>
<div class="badge">🚩 Red Flag Scanner</div>
<div class="badge">💘 Flirt Detection</div>
<div class="badge">📸 Screenshot Analysis</div>

</div>

<h1>
Découvre ce qu’ils
<span>ressentent vraiment.</span>
</h1>

<p>
DM Tribunal AI analyse automatiquement
les conversations,
les screenshots,
les intentions émotionnelles,
la chaleur,
la froideur,
les red flags,
les green flags
et les dynamiques relationnelles.
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
id="imageInput"
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
🟢 TOTALEMENT ACQUITTÉ
</h3>

<p>
“Bonjour princesse ❤️”
<br><br>
Très forte chaleur émotionnelle détectée.
</p>

</div>

<div class="card">

<h3>
🟠 COUPABLE
</h3>

<p>
“oe jsp”
<br><br>
Énergie émotionnelle mitigée.
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
la froideur,
les intentions
et les dynamiques relationnelles.
</p>

</div>

<div class="card">

<h3>
💘 Détection relationnelle
</h3>

<p>
Détection automatique
des red flags,
green flags,
du flirt
et du désintérêt émotionnel.
</p>

</div>

<div class="card">

<h3>
📸 Analyse de screenshots
</h3>

<p>
Le site peut lire automatiquement
le texte présent dans les captures d’écran.
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
placeholder="Nom d'utilisateur"
>

<input
type="email"
placeholder="Adresse mail"
style="display:none;"
id="emailField"
>

<input
type="password"
placeholder="Mot de passe"
>

<button
class="main-btn"
style="width:100%;"
onclick="closeAuth()"
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
AUTH
========================================================= */

let loginMode = true;

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

const email =
document.getElementById("emailField");

const switchText =
document.querySelector(".switch span");

if(loginMode){

title.innerHTML = "Connexion";

email.style.display = "none";

switchText.innerHTML =
"Pas encore de compte ? Créer un compte";

}

else{

title.innerHTML = "Créer un compte";

email.style.display = "block";

switchText.innerHTML =
"Déjà un compte ? Se connecter";

}

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

document
.getElementById("imageInput")
.value = "";

}

/* =========================================================
IA ANALYSE
========================================================= */

async function analyzeConversation(){

const textarea =
document
.getElementById("conversation");

let text =
textarea.value.trim();

const fileInput =
document.getElementById("imageInput");

const file =
fileInput.files[0];

const loading =
document.getElementById("loading");

const result =
document.getElementById("result");

const verdict =
document.getElementById("verdict");

const analysis =
document.getElementById("analysis");

/* =========================================================
VÉRIFICATION
========================================================= */

if(text === "" && !file){

alert(
"Ajoute une conversation ou une image"
);

return;

}

loading.style.display = "block";
result.style.display = "none";

/* =========================================================
OCR IMAGE
========================================================= */

if(file){

try{

const {
data:{ text:imageText }
}

=

await Tesseract.recognize(
file,
'fra+eng'
);

text += " " + imageText;

}

catch(error){

console.log(error);

}

}

/* =========================================================
SIMULATION IA
========================================================= */

await new Promise(resolve =>
setTimeout(resolve,1200)
);

const lower =
text.toLowerCase();

/* =========================================================
ANALYSE ÉMOTIONNELLE
========================================================= */

let warmth = 0;
let affection = 0;
let coldness = 0;
let tension = 0;
let effort = 0;

/* LONGUEUR */

if(text.length > 40){

effort += 2;

}

if(text.length > 120){

effort += 3;

}

/* QUESTIONS */

const questions =
(text.match(/\?/g) || []).length;

effort += questions;

/* EXCLAMATIONS */

const exclamations =
(text.match(/!/g) || []).length;

warmth += exclamations;

/* EMOJIS */

const positiveEmojis =
(text.match(
/❤️|💕|💖|🥰|😍|😘|🫶|☺️|😊|😭|😩|😻/g
) || []).length;

affection += positiveEmojis * 2;

/* AFFECTION */

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

/* RIRE */

if(
lower.includes("ahah") ||
lower.includes("mdrrrr") ||
lower.includes("ptddddr")
){

warmth += 4;

}

/* FROIDEUR */

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

/* AGRESSIVITÉ */

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

/* BONUS AFFECTUEUX */

if(
lower.includes("bonjour") &&
affection > 0
){

warmth += 10;
affection += 5;

}

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
RESULT
========================================================= */

loading.style.display = "none";
result.style.display = "block";

/* POSITIF */

if(finalScore >= 10){

verdict.innerHTML =
"🟢 TOTALEMENT ACQUITTÉ";

const positiveTexts = [

"Très forte chaleur émotionnelle détectée.",

"L’IA détecte une énergie affectueuse et sincère.",

"Le message paraît tendre et émotionnellement safe.",

"Flirt, douceur et attention émotionnelle détectés."

];

analysis.innerHTML =

positiveTexts[
Math.floor(
Math.random() *
positiveTexts.length
)
];

}

/* NÉGATIF */

else if(finalScore <= 0){

verdict.innerHTML =
"🔴 CONDAMNÉ";

const negativeTexts = [

"Très forte froideur émotionnelle détectée.",

"L’énergie paraît émotionnellement distante.",

"Le tribunal détecte une vibe sèche.",

"Red flags potentiels détectés."

];

analysis.innerHTML =

negativeTexts[
Math.floor(
Math.random() *
negativeTexts.length
)
];

}

/* MITIGÉ */

else{

verdict.innerHTML =
"🟠 COUPABLE";

const neutralTexts = [

"Énergie émotionnelle mitigée.",

"Vibe émotionnelle difficile à lire.",

"Quelques efforts détectés mais dynamique floue.",

"Le message paraît émotionnellement ambigu."

];

analysis.innerHTML =

neutralTexts[
Math.floor(
Math.random() *
neutralTexts.length
)
];

}

/* DETAILS */

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

/* RESET */

setTimeout(()=>{

textarea.value = "";

document
.getElementById("preview")
.style.display = "none";

fileInput.value = "";

},1000);

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