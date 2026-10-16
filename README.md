<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Castles and Caravans</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Cinzel:wght@700;900&family=Nunito:wght@600;700;800;900&display=swap">
<style>
/* Layout: an adventurer's map. A hub map with nine challenge stations (Europe north, West Africa south),
   each station opens as a parchment card; a coin purse and badge row track progress. */
:root{
  --parch:#F6EAD0;     /* parchment */
  --parch2:#EAD7AE;
  --ink:#2A1B0F;       /* iron-gall ink */
  --ink2:#5A4026;
  --gold:#E2A72E;      /* Mali gold */
  --gold-dk:#A86F0A;
  --clay:#B5532F;      /* Djenne mud-brick */
  --river:#2F7FB8;
  --royal:#3B3F8F;     /* castle banner blue */
  --ok:#2E8B57; --no:#C0392B;
  --display:"Cinzel",Georgia,"Times New Roman",serif;
  --body:"Nunito","Trebuchet MS",Verdana,sans-serif;
  color-scheme:light;
}
*{box-sizing:border-box}
[hidden]{display:none!important}
body{margin:0;background:var(--parch2);color:var(--ink);font-family:var(--body);
  background-image:radial-gradient(rgba(90,64,38,.08) 1px,transparent 1.4px);background-size:9px 9px}
