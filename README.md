# aadiii-tic-tac-toe
✨ Modern Tic Tac Toe with AI, animations and glassmorphism UI.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
content="width=device-width,initial-scale=1.0">

<title>Aadiii Tic Tac Toe</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
-webkit-user-select:none;
user-select:none;
-webkit-tap-highlight-color:transparent;
}

:root{
--x:#8b93ff;
--o:#ff5ca8;
}

html,body{
height:100%;
width:100%;
}

body{
font-family:Inter,Segoe UI,sans-serif;
display:flex;
justify-content:center;
align-items:center;
padding:18px;
overflow:hidden;
background:
radial-gradient(circle at top left,#90a5ff55,transparent 40%),
radial-gradient(circle at bottom right,#ff82c955,transparent 40%),
linear-gradient(135deg,#111827,#312e81,#4c1d95);
background-size:200% 200%;
animation:bgMove 12s infinite alternate ease;
}

@keyframes bgMove{
from{
background-position:left top;
}
to{
background-position:right bottom;
}
}

body:before{
content:"";
position:fixed;
inset:0;
backdrop-filter:blur(28px);
pointer-events:none;
}

.container{
width:100%;
max-width:520px;
text-align:center;
z-index:2;
animation:fadeUp .8s ease;
}

@keyframes fadeUp{
from{
opacity:0;
transform:translateY(40px);
}
to{
opacity:1;
transform:none;
}
}

.status{
font-size:1.3rem;
font-weight:800;
color:white;
margin-bottom:25px;
text-shadow:0 4px 10px rgba(0,0,0,.3);
}

.controls{
display:flex;
justify-content:center;
gap:14px;
flex-wrap:wrap;
margin-bottom:28px;
}

/* -------- FIXED BUTTONS -------- */

button{
border:none;
outline:none;
cursor:pointer;
-webkit-tap-highlight-color:transparent;
appearance:none;
-webkit-appearance:none;
}

button:focus,
button:active{
outline:none;
box-shadow:none;
}

.mode-btn,
.reset-btn{
padding:13px 22px;
border-radius:16px;
font-weight:800;
font-size:14px;
transition:.3s;
}

.mode-btn{
background:rgba(255,255,255,.08);
backdrop-filter:blur(15px);
border:1px solid rgba(255,255,255,.2);
color:white;
box-shadow:
0 10px 20px rgba(0,0,0,.18),
inset 0 1px 1px rgba(255,255,255,.15);
}

.mode-btn.active{
background:
linear-gradient(
135deg,
#8ea2ff,
#6674ff
);
transform:translateY(-2px);
box-shadow:
0 10px 28px rgba(100,100,255,.45);
}

.mode-btn:not(.active):hover{
transform:translateY(-3px);
}

.reset-btn{
background:
linear-gradient(
135deg,
#5d68ff,
#7c87ff
);
color:white;
box-shadow:
0 10px 24px rgba(93,104,255,.4);
}

.reset-btn:hover{
transform:translateY(-3px);
}

/* -------- BOARD -------- */

.game-board{
display:grid;
grid-template-columns:repeat(3,1fr);
gap:14px;
padding:24px;
max-width:390px;
margin:auto;
aspect-ratio:1;
border-radius:34px;
background:rgba(255,255,255,.08);
border:1px solid rgba(255,255,255,.15);
backdrop-filter:blur(20px);
box-shadow:
0 30px 70px rgba(0,0,0,.35),
inset 0 1px 2px rgba(255,255,255,.12);
}

.cell{
aspect-ratio:1;
border:none;
border-radius:22px;
background:
linear-gradient(
145deg,
rgba(255,255,255,.97),
rgba(240,244,255,.92)
);
display:flex;
justify-content:center;
align-items:center;
font-size:clamp(2.8rem,8vw,4rem);
font-weight:900;
transition:.25s;
box-shadow:
0 8px 20px rgba(0,0,0,.12),
inset 0 1px 2px white;
}

.cell:hover{
transform:translateY(-4px);
}

.cell:active{
transform:scale(.94);
}

.x{
color:var(--x);
text-shadow:0 0 14px rgba(139,147,255,.4);
}

.o{
color:var(--o);
text-shadow:0 0 14px rgba(255,92,168,.4);
}

@keyframes pop{
0%{
transform:scale(.2);
opacity:0;
}
100%{
transform:scale(1);
opacity:1;
}
}

.pop{
animation:pop .3s ease;
}

.winner{
background:
linear-gradient(
135deg,
#fff4b4,
#ffd86f
)!important;
box-shadow:
0 0 30px rgba(255,210,50,.6);
animation:pulse 1s infinite alternate;
}

@keyframes pulse{
to{
transform:scale(1.06);
}
}

/* -------- SCORE -------- */

.score{
margin-top:30px;
display:flex;
justify-content:center;
gap:22px;
color:white;
}

.score div{
padding:15px 18px;
border-radius:18px;
background:rgba(255,255,255,.08);
border:1px solid rgba(255,255,255,.12);
backdrop-filter:blur(14px);
min-width:90px;
}

.score span{
display:block;
font-size:30px;
font-weight:900;
margin-top:8px;
}

.credit{
margin-top:30px;
color:rgba(255,255,255,.85);
font-weight:700;
letter-spacing:1.3px;
}

/* confetti */

#confetti-container{
position:fixed;
inset:0;
pointer-events:none;
overflow:hidden;
z-index:999;
}

.confetti{
position:absolute;
top:-20px;
border-radius:4px;
animation:fall linear forwards;
}

@keyframes fall{
to{
transform:
translateY(110vh)
rotate(1000deg);
opacity:0;
}
}

@media(max-width:480px){

.game-board{
gap:10px;
padding:18px;
}

.cell{
border-radius:18px;
}

.mode-btn,
.reset-btn{
padding:11px 16px;
font-size:13px;
}

.score{
gap:14px;
}

.score div{
min-width:70px;
padding:12px;
}

.score span{
font-size:22px;
}

}
</style>
</head>

<body>

<div class="container">

<div class="status" id="status">
Player X's Turn
</div>

<div class="controls">
<button class="mode-btn active"
id="pvpBtn">
PvP
</button>

<button class="mode-btn"
id="aiBtn">
vs AI
</button>

<button class="reset-btn"
id="resetBtn">
New Game
</button>
</div>

<div class="game-board"
id="gameBoard">

<button class="cell"
data-index="0"></button>

<button class="cell"
data-index="1"></button>

<button class="cell"
data-index="2"></button>

<button class="cell"
data-index="3"></button>

<button class="cell"
data-index="4"></button>

<button class="cell"
data-index="5"></button>

<button class="cell"
data-index="6"></button>

<button class="cell"
data-index="7"></button>

<button class="cell"
data-index="8"></button>

</div>

<div class="score">
<div>
X
<span id="scoreX">0</span>
</div>

<div>
Draw
<span id="scoreDraw">0</span>
</div>

<div>
O
<span id="scoreO">0</span>
</div>
</div>

<div class="credit">
Designed by Aadiii ✨
</div>

</div>

<div id="confetti-container"></div>

<script>

let board=[
"","","",
"","","",
"","",""
];

let currentPlayer="X";
let gameActive=true;
let gameMode="pvp";

let scores={
X:0,
O:0,
draw:0
};

const wins=[
[0,1,2],
[3,4,5],
[6,7,8],
[0,3,6],
[1,4,7],
[2,5,8],
[0,4,8],
[2,4,6]
];

const cells=
document.querySelectorAll(".cell");

const statusDisplay=
document.getElementById(
"status"
);

document
.getElementById(
"gameBoard"
)
.addEventListener(
"click",
e=>{
let cell=
e.target.closest(".cell");

if(!cell) return;

playerMove(
parseInt(
cell.dataset.index
)
);
}
);

document
.getElementById("pvpBtn")
.onclick=()=>setGameMode("pvp");

document
.getElementById("aiBtn")
.onclick=()=>setGameMode("ai");

document
.getElementById("resetBtn")
.onclick=resetGame;


function playerMove(i){

if(
board[i]!=="" ||
!gameActive ||
(
gameMode==="ai" &&
currentPlayer==="O"
)
) return;

board[i]=currentPlayer;

updateDisplay();

if(checkWinner()){

endGame(
gameMode==="ai"
&& currentPlayer==="O"
?
"AI Wins 🤖"
:
`Player ${currentPlayer} Wins 🎉`
);

scores[currentPlayer]++;
updateScore();
return;

}

if(boardFull()){
drawGame();
return;
}

currentPlayer=
currentPlayer==="X"
?
"O"
:
"X";

if(
gameMode==="ai" &&
currentPlayer==="O"
){
statusDisplay.textContent=
"AI Thinking...";
setTimeout(aiMove,500);
}else{
updateStatus();
}

}

function aiMove(){

let move=
findWinning("O")||
findWinning("X")||
(board[4]===""?4:getRandom());

board[move]="O";

updateDisplay();

if(checkWinner()){
endGame("AI Wins 🤖");
scores.O++;
updateScore();
return;
}

if(boardFull()){
drawGame();
return;
}

currentPlayer="X";
updateStatus();

}

function findWinning(p){

for(let line of wins){

let[a,b,c]=line;

let vals=[
board[a],
board[b],
board[c]
];

if(
vals.filter(
v=>v===p
).length===2
&& vals.includes("")
){
return line.find(
i=>board[i]===""
);
}

}

return null;

}

function getRandom(){

let open=
board
.map(
(v,i)=>
v===""?i:null
)
.filter(
v=>v!==null
);

return open[
Math.floor(
Math.random()
*open.length
)
];

}

function checkWinner(){

for(let p of wins){

let[a,b,c]=p;

if(
board[a] &&
board[a]===board[b] &&
board[a]===board[c]
){
highlight(p);
return true;
}

}

return false;

}

function highlight(pattern){

pattern.forEach(i=>{
cells[i]
.classList
.add("winner");
});

}

function boardFull(){
return board.every(
c=>c!==""
);
}

function drawGame(){

gameActive=false;

statusDisplay.textContent=
"It's a Draw!";

scores.draw++;

updateScore();

}

function endGame(msg){
gameActive=false;
statusDisplay.textContent=msg;
confetti();
}

function updateDisplay(){

cells.forEach(
(cell,i)=>{

cell.textContent=
board[i];

cell.classList.remove(
"x","o","pop"
);

if(board[i]==="X"){
cell.classList.add(
"x","pop"
);
}

if(board[i]==="O"){
cell.classList.add(
"o","pop"
);
}

}
);

}

function updateStatus(){
statusDisplay.textContent=
`Player ${currentPlayer}'s Turn`;
}

function updateScore(){

document
.getElementById("scoreX")
.textContent=scores.X;

document
.getElementById("scoreO")
.textContent=scores.O;

document
.getElementById("scoreDraw")
.textContent=scores.draw;

}

function resetGame(){

board=[
"","","",
"","","",
"","",""
];

currentPlayer="X";
gameActive=true;

cells.forEach(
cell=>{
cell.textContent="";
cell.classList.remove(
"x",
"o",
"winner",
"pop"
);
}
);

document
.getElementById(
"confetti-container"
).innerHTML="";

updateStatus();

}

function setGameMode(mode){

gameMode=mode;

/* only clicked button stays active */

document
.querySelectorAll(".mode-btn")
.forEach(
btn=>
btn.classList.remove(
"active"
)
);

if(mode==="pvp"){
document
.getElementById("pvpBtn")
.classList.add(
"active"
);
}

if(mode==="ai"){
document
.getElementById("aiBtn")
.classList.add(
"active"
);
}

resetGame();

}

function confetti(){

let box=
document.getElementById(
"confetti-container"
);

for(let i=0;i<120;i++){

let c=
document.createElement(
"div"
);

c.className=
"confetti";

c.style.left=
Math.random()*100+"vw";

c.style.background=
[
"#ff4d6d",
"#ffd60a",
"#06d6a0",
"#4cc9f0",
"#7209b7"
][
Math.floor(
Math.random()*5
)
];

let s=
Math.random()*10+8;

c.style.width=s+"px";
c.style.height=s+"px";

c.style.animationDuration=
(Math.random()*3+2)
+"s";

box.appendChild(c);

setTimeout(()=>{
c.remove();
},5000);

}

}

updateDisplay();

</script>

</body>
</html>
