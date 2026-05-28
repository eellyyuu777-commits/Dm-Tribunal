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
background:#07070b;
color:white;
overflow-x:hidden;
}

/* BACKGROUND */

body::before{
content:"";
position:fixed;
inset:0;
background:
radial-gradient(circle at top left,#ff2f92 0%,transparent 30%),
radial-gradient(circle at bottom right,#7b2fff 0%,transparent 30%);
opacity:0.15;
z-index:-1;
}

/* HEADER */

header{
display:flex;
justify-content:space-between;
align-items:center;
padding:25px 8%;
border-bottom:1px solid rgba(255,255,255,0.08);
background:rgba(7,7,11,0.85);
backdrop-filter:blur(12px);
position:sticky;
top:0;
z-index:999;
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
color:#d9d9d9;
}

nav{
display:flex;
gap:20px;
align-items:center;
}

nav button{
background:none;
border:none;
color:#ccc;
cursor:pointer;
font-size:15px;
transition:0.3s;
}

nav button:hover{
color:#ff5eb5;
}

.main-btn{
background:linear-gradient(90deg,#ff4fa3,#ff73c7);
border:none;
padding:14px 26px;
border-radius:30px;
color:white;
cursor:pointer;
font-weight:700;
transition:0.3s;
}

.main-btn:hover{
transform:translateY(-2px);
}

/* HERO */

.hero{
padding:90px 8%;
display:flex;
justify-content:space-between;
gap:60px;
align-items:flex-start;
}

.left{
max-width:620px;
}

.left h1{
font-size:82px;
line-height:0.95;
margin-bottom:25px;
}

.left h1 span{
color:#ff5eb5;
}

.left p{
color:#aaa;
line-height:1.8;
margin-bottom:35px;
font-size:17px;
}

.counter{
margin-top:20px;
color:#ff73c7;
font-weight:700;
}

/* PANEL */

.panel{
width:520px;
background:#111118;
border:1px solid rgba(255,255,255,0.08);
border-radius:30px;
padding:28px;
box-shadow:0 0 40px rgba(255,79,163,0.1);
}

textarea{
width:100%;
height:240px;
background:#1a1a22;
border:none;
border-radius:20px;
padding:20px;
color:white;
resize:none;
font-size:15px;
margin-bottom:18px;
}

.upload{
background:#1a1a22;
padding:18px;
border-radius:20px;
margin-bottom:18px;
}

.upload p{
margin-bottom:10px;
color:#ccc;
}

input{
width:100%;
padding:15px;
background:#1a1a22;
border:none;
border-radius:15px;
color:white;
margin-bottom:15px;
}

.preview{
width:100%;
border-radius:18px;
margin-top:15px;
display:none;
max-height:300px;
object-fit:cover;
}

.result{
margin-top:20px;
background:rgba(255,255,255,0.04);
padding:24px;
border-radius:22px;
display:none;
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

.loading{
display:none;
margin-top:15px;
font-weight:700;
color:#ff73c7;
}

/* SECTIONS */

.examples,
.help{
padding:90px 8%;
}

.examples h2,
.help h2{
font-size:46px;
margin-bottom:30px;
}

.cards{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
gap:20px;
}

.card{
background:rgba(255,255,255,0.04);
border:1px solid rgba(255,255,255,0.08);
border-radius:22px;
padding:25px;
}

.card h3{
margin-bottom:15px;
color:#ff73c7;
}

.help p{
max-width:850px;
line-height:1.8;
color:#aaa;
}

/* AUTH */

.auth{
position:fixed;
inset:0;
background:rgba(0,0,0,0.85);
display:none;
justify-content:center;
align-items:center;
z-index:9999;
}

.auth-box{
width:420px;
background:#111118;
padding:30px;
border-radius:25px;
}

.switch{
margin-top:15px;
text-align:center;
font-size:14px;
color:#aaa;
}

.switch span{
color:#ff73c7;
cursor:pointer;
}

/* FOOTER */

footer{
padding:50px;
text-align:center;
color:#777;
}

/* MOBILE */

@media(max-width:950px){

.hero{
flex-direction:column;
}

.left h1{
font-size:56px;
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

<button onclick="scrollToSection('help')">
Aide
</button>

<button class="main-btn" onclick="openAuth()">
Connexion
</button>

</nav>

</header>

<section class="hero" id="home">

<div class="left">

<h1>
Analyse les
<span>DM</span>
comme une vraie IA
</h1>

<p>
DM Tribunal AI détecte automatiquement
les intentions émotionnelles,
les red flags,
les green flags,
le flirt,
la froideur,
la manipulation
et les dynamiques relationnelles.
</p>

<button
class="main-btn"
onclick="scrollToAnalyzer()"
>
Analyser maintenant
</button>

<div class="counter" id="freeCounter">
5 analyses gratuites restantes
</div>

</div>

<div class="panel" id="analyzer">

<h2 style="margin-bottom:20px;">
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

<img id="preview" class="preview">

</div>

<button
class="main-btn"
style="width:100%;"
onclick="analyzeConversation()"
>
Analyser
</button>

<div class="loading" id="loading">
Analyse IA émotionnelle en cours...
</div>

<div class="result" id="result">

<h2 id="verdict"></h2>

<p id="analysis"></p>

</div>

</div>

</section>

<section class="examples" id="examples">

<h2>
Exemples d’analyses
</h2>

<div class="cards">

<div class="card">

<h3>
🟢 ACQUITTÉ
</h3>

<p>
“Bonne nuit princesse ❤️”
<br><br>
Affection, douceur,
intérêt émotionnel
et flirt détectés.
</p>

</div>

<div class="card">

<h3>
🟠 COUPABLE
</h3>

<p>
“oe jsp”
<br><br>
Énergie émotionnelle mitigée,
vibe difficile à lire.
</p>

</div>

<div class="card">

<h3>
🔴 CONDAMNÉ
</h3>

<p>
“vu”
<br><br>
Très forte froideur émotionnelle détectée.
</p>

</div>

</div>

</section>

<section class="help" id="help">

<h2>
Comment fonctionne l’IA ?
</h2>

<p>
L’intelligence artificielle analyse :
<br><br>

• le ton émotionnel
<br>
• le niveau d’investissement
<br>
• la chaleur ou la froideur
<br>
• l’intention derrière les messages
<br>
• la tension émotionnelle
<br>
• le flirt
<br>
• la sécheresse
<br>
• l’énergie générale
<br><br>

Puis elle génère automatiquement
un verdict émotionnel.
</p>

</section>

<footer>
© 2026 — DM Tribunal AI
</footer>

<!-- AUTH -->

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
let freeAnalyses = 5;

const savedAnalyses =
localStorage.getItem("freeAnalyses");

if(savedAnalyses !== null){

freeAnalyses =
parseInt(savedAnalyses);

}

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

const email =
document.getElementById("email").value;

if(loginMode){

const users =
JSON.parse(localStorage.getItem("users")) || [];

const user =
users.find(
u =>
u.username === username &&
u.password === password
);

if(!user){

alert("Identifiants incorrects");

return;

}

localStorage.setItem(
"loggedIn",
"true"
);

localStorage.setItem(
"loggedUser",
username
);

alert("Connexion réussie ✅");

closeAuth();

}

else{

const users =
JSON.parse(localStorage.getItem("users")) || [];

users.push({
username,
password,
email
});

localStorage.setItem(
"users",
JSON.stringify(users)
);

localStorage.setItem(
"loggedIn",
"true"
);

localStorage.setItem(
"loggedUser",
username
);

alert("Compte créé ✅");

closeAuth();

}

updateFreeCounter();

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
COUNTER
========================================================= */

function updateFreeCounter(){

const isLoggedIn =
localStorage.getItem("loggedIn");

const counter =
document.getElementById("freeCounter");

if(isLoggedIn){

counter.innerHTML =
"Connecté en tant que : " +
localStorage.getItem("loggedUser");

}

else{

counter.innerHTML =
freeAnalyses +
" analyses gratuites restantes";

}

}

/* =========================================================
IA ÉMOTIONNELLE
========================================================= */

async function analyzeConversation(){

const isLoggedIn =
localStorage.getItem("loggedIn");

if(
freeAnalyses <= 0 &&
!isLoggedIn
){

alert(
"Tu as utilisé tes 5 analyses gratuites."
);

openAuth();

return;

}

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
setTimeout(resolve,1800)
);

/* =========================================================
ANALYSE AVANCÉE
========================================================= */

let affection = 0;
let tension = 0;
let investment = 0;
let coldness = 0;
let enthusiasm = 0;

const lower = text.toLowerCase();

/* LONGUEUR */

if(text.length > 40){

investment += 2;

}

if(text.length > 120){

investment += 3;

}

if(text.length > 250){

investment += 4;

}

/* QUESTIONS */

const questions =
(text.match(/\?/g) || []).length;

investment += questions;

/* EXCLAMATIONS */

const exclamations =
(text.match(/!/g) || []).length;

enthusiasm += exclamations;

/* EMOJIS */

const positiveEmojis =
(text.match(
/❤️|💕|💖|🥰|😍|😘|🫶|😊|☺️|😭|😩|😻/g
) || []).length;

affection += positiveEmojis * 2;

/* EXPRESSIVITÉ */

if(
lower.includes("ahah") ||
lower.includes("mdrrrr") ||
lower.includes("ptddddr")
){

enthusiasm += 3;
affection += 1;

}

/* DOUCEUR */

if(
lower.includes("bonne nuit") ||
lower.includes("prends soin") ||
lower.includes("princesse") ||
lower.includes("mon coeur") ||
lower.includes("jtm") ||
lower.includes("je t'aime") ||
lower.includes("tu me manques")
){

affection += 5;

}

/* FROIDEUR */

if(text.length <= 8){

coldness += 4;

}

if(
lower.includes("vu") ||
lower.includes("ok.") ||
lower.includes("cool.") ||
lower.includes("jsp")
){

coldness += 3;

}

/* AGRESSIVITÉ */

if(
lower.includes("tg") ||
lower.includes("ta gueule") ||
lower.includes("ferme la") ||
lower.includes("casse toi")
){

tension += 6;

}

/* MULTI QUESTION */

if(
text.includes("???")
){

tension += 2;

}

/* SCORE */

const finalScore =

(
affection +
investment +
enthusiasm
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

if(finalScore >= 7){

verdict.innerHTML =
"🟢 ACQUITTÉ";

const positiveTexts = [

"Très forte chaleur émotionnelle détectée. La conversation paraît sincère, investie et affectueuse.",

"Le tribunal détecte beaucoup de green flags et une vraie connexion émotionnelle.",

"L’énergie générale paraît douce, naturelle et émotionnellement réciproque.",

"Flirt, attention et investissement émotionnel détectés."

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

"Le tribunal détecte une énergie distante ou déséquilibrée.",

"La conversation paraît émotionnellement sèche ou tendue.",

"Ghosting, désintérêt ou red flags potentiels détectés."

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

"La conversation paraît émotionnellement mitigée.",

"Le mood général semble hésitant ou difficile à lire.",

"Quelques efforts sont visibles mais la dynamique reste floue.",

"Le tribunal détecte une énergie émotionnelle instable."

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

✨ Investissement :
${Math.max(0,investment)}

<br>

⚡ Énergie :
${Math.max(0,enthusiasm)}

<br>

❄️ Froideur :
${Math.max(0,coldness)}

<br>

🌧️ Tension :
${Math.max(0,tension)}

`;

/* RESET */

setTimeout(()=>{

document
.getElementById("conversation")
.value = "";

document
.getElementById("preview")
.style.display = "none";

},1000);

/* FREE ANALYSES */

if(!isLoggedIn){

freeAnalyses--;

localStorage.setItem(
"freeAnalyses",
freeAnalyses
);

}

updateFreeCounter();

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
CLICK OUTSIDE
========================================================= */

window.onclick = function(event){

const auth =
document.getElementById("auth");

if(event.target === auth){

closeAuth();

}

};

/* =========================================================
LOAD
========================================================= */

window.onload = () => {

updateFreeCounter();

};

</script>

</body>
</html>