button{font-family:var(--body);font-weight:900;cursor:pointer}
button:focus-visible{outline:3px solid var(--royal);outline-offset:3px}
.wrap{max-width:1080px;margin:0 auto;padding-left:max(16px,env(safe-area-inset-left,0px));padding-right:max(16px,env(safe-area-inset-right,0px));padding-block:16px 32px;display:flex;flex-direction:column;gap:14px}
header{display:flex;align-items:center;gap:14px;flex-wrap:wrap}
h1{font-family:var(--display);font-weight:900;font-size:clamp(28px,5vw,46px);margin:0;line-height:1;letter-spacing:.5px;text-wrap:balance}
h1 small{display:block;font-family:var(--body);font-size:15px;letter-spacing:2px;text-transform:uppercase;color:var(--ink2);margin-top:6px}
.purse{margin-left:auto;display:flex;gap:10px;align-items:center;flex-wrap:wrap}
.chip{background:var(--parch);border:2px solid var(--ink);border-radius:999px;padding:6px 14px;font-weight:900;font-variant-numeric:tabular-nums;display:flex;gap:6px;align-items:center}
.coin{width:18px;height:18px;border-radius:50%;background:radial-gradient(circle at 35% 30%,#FFE9A8,var(--gold) 55%,var(--gold-dk));border:2px solid var(--gold-dk);display:inline-block}
.mapbox{background:var(--parch);border:3px solid var(--ink);border-radius:20px;padding:10px;box-shadow:0 8px 0 rgba(42,27,15,.25)}
.mapbox svg{display:block;width:100%;height:auto}
.station{cursor:pointer}
.station:focus{outline:none}
.station:focus-visible circle.ring{stroke:var(--royal);stroke-width:6}
.legend{display:flex;gap:10px;flex-wrap:wrap}
.legend button{display:flex;align-items:center;gap:8px;background:var(--parch);border:2px solid var(--ink);border-radius:12px;padding:8px 12px;font-size:15px;text-align:left;color:var(--ink)}
.legend button .n{width:26px;height:26px;border-radius:50%;display:grid;place-items:center;color:#fff;font-size:14px;flex:none}
.legend button.done{background:#E3F2E1}
/* overlay card */
.overlay{position:fixed;inset:0;background:rgba(42,27,15,.55);display:flex;align-items:center;justify-content:center;padding:16px max(16px,env(safe-area-inset-left,0px));z-index:10}
.card{background:var(--parch);border:4px solid var(--ink);border-radius:22px;max-width:760px;width:100%;max-height:100%;overflow:auto;padding:22px 24px;box-shadow:0 10px 0 rgba(0,0,0,.25)}
.card h2{font-family:var(--display);font-size:clamp(22px,3.6vw,32px);margin:0 0 4px;line-height:1.1;text-wrap:balance}
.std{display:inline-block;font-size:13px;font-weight:900;letter-spacing:1px;text-transform:uppercase;background:var(--ink);color:var(--parch);border-radius:8px;padding:3px 10px;margin-bottom:8px}
.lore{font-size:17px;line-height:1.55;background:#FFF8E8;border-left:6px solid var(--gold);border-radius:10px;padding:10px 14px;margin:8px 0 12px;max-width:68ch}
.q{font-size:19px;font-weight:800;margin:10px 0}
.opts{display:grid;gap:8px}
.opt{text-align:left;background:#fff;border:3px solid var(--ink);border-radius:14px;padding:10px 14px;font-size:17px;color:var(--ink)}
.opt:hover{background:#FFF3D6}
.opt.right{background:#DDF3E1;border-color:var(--ok)}
.opt.wrong{background:#F9DEDA;border-color:var(--no)}
.fb{border-radius:12px;padding:10px 14px;font-size:16px;line-height:1.5;margin-top:10px}
.fb.ok{background:#DDF3E1;border:2px solid var(--ok)}
.fb.bad{background:#F9DEDA;border:2px solid var(--no)}
.row{display:flex;gap:10px;flex-wrap:wrap;align-items:center;margin-top:14px}
.big{background:var(--gold);color:var(--ink);font-family:var(--display);font-weight:900;font-size:18px;border:3px solid var(--ink);border-radius:14px;padding:10px 20px;box-shadow:0 4px 0 var(--gold-dk)}
.big:active{transform:translateY(3px);box-shadow:0 1px 0 var(--gold-dk)}
.ghost{background:#fff;border:3px solid var(--ink);border-radius:14px;padding:9px 16px;font-size:16px;color:var(--ink)}
.pill{display:inline-flex;align-items:center;justify-content:center;background:#fff;border:3px solid var(--ink);border-radius:999px;padding:8px 14px;font-size:16px;font-weight:800;color:var(--ink)}
.pill.sel{background:var(--gold);box-shadow:0 0 0 4px rgba(226,167,46,.4)}
.pill.used{opacity:.35;pointer-events:none}
.bank{display:flex;gap:8px;flex-wrap:wrap;margin:10px 0}
.slots{display:grid;gap:8px}
.slot{display:flex;align-items:center;gap:10px;background:#fff;border:3px dashed var(--ink2);border-radius:14px;padding:8px 12px;min-height:52px;font-size:16px;cursor:pointer;text-align:left;color:var(--ink)}
.slot .lab{font-weight:900;min-width:0;flex:1}
.slot .put{font-weight:900;color:var(--royal)}
.slot.right{border-style:solid;border-color:var(--ok);background:#DDF3E1}
.slot.wrong{border-style:solid;border-color:var(--no);background:#F9DEDA}
.pyr .slot{margin-inline:auto}
.prog{font-size:14px;font-weight:800;color:var(--ink2)}
.stars{font-family:var(--display);color:var(--gold-dk);font-size:28px;letter-spacing:4px}
.codebox{font-family:var(--display);font-size:clamp(28px,6vw,44px);background:var(--ink);color:var(--gold);border-radius:14px;padding:10px 18px;display:inline-block;letter-spacing:3px}
.wa svg{width:100%;height:auto;display:block;border:3px solid var(--ink);border-radius:14px}
.spot{cursor:pointer}
@media (max-width:560px){.legend button{font-size:14px;padding:7px 10px}}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <h1>Castles &amp; Caravans<small>5th Grade Social Studies · Medieval Europe &amp; West Africa</small></h1>
    <div class="purse">
      <div class="chip"><span class="coin" aria-hidden="true"></span><span id="coins">0</span> gold</div>
      <div class="chip">Stations <span id="done">0</span>/9</div>
    </div>
  </header>

  <div class="mapbox">
    <svg viewBox="0 0 1000 560" role="img" aria-label="Quest map with nine stations: five in medieval Europe at the top and four in West Africa at the bottom">
      <defs>
        <pattern id="sand" width="18" height="18" patternUnits="userSpaceOnUse"><rect width="18" height="18" fill="#EBCB8B"/><circle cx="4" cy="5" r="1.4" fill="#D7AE63"/><circle cx="13" cy="12" r="1.2" fill="#D7AE63"/></pattern>
        <pattern id="grass" width="20" height="20" patternUnits="userSpaceOnUse"><rect width="20" height="20" fill="#9CC17A"/><path d="M5 14 l2 -5 l2 5 M13 8 l2 -5 l2 5" stroke="#7FA75E" stroke-width="1.5" fill="none"/></pattern>
      </defs>
      <rect width="1000" height="560" fill="#9CC9E6"/>
      <!-- Europe -->
      <path d="M140 40 C260 10 420 30 520 20 C640 10 760 40 860 30 C920 60 900 120 860 150 C800 190 700 180 640 200 C560 225 520 210 470 230 C420 250 360 230 320 240 C250 255 200 230 170 200 C120 160 100 90 140 40Z" fill="url(#grass)" stroke="#2A1B0F" stroke-width="3"/>
      <path d="M420 230 C440 260 470 270 480 250" stroke="#2A1B0F" stroke-width="3" fill="#9CC17A"/>
      <text x="470" y="75" text-anchor="middle" font-family="Cinzel, Georgia, serif" font-weight="900" font-size="26" fill="#2A1B0F">MEDIEVAL EUROPE</text>
      <!-- Mediterranean -->
      <text x="560" y="275" text-anchor="middle" font-family="Georgia, serif" font-style="italic" font-size="16" fill="#1F5F8B">Mediterranean Sea</text>
      <!-- Africa -->
      <path d="M90 300 C200 285 380 290 520 300 C680 300 820 290 930 310 L930 560 L90 560 Z" fill="url(#sand)" stroke="#2A1B0F" stroke-width="3"/>
      <path d="M90 450 C220 440 300 430 420 440 C560 450 700 430 930 445 L930 560 L90 560Z" fill="#B7CF84" opacity=".85"/>
      <text x="770" y="350" text-anchor="middle" font-family="Cinzel, Georgia, serif" font-weight="900" font-size="22" fill="#7A4E12">SAHARA DESERT</text>
      <path d="M260 520 C330 470 420 440 470 400 C520 430 560 470 600 540" stroke="#2F7FB8" stroke-width="7" fill="none" stroke-linecap="round"/>
      <text x="600" y="505" font-family="Georgia, serif" font-style="italic" font-size="15" fill="#1F5F8B">Niger River</text>
      <text x="520" y="548" text-anchor="middle" font-family="Cinzel, Georgia, serif" font-weight="900" font-size="20" fill="#2A1B0F">WEST AFRICA</text>
      <!-- caravan trail -->
      <path d="M470 395 C470 330 560 300 600 250" stroke="#7A4E12" stroke-width="3" stroke-dasharray="8 8" fill="none"/>
      <g id="pins"></g>
    </svg>
  </div>
  <div class="legend" id="legend"></div>
</div>

<div class="overlay" id="ov" hidden><div class="card" id="card" role="dialog" aria-modal="true" aria-labelledby="ctitle"></div></div>

<script>
(()=>{
const END_CODE="Timbuktu";
// ---------------------------------------------------------------- stations
const ST=[
{id:"feudal",n:1,region:"eu",x:200,y:115,color:"#3B3F8F",title:"The Feudal Ladder",std:"5.9.d · Feudalism",
 lore:"In medieval Europe, the king owned the land. He gave pieces of land, called fiefs, to nobles (lords) in exchange for loyalty and soldiers. Lords gave land to knights who fought for them. Peasants and serfs farmed the land and got protection in return.",
 type:"order",prompt:"Build the feudal ladder. Tap a group, then tap the rung where it belongs, from the TOP down.",
 slots:["Top: most power, owns all the land","Second: gets fiefs, promises loyalty and soldiers","Third: fights on horseback for a lord","Bottom: farms the land for protection"],
 items:["King","Nobles / Lords","Knights","Peasants / Serfs"],
 explain:"The king was at the top, then nobles, then knights, and peasants and serfs at the bottom. Each group owed something to the group above it."},
{id:"manor",n:2,region:"eu",x:350,y:170,color:"#3B3F8F",title:"Life on the Manor",std:"5.9.d · Manorialism",
 lore:"A manor was a lord’s estate: his house or castle, farmland, a village, a church, a mill, and woods. Serfs lived and worked there and could not leave without permission. Manors made almost everything they needed themselves.",
 type:"mcq",qs:[
 {q:"Why was a manor called “self-sufficient”?",o:["It produced almost everything the people needed","It bought everything from faraway cities","It was run by the king himself","Only knights lived there"],a:0,e:"Manors grew their own food and made their own tools, cloth, and flour, so they rarely needed to trade."},
 {q:"What did serfs receive in exchange for working the lord’s land?",o:["Protection and a small plot of land to farm","Gold coins every week","Their own castle","The right to move anywhere"],a:0,e:"Serfs got protection and land to grow food, but they owed labor to the lord and could not leave the manor."},
 {q:"How did feudalism and manors shape the medieval economy?",o:["Wealth was based on land and farming","Most people worked in factories","Everyone traded with paper money","People lived mostly in big cities"],a:0,e:"Land was the main source of wealth, and most people were farmers living on manors."}]},
{id:"crusades",n:3,region:"eu",x:540,y:160,color:"#3B3F8F",title:"The Crusades",std:"5.9.f · The Crusades",
 lore:"The Crusades (1096–1291) were a series of religious wars. European Christians fought to control Jerusalem and the Holy Land, a region also holy to Muslims and Jews. The wars caused great suffering, but they also brought Europeans into contact with new goods and ideas.",
 type:"mcq",qs:[
 {q:"What was the main goal of the Crusades for European Christians?",o:["To control Jerusalem and the Holy Land","To explore the Americas","To build castles in Africa","To end the Black Death"],a:0,e:"Christian armies wanted to control Jerusalem, a city holy to Christians, Muslims, and Jews."},
 {q:"How did the Crusades affect Jewish communities in Europe?",o:["Many Jewish communities were attacked and treated unfairly","Jewish people were given more land","They were not affected at all","They became the rulers of Europe"],a:0,e:"Some crusaders attacked Jewish communities in Europe, and prejudice against Jewish people grew."},
 {q:"Which was a lasting effect of the Crusades on Europe?",o:["More trade and contact with Muslim learning, goods, and ideas","Europe stopped all trade","Feudalism grew stronger forever","Everyone in Europe became a knight"],a:0,e:"Europeans brought back spices, silk, and knowledge from Muslim scholars, which helped trade grow."}]},
{id:"plague",n:4,region:"eu",x:790,y:90,color:"#3B3F8F",title:"The Black Death",std:"5.9.g · Bubonic Plague",
 lore:"In the 1300s, a terrible disease called the Black Death spread along busy trade routes. Fleas on rats carried it on ships and with caravans. It killed about one third of Europe’s people. Afterward, there were fewer workers, so the workers who were left could ask for higher pay.",
 type:"order",prompt:"Trace how the plague spread along trade routes. Tap a place, then tap the step where it belongs.",
 slots:["Step 1","Step 2","Step 3","Step 4"],items:["Central Asia","China","Middle East","Europe"],
 explain:"The plague began in Central Asia, spread to China, then along trade routes to the Middle East, and on to Europe by ship.",
 follow:[{q:"After the Black Death, why could peasants ask for higher wages?",o:["There were far fewer workers, so their labor was worth more","Kings gave everyone gold","Manors grew bigger","More people moved to farms"],a:0,e:"With so many people gone, lords needed workers badly. This helped weaken feudalism."}]},
{id:"hundred",n:5,region:"eu",x:700,y:165,color:"#3B3F8F",title:"The Hundred Years’ War",std:"5.9.h · Hundred Years’ War",
 lore:"The Hundred Years’ War (1337–1453) was a long series of wars between England and France. England’s King Henry V won a famous battle at Agincourt in 1415 and used English, not French, in his royal letters. Joan of Arc, a teenage French girl, led French troops to victory at Orléans in 1429 and inspired France to unite.",
 type:"match",prompt:"Match each clue to the right person. Tap a clue, then tap the person.",
 targets:["Henry V","Joan of Arc"],
 items:[["Won the Battle of Agincourt in 1415","Henry V"],["Led the French to victory at Orléans","Joan of Arc"],["Helped make English an important language in England","Henry V"],["Inspired the French people to unite","Joan of Arc"]],
 explain:"Henry V was an English king who won at Agincourt and promoted the English language. Joan of Arc was a French heroine who inspired France."},
{id:"map",n:6,region:"af",x:220,y:420,color:"#B5532F",title:"Map of West Africa",std:"5.11.a · Geography",
 lore:"West Africa has the huge Sahara Desert to the north, the Atlantic Ocean to the west, and the Gulf of Guinea to the south. The Niger River curves through the land. Cities like Timbuktu and Djenne grew up near the river.",
 type:"map",prompt:"Tap a label, then tap the numbered spot on the map where it belongs."},
{id:"caravan",n:7,region:"af",x:520,y:330,color:"#B5532F",title:"Salt for Gold",std:"5.11.c · Trans-Saharan Trade",
 lore:"Camel caravans crossed the Sahara to trade. The desert had salt, which people needed to keep food from spoiling and to stay healthy in the heat. The lands to the south had gold. Muslim traders on the caravans also brought Islam, books, and the Arabic language to West Africa. Sadly, enslaved people were also traded along these routes.",
 type:"mcq",qs:[
 {q:"A caravan is leaving the Sahara and heading SOUTH. What should the camels carry?",o:["Salt","Gold","Snow","Fish"],a:0,e:"Salt came from the desert in the north, so caravans carried it south to trade for gold."},
 {q:"Why were camels the best animals for crossing the Sahara?",o:["They can go many days without water and walk on sand","They can fly over dunes","They swim across rivers quickly","They pull large wagons on roads"],a:0,e:"Camels store fat for energy, need little water, and have wide feet for walking on sand."},
 {q:"How did the trans-Saharan trade change West African culture?",o:["It spread Islam, Arabic writing, and learning","It brought cars and trains","It stopped all religion","It made everyone move to Europe"],a:0,e:"Muslim traders brought Islam, Arabic, and books. Many West African rulers and scholars became Muslim."}]},
{id:"kingdoms",n:8,region:"af",x:700,y:420,color:"#B5532F",title:"Rise of the Kingdoms",std:"5.11.b · Ghana, Mali, Songhai",
 lore:"Three great empires grew rich by controlling the gold and salt trade. Ghana came first and was called the “Land of Gold.” Mali rose next and turned Timbuktu and Djenne into centers of trade and learning. Songhai came last and became the largest of the three.",
 type:"order",prompt:"Put the empires in order from EARLIEST to LATEST. Tap an empire, then tap its spot on the timeline.",
 slots:["First (about 300s–1100s)","Second (about 1230s–1400s)","Third (about 1460s–1591)"],items:["Ghana","Mali","Songhai"],
 explain:"Ghana came first, then Mali, then Songhai. Each grew strong by controlling the trade routes.",
 follow:[{q:"What made Timbuktu famous during the Mali and Songhai empires?",o:["It was a center of trade, books, and learning","It was the capital of France","It was a fishing village in the ocean","It had no people living there"],a:0,e:"Timbuktu had great mosques, universities, and thousands of handwritten books."}]},
{id:"musa",n:9,region:"af",x:420,y:480,color:"#B5532F",title:"Mansa Musa’s Journey",std:"5.11.d · Mansa Musa",
 lore:"Mansa Musa ruled the Mali Empire in the 1300s and may have been one of the richest people in history. In 1324 he made a pilgrimage, a holy journey, to Mecca. He traveled with thousands of people and camels carrying gold, and he gave so much away in Cairo that the price of gold there dropped for years.",
 type:"mcq",qs:[
 {q:"Why did Mansa Musa travel to Mecca?",o:["To make a pilgrimage, a religious journey for Muslims","To start a war with Egypt","To sell salt in Europe","To find a new place to live"],a:0,e:"Mansa Musa was Muslim, and making a pilgrimage (the Hajj) to Mecca is an important part of Islam."},
 {q:"What happened when Mansa Musa gave away so much gold in Cairo?",o:["Gold became less valuable there for years","Gold became more valuable","Nothing changed at all","Cairo ran out of salt"],a:0,e:"So much gold flooded in that it lost value. This shows how rich Mali was!"},
 {q:"Why was Mansa Musa’s pilgrimage important for Mali?",o:["It made Mali famous and brought scholars and architects back to Mali","It made Mali smaller","It ended trade in West Africa","It moved Mali’s capital to Europe"],a:0,e:"The world learned about Mali’s wealth, and Musa brought back scholars and builders who helped Timbuktu grow."}]}
];
const MAPSPOTS=[
 {k:"Atlantic Ocean",x:60,y:230},{k:"Gulf of Guinea",x:330,y:330},{k:"Sahara Desert",x:330,y:70},
 {k:"Niger River",x:400,y:220},{k:"Timbuktu",x:300,y:140},{k:"Djenne",x:250,y:200}];

// ---------------------------------------------------------------- state
let coins=0, done={}, best={};
try{const s=JSON.parse(localStorage.getItem('cc-save')||'{}');coins=s.coins||0;done=s.done||{};best=s.best||{}}catch(e){}
const save=()=>{try{localStorage.setItem('cc-save',JSON.stringify({coins,done,best}))}catch(e){}};
const $=id=>document.getElementById(id);
function refresh(){
  $('coins').textContent=coins;$('done').textContent=Object.keys(done).length;
  const pins=ST.map(s=>`<g class="station" tabindex="0" role="button" aria-label="Station ${s.n}: ${s.title}${done[s.id]?' (done)':''}" data-id="${s.id}" transform="translate(${s.x} ${s.y})">
    <circle class="ring" r="26" fill="${done[s.id]?'#2E8B57':s.color}" stroke="#2A1B0F" stroke-width="4"/>
    <text y="8" text-anchor="middle" font-family="Cinzel, Georgia, serif" font-weight="900" font-size="24" fill="#fff">${done[s.id]?'★':s.n}</text>
    <text y="46" text-anchor="middle" font-family="Nunito, Verdana, sans-serif" font-weight="900" font-size="15" fill="#2A1B0F" stroke="#F6EAD0" stroke-width="4" paint-order="stroke">${s.title}</text></g>`).join('');
  $('pins').innerHTML=pins;
  $('pins').querySelectorAll('.station').forEach(g=>{g.onclick=()=>open(g.dataset.id);g.onkeydown=e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();open(g.dataset.id)}}});
  $('legend').innerHTML=ST.map(s=>`<button type="button" data-id="${s.id}" class="${done[s.id]?'done':''}"><span class="n" style="background:${done[s.id]?'#2E8B57':s.color}">${done[s.id]?'★':s.n}</span>${s.title}</button>`).join('')+
   (Object.keys(done).length===9?`<button type="button" id="finish" style="background:var(--gold)"><span class="n" style="background:#2A1B0F">★</span>See your reward</button>`:'');
  $('legend').querySelectorAll('button[data-id]').forEach(b=>b.onclick=()=>open(b.dataset.id));
  if($('finish'))$('finish').onclick=finale;
}
function card(html){$('card').innerHTML=html;$('ov').hidden=false;const f=$('card').querySelector('button');if(f)f.focus()}
function close(){$('ov').hidden=true;refresh()}
$('ov').addEventListener('click',e=>{if(e.target.id==='ov')close()});
addEventListener('keydown',e=>{if(e.key==='Escape'&&!$('ov').hidden)close()});
const shuffle=a=>a.map(v=>[Math.random(),v]).sort((x,y)=>x[0]-y[0]).map(v=>v[1]);
const head=s=>`<span class="std">${s.std}</span><h2 id="ctitle">${s.n}. ${s.title}</h2><div class="lore">${s.lore}</div>`;

// ---------------------------------------------------------------- station runner
let run=null;
function open(id){const s=ST.find(x=>x.id===id);run={s,earned:0,max:0,tries:0};
  if(s.type==='mcq')mcq(s.qs,0,()=>finish());
  else if(s.type==='order')order(s);
  else if(s.type==='match')match(s);
  else if(s.type==='map')mapGame(s);}
function finish(){
  const s=run.s, pct=run.max?run.earned/run.max:1, stars=pct>=.99?3:pct>=.6?2:1;
  coins+=run.earned;done[s.id]=true;best[s.id]=Math.max(best[s.id]||0,stars);save();
  card(`${'<span class="std">'+s.std+'</span>'}<h2 id="ctitle">Station complete!</h2>
   <p class="stars" aria-label="${stars} of 3 stars">${'★'.repeat(stars)}${'☆'.repeat(3-stars)}</p>
   <p style="font-size:18px">You earned <b>${run.earned} gold</b> at <b>${s.title}</b>.</p>
   <div class="row"><button class="big" type="button" id="back">Back to the map</button>${stars<3?'<button class="ghost" type="button" id="again">Try for 3 stars</button>':''}</div>`);
  $('back').onclick=close; if($('again'))$('again').onclick=()=>open(s.id);
}
// multiple choice (with retry: 10 gold first try, 5 second)
function mcq(qs,i,then){
  if(i>=qs.length)return then();
  const s=run.s,Q=qs[i];const order=shuffle(Q.o.map((t,k)=>k));let tries=0;run.max+=10;
  card(`${head(s)}<p class="prog">Question ${i+1} of ${qs.length}</p><p class="q">${Q.q}</p><div class="opts">${order.map(k=>`<button class="opt" type="button" data-k="${k}">${Q.o[k]}</button>`).join('')}</div><div id="fb"></div>`);
  $('card').querySelectorAll('.opt').forEach(b=>b.onclick=()=>{
    const k=+b.dataset.k;tries++;
    if(k===Q.a){b.classList.add('right');const g=tries===1?10:tries===2?5:0;run.earned+=g;
      $('card').querySelectorAll('.opt').forEach(x=>x.disabled=true);
      $('fb').innerHTML=`<div class="fb ok"><b>Correct! +${g} gold.</b> ${Q.e}</div><div class="row"><button class="big" type="button" id="nx">${i+1<qs.length?'Next question':'Continue'}</button></div>`;
      $('nx').onclick=()=>mcq(qs,i+1,then);$('nx').focus();}
    else{b.classList.add('wrong');b.disabled=true;$('fb').innerHTML=`<div class="fb bad"><b>Not quite.</b> Reread the story box and try again.</div>`}
  });
}
// tap-to-place ordering
function order(s){
  const items=shuffle(s.items.slice());const placed=Array(s.slots.length).fill(null);let sel=null;run.max+=s.items.length*10;
  const pyr=s.id==='feudal';
  const render=()=>{
    card(`${head(s)}<p class="q">${s.prompt}</p>
    <div class="bank">${items.map(t=>`<button class="pill ${sel===t?'sel':''} ${placed.includes(t)?'used':''}" type="button" data-t="${t}">${t}</button>`).join('')}</div>
    <div class="slots ${pyr?'pyr':''}">${s.slots.map((l,i)=>`<button class="slot" type="button" data-i="${i}" style="${pyr?`width:${55+i*15}%`:''}"><span class="lab">${l}</span><span class="put">${placed[i]||'tap to place'}</span></button>`).join('')}</div>
    <div class="row"><button class="big" type="button" id="check" ${placed.includes(null)?'disabled style="opacity:.5"':''}>Check my answer</button><button class="ghost" type="button" id="clear">Clear</button></div><div id="fb"></div>`);
    $('card').querySelectorAll('.pill').forEach(b=>b.onclick=()=>{sel=b.dataset.t;render()});
    $('card').querySelectorAll('.slot').forEach(b=>b.onclick=()=>{const i=+b.dataset.i;if(sel){const old=placed.indexOf(sel);if(old>-1)placed[old]=null;placed[i]=sel;sel=null}else placed[i]=null;render()});
    $('clear').onclick=()=>{placed.fill(null);sel=null;render()};
    $('check').onclick=check;
  };
  let attempt=0;
  const check=()=>{attempt++;let ok=0;
    $('card').querySelectorAll('.slot').forEach((b,i)=>{const r=placed[i]===s.items[i];b.classList.add(r?'right':'wrong');if(r)ok++});
    if(ok===s.items.length){const g=attempt===1?s.items.length*10:attempt===2?s.items.length*5:s.items.length*2;run.earned+=g;
      $('fb').innerHTML=`<div class="fb ok"><b>All correct! +${g} gold.</b> ${s.explain}</div><div class="row"><button class="big" type="button" id="nx">Continue</button></div>`;
      $('check').disabled=true;$('nx').onclick=()=>s.follow?mcq(s.follow,0,finish):finish();$('nx').focus()}
    else{$('fb').innerHTML=`<div class="fb bad"><b>${ok} of ${s.items.length} are in the right place.</b> Green ones are correct. Move the red ones and check again.</div>`;
      setTimeout(()=>{s.items.forEach((t,i)=>{if(placed[i]!==t)placed[i]=null});render();$('fb').innerHTML=`<div class="fb bad"><b>${ok} of ${s.items.length} were right.</b> The correct ones stayed. Place the rest and check again.</div>`},1400)}
  };
  render();
}
// match clues to people
function match(s){
  const clues=shuffle(s.items.slice());let sel=null;const ans={};let wrongs=0;run.max+=s.items.length*10;
  const render=(msg)=>{
    card(`${head(s)}<p class="q">${s.prompt}</p>
    <div class="slots">${clues.map(([c],i)=>`<button class="slot ${ans[c]?(ans[c].ok?'right':'wrong'):''}" type="button" data-c="${i}" ${ans[c]&&ans[c].ok?'disabled':''} style="${sel===i?'box-shadow:0 0 0 4px rgba(226,167,46,.6)':''}"><span class="lab">${c}</span><span class="put">${ans[c]?ans[c].who:''}</span></button>`).join('')}</div>
    <div class="bank" style="margin-top:12px">${s.targets.map(t=>`<button class="pill" type="button" data-w="${t}" style="font-size:18px;padding:12px 20px">${t}</button>`).join('')}</div><div id="fb">${msg||''}</div>`);
    $('card').querySelectorAll('.slot').forEach(b=>b.onclick=()=>{sel=+b.dataset.c;render()});
    $('card').querySelectorAll('.pill').forEach(b=>b.onclick=()=>{if(sel===null){render('<div class="fb bad">Tap a clue first, then tap a person.</div>');return}
      const [c,w]=clues[sel];const ok=b.dataset.w===w;ans[c]={who:b.dataset.w,ok};if(!ok)wrongs++;sel=null;
      if(clues.every(([c])=>ans[c]&&ans[c].ok)){const g=Math.max(10,s.items.length*10-wrongs*5);run.earned+=g;render(`<div class="fb ok"><b>All matched! +${g} gold.</b> ${s.explain}</div><div class="row"><button class="big" type="button" id="nx">Continue</button></div>`);$('nx').onclick=finish;$('nx').focus()}
      else render(ok?'<div class="fb ok">Correct!</div>':'<div class="fb bad">Not quite. Reread the story box and tap that clue again.</div>')});
  };render();
}
// map labeling
function mapGame(s){
  const labels=shuffle(MAPSPOTS.map(m=>m.k));const placed={};let sel=null,wrongs=0;run.max+=60;
  const svg=()=>`<svg viewBox="0 0 520 380" role="img" aria-label="Map of West Africa with six numbered spots">
   <rect width="520" height="380" fill="#9CC9E6"/>
   <path d="M120 0 L520 0 L520 300 C470 290 430 300 400 296 C360 292 320 300 280 292 C240 286 200 300 170 290 C140 282 125 260 120 230 C110 190 90 160 100 120 C108 80 118 40 120 0Z" fill="#EBCB8B" stroke="#2A1B0F" stroke-width="3"/>
   <path d="M100 160 C140 170 200 175 260 172 C330 170 420 176 520 170 L520 300 C470 290 430 300 400 296 C360 292 320 300 280 292 C240 286 200 300 170 290 C140 282 125 260 120 230 C110 190 95 175 100 160Z" fill="#B7CF84"/>
   <path d="M150 262 C190 220 230 180 300 150 C340 160 380 190 420 230 C440 260 450 280 460 300" stroke="#2F7FB8" stroke-width="7" fill="none" stroke-linecap="round"/>
   <path d="M380 300 L520 300 L520 380 L380 380Z" fill="#7FB6DC"/>
   ${MAPSPOTS.map((m,i)=>{const p=placed[m.k];const ok=p===true;return `<g class="spot" data-k="${m.k}" role="button" aria-label="Spot ${i+1}${ok?': '+m.k:''}" tabindex="0">
     <circle cx="${m.x}" cy="${m.y}" r="18" fill="${ok?'#2E8B57':'#2A1B0F'}" stroke="#fff" stroke-width="3"/>
     <text x="${m.x}" y="${m.y+6}" text-anchor="middle" font-family="Cinzel, Georgia, serif" font-weight="900" font-size="18" fill="#fff">${ok?'✓':i+1}</text>
     ${ok?`<text x="${m.x}" y="${m.y-26}" text-anchor="middle" font-family="Nunito, Verdana, sans-serif" font-weight="900" font-size="15" fill="#2A1B0F" stroke="#F6EAD0" stroke-width="4" paint-order="stroke">${m.k}</text>`:''}</g>`}).join('')}
  </svg>`;
  const render=(msg)=>{
    card(`${head(s)}<p class="q">${s.prompt}</p>
    <div class="bank">${labels.map(l=>`<button class="pill ${sel===l?'sel':''} ${placed[l]===true?'used':''}" type="button" data-l="${l}">${l}</button>`).join('')}</div>
    <div class="wa">${svg()}</div><div id="fb">${msg||''}</div>`);
    $('card').querySelectorAll('.pill').forEach(b=>b.onclick=()=>{sel=b.dataset.l;render()});
    $('card').querySelectorAll('.spot').forEach(g=>{const act=()=>{if(!sel){render('<div class="fb bad">Tap a label first, then tap a numbered spot.</div>');return}
      if(g.dataset.k===sel){placed[sel]=true;sel=null;
        if(MAPSPOTS.every(m=>placed[m.k]===true)){const gld=Math.max(15,60-wrongs*5);run.earned+=gld;render(`<div class="fb ok"><b>Map complete! +${gld} gold.</b> The Sahara is north, the Atlantic is west, the Gulf of Guinea is south, and Timbuktu and Djenne sit near the Niger River.</div><div class="row"><button class="big" type="button" id="nx">Continue</button></div>`);$('nx').onclick=finish;$('nx').focus()}
        else render('<div class="fb ok">Correct!</div>')}
      else{wrongs++;render('<div class="fb bad">Not that spot. Hint: reread the story box for which direction each place is.</div>')}};
      g.onclick=act;g.onkeydown=e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();act()}}});
  };render();
}
function finale(){
  const stars=Object.values(best).reduce((a,b)=>a+b,0);
  card(`<span class="std">Quest complete</span><h2 id="ctitle">You crossed castles and caravans!</h2>
  <p style="font-size:18px">You collected <b>${coins} gold</b> and <b>${stars} of 27 stars</b>. Mansa Musa would be proud!</p>
  <p>Your secret code is:</p><p class="codebox">${END_CODE}</p>
  <p>Write this code down and turn it in to your teacher.</p>
  <div class="row"><button class="big" type="button" id="back">Back to the map</button><button class="ghost" type="button" id="reset">Start a new quest</button></div>`);
  $('back').onclick=close;$('reset').onclick=()=>{coins=0;done={};best={};save();close()};
}
refresh();
if(!Object.keys(done).length){card(`<span class="std">Welcome, traveler</span><h2 id="ctitle">Castles &amp; Caravans</h2>
<div class="lore">Your quest takes you from the castles and manors of medieval Europe to the golden kingdoms of West Africa. Visit all <b>9 stations</b> on the map, earn gold for correct answers, and unlock the secret code at the end!</div>
<p>Tap any numbered station to begin. Read the story box at each station first. It holds the clues you need.</p>
<div class="row"><button class="big" type="button" id="start">Start the quest</button></div>`);$('start').onclick=close}
})();
</script>
</body>
</html>
