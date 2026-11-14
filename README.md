
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>downXload - Apps & Games</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;
 font-family:Arial,sans-serif;
 background:#101827;
 color:white;
}
header{
 background:#17243b;
 padding:22px 12px;
 text-align:center;
}
.logo{font-size:32px;font-weight:bold;color:#20d9a0}
header p{color:#ccd5e4}
.search{
 width:90%;max-width:500px;
 padding:14px;border:0;border-radius:12px;
 margin:12px auto;font-size:16px;
 display:block;
}
nav{text-align:center;padding:12px}
nav button{
 padding:11px 20px;margin:5px;
 border:0;border-radius:20px;
 background:#263a55;color:white;
 font-weight:bold;
}
nav button.active{background:#20d9a0;color:#102033}
h2{text-align:center;color:#20d9a0}
.container{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(145px,1fr));
 gap:13px;padding:14px;
 max-width:1100px;margin:auto;
}
.card{
 background:#1d2b40;
 padding:16px 10px;
 border-radius:14px;
 text-align:center;
 border:1px solid #30445f;
}
.emoji{font-size:36px}
.card h3{font-size:16px;min-height:36px}
.card p{font-size:12px;color:#b9c6d8}
.card a{
 display:block;
 background:#20d9a0;
 color:#102033;
 padding:10px 5px;
 text-decoration:none;
 border-radius:9px;
 font-weight:bold;
 font-size:13px;
}
footer{text-align:center;padding:25px;color:#aebbd0}
</style>
</head>
<body>

<header>
 <div class="logo">downXload</div>
 <p>Download Apps & Games</p>
</header>

<input class="search" id="search"
 placeholder="🔍 Search Apps and Games..."
 oninput="showItems()">

<nav>
 <button class="active" onclick="setCategory('all',this)">All</button>
 <button onclick="setCategory('app',this)">Apps</button>
 <button onclick="setCategory('game',this)">Games</button>
</nav>

<h2 id="heading">All Apps & Games</h2>
<div class="container" id="items"></div>

<footer>
 © 2026 downXload | All Rights Reserved
</footer>

<script>
const data = [
["WhatsApp","app","💬"],
["Instagram","app","📸"],
["Facebook","app","🔵"],
["YouTube","app","▶️"],
["Google Chrome","app","🌐"],
["Google Maps","app","🗺️"],
["Gmail","app","📧"],
["Google Drive","app","☁️"],
["Google Photos","app","🖼️"],
["Google Translate","app","🌍"],
["Telegram","app","✈️"],
["Snapchat","app","👻"],
["Pinterest","app","📌"],
["Spotify","app","🎵"],
["Netflix","app","🎬"],
["Amazon Shopping","app","🛒"],
["Flipkart","app","🛍️"],
["PhonePe","app","💜"],
["Google Pay","app","💳"],
["Paytm","app","💰"],
["Microsoft Word","app","📄"],
["Microsoft Excel","app","📊"],
["Microsoft PowerPoint","app","📽️"],
["Canva","app","🎨"],
["Adobe Acrobat Reader","app","📕"],
["ChatGPT","app","🤖"],
["Duolingo","app","🦉"],
["Khan Academy","app","📚"],
["Wikipedia","app","📖"],
["Shazam","app","🎧"],
["SoundCloud","app","🎼"],
["Discord","app","🎮"],
["Reddit","app","👽"],
["LinkedIn","app","💼"],
["X","app","✖️"],
["Zomato","app","🍔"],
["Swiggy","app","🍕"],
["Uber","app","🚕"],
["Google Meet","app","📹"],
["Zoom","app","💻"],
["Microsoft Teams","app","👥"],
["Notion","app","📝"],
["CapCut","app","🎞️"],
["Snapseed","app","📷"],
["VLC","app","🎥"],
["Files by Google","app","📁"],
["Google Calendar","app","📅"],
["Microsoft OneNote","app","📓"],
["Google Keep","app","📒"],
["Subway Surfers","game","🏃"],
["Temple Run 2","game","🏃"],
["Minecraft","game","⛏️"],
["Roblox","game","🎮"],
["Candy Crush Saga","game","🍬"],
["Ludo King","game","🎲"],
["8 Ball Pool","game","🎱"],
["Hill Climb Racing","game","🚗"],
["Hill Climb Racing 2","game","🏎️"],
["Asphalt 8","game","🏁"],
["Asphalt Legends","game","🚘"],
["Clash of Clans","game","⚔️"],
["Clash Royale","game","👑"],
["Brawl Stars","game","⭐"],
["Stumble Guys","game","🤸"],
["Angry Birds 2","game","🐦"],
["Plants vs Zombies 2","game","🌻"],
["Fruit Ninja","game","🍉"],
["Chess","game","♟️"],
["Carrom Pool","game","🎯"],
["Traffic Rider","game","🏍️"],
["Real Racing 3","game","🏎️"],
["Shadow Fight 2","game","🥷"],
["Shadow Fight 3","game","🥋"],
["Hill Climb Racing","game","🚙"],
["World Cricket Championship 3","game","🏏"],
["Real Cricket","game","🏏"],
["Dream League Soccer","game","⚽"],
["eFootball","game","⚽"],
["EA SPORTS FC Mobile","game","⚽"],
["Pokémon GO","game","⚡"],
["Among Us","game","👨‍🚀"],
["Crossy Road","game","🐔"],
["Geometry Dash Lite","game","🔷"],
["Plants vs Zombies","game","🌱"],
["Sonic Dash","game","🦔"],
["Jetpack Joyride","game","🚀"],
["My Talking Tom 2","game","🐱"],
["Talking Tom Gold Run","game","🏃"],
["Pou","game","👾"],
["Badland","game","🌲"],
["Hungry Shark Evolution","game","🦈"],
["Mini Militia","game","🔫"],
["Fruit Ninja Classic","game","🍎"],
["Cut the Rope","game","🍭"],
["Where's My Water?","game","💧"],
["2048","game","🔢"],
["Sudoku","game","🧩"]
];

let category="all";

function setCategory(value,button){
 category=value;
 document.querySelectorAll("nav button").forEach(b=>b.classList.remove("active"));
 button.classList.add("active");
 document.getElementById("heading").textContent=
 value==="all"?"All Apps & Games":
 value==="app"?"Popular Apps":"Popular Games";
 showItems();
}

function showItems(){
 const search=document.getElementById("search").value.toLowerCase();
 const container=document.getElementById("items");
 container.innerHTML="";

 const filtered=data.filter(item=>
 (category==="all"||item[1]===category)&&
 item[0].toLowerCase().includes(search)
 );

 filtered.forEach(item=>{
 const card=document.createElement("div");
 card.className="card";

 const emoji=document.createElement("div");
 emoji.className="emoji";
 emoji.textContent=item[2];

 const name=document.createElement("h3");
 name.textContent=item[0];

 const type=document.createElement("p");
 type.textContent=item[1]==="app"?"Android App":"Android Game";

 const link=document.createElement("a");
 link.textContent="Download / View";
 link.href="https://play.google.com/store/search?q="+
 encodeURIComponent(item[0])+"&c=apps";
 link.target="_blank";
 link.rel="noopener noreferrer";

 card.append(emoji,name,type,link);
 container.appendChild(card);
 });

 if(filtered.length===0){
 container.textContent="No Apps or Games Found!";
 }
}
showItems();
</script>
</body>
</html>
