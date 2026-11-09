<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#7047eb">
<title>SmartBook Promoter AI</title>

<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' rx='25' fill='%237047eb'/%3E%3Cpath d='M20 25 Q40 17 50 30 Q60 17 80 25 V75 Q60 67 50 80 Q40 67 20 75Z' fill='white'/%3E%3C/svg%3E">

<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');

:root{
--purple:#7047eb;
--purple2:#9475ff;
--blue:#397bff;
--pink:#f0448b;
--red:#f04462;
--yellow:#ffc247;
--green:#24b47e;
--navy:#202448;
--bg:#f5f6fc;
--white:#ffffff;
--muted:#8589a5;
--border:#ececf5;
--shadow:0 12px 35px rgba(45,35,100,.08);
--radius:20px;
}

*{box-sizing:border-box;margin:0;padding:0}

body{
font-family:'DM Sans',sans-serif;
background:var(--bg);
color:var(--navy);
overflow-x:hidden;
}

button,input,textarea,select{font:inherit}
button{cursor:pointer}
a{text-decoration:none;color:inherit}

.app{
display:flex;
min-height:100vh;
}

/* SIDEBAR */

.sidebar{
width:265px;
height:100vh;
position:fixed;
left:0;
top:0;
background:white;
border-right:1px solid var(--border);
z-index:100;
display:flex;
flex-direction:column;
transition:.35s;
overflow-y:auto;
}

.brand{
display:flex;
align-items:center;
gap:12px;
padding:25px 21px;
border-bottom:1px solid var(--border);
}

.logo{
width:43px;
height:43px;
border-radius:14px;
background:linear-gradient(135deg,#7047eb,#397bff,#f0448b);
display:grid;
place-items:center;
color:white;
font-size:24px;
box-shadow:0 7px 20px #7047eb40;
}

.brand h2{
font-family:'Plus Jakarta Sans';
font-size:16px;
font-weight:800;
letter-spacing:-.6px;
}

.brand small{
color:var(--purple);
font-size:10px;
font-weight:800;
letter-spacing:1.4px;
}

.nav-label{
padding:23px 22px 9px;
font-size:10px;
font-weight:800;
letter-spacing:1.5px;
color:#a3a4b8;
}

.nav-item{
display:flex;
align-items:center;
gap:13px;
padding:12px 17px;
margin:3px 13px;
border-radius:12px;
font-size:13px;
font-weight:600;
color:#777b99;
transition:.25s;
cursor:pointer;
border:0;
background:transparent;
width:calc(100% - 26px);
text-align:left;
}

.nav-item:hover{
background:#f4f0ff;
color:var(--purple);
transform:translateX(3px);
}

.nav-item.active{
background:linear-gradient(100deg,#eee8ff,#f3efff);
color:var(--purple);
font-weight:800;
box-shadow:inset 3px 0 var(--purple);
}

.nav-icon{
font-size:18px;
width:23px;
text-align:center;
}

.sidebar-bottom{
margin-top:auto;
padding:17px;
}

.sidebar-promo{
background:linear-gradient(140deg,#7047eb,#397bff,#b04be8);
border-radius:18px;
padding:19px;
color:white;
position:relative;
overflow:hidden;
}

.sidebar-promo:after{
content:'✦';
position:absolute;
right:10px;
top:5px;
font-size:55px;
opacity:.2;
}

.sidebar-promo h3{font-size:14px;margin-bottom:7px}
.sidebar-promo p{font-size:11px;line-height:1.6;opacity:.9}

.sidebar-promo button{
background:white;
border:0;
border-radius:9px;
padding:9px 13px;
margin-top:13px;
color:var(--purple);
font-weight:800;
font-size:11px;
}

/* MAIN */

.main{
margin-left:265px;
width:calc(100% - 265px);
min-height:100vh;
}

.topbar{
height:78px;
background:rgba(255,255,255,.9);
backdrop-filter:blur(15px);
border-bottom:1px solid var(--border);
display:flex;
align-items:center;
justify-content:space-between;
padding:0 32px;
position:sticky;
top:0;
z-index:50;
}

.search{
width:min(360px,40vw);
position:relative;
}

.search input{
width:100%;
padding:12px 16px 12px 43px;
border:1px solid var(--border);
border-radius:12px;
outline:none;
background:#f8f8fc;
font-size:12px;
}

.search span{
position:absolute;
left:15px;
top:10px;
font-size:17px;
}

.top-actions{
display:flex;
align-items:center;
gap:17px;
}

.top-btn{
width:39px;
height:39px;
border-radius:12px;
border:1px solid var(--border);
background:white;
font-size:17px;
}

.profile{
display:flex;
align-items:center;
gap:10px;
}

.avatar{
width:39px;
height:39px;
display:grid;
place-items:center;
border-radius:13px;
background:linear-gradient(135deg,#7047eb,#f0448b);
color:white;
font-weight:800;
}

.profile-info strong{font-size:12px;display:block}
.profile-info small{font-size:10px;color:var(--muted)}

.mobile-menu{display:none}

/* CONTENT */

.content{
padding:30px;
max-width:1600px;
margin:auto;
}

.page{
display:none;
animation:pageIn .45s ease;
}

.page.active{display:block}

@keyframes pageIn{
from{opacity:0;transform:translateY(12px)}
to{opacity:1;transform:translateY(0)}
}

.page-heading{
display:flex;
justify-content:space-between;
align-items:center;
gap:15px;
margin-bottom:25px;
}

.page-heading h1{
font-family:'Plus Jakarta Sans';
font-size:clamp(22px,3vw,30px);
font-weight:800;
letter-spacing:-1.3px;
}

.page-heading p{
font-size:12px;
color:var(--muted);
margin-top:6px;
}

/* BUTTONS */

.btn{
border:0;
padding:12px 17px;
border-radius:11px;
font-size:12px;
font-weight:800;
transition:.25s;
display:inline-flex;
align-items:center;
justify-content:center;
gap:8px;
}

.btn:hover{
transform:translateY(-3px);
box-shadow:0 8px 20px #7047eb30;
}

.primary{
background:linear-gradient(110deg,#7047eb,#397bff);
color:white;
}

.secondary{
background:#eee9ff;
color:var(--purple);
}

.success{background:#e4f8ef;color:#169763}
.danger{background:#fff0f2;color:#e34561}
.light{background:white;border:1px solid var(--border);color:var(--navy)}

.full{width:100%}

/* HERO */

.hero{
background:linear-gradient(115deg,#3821a7,#7047eb 48%,#397bff 100%);
border-radius:25px;
padding:36px;
color:white;
position:relative;
overflow:hidden;
margin-bottom:25px;
min-height:260px;
display:flex;
align-items:center;
}

.hero:before{
content:'';
position:absolute;
width:310px;
height:310px;
border:1px solid #ffffff25;
border-radius:50%;
right:9%;
top:-140px;
box-shadow:0 0 0 35px #ffffff09,0 0 0 70px #ffffff08;
animation:orbit 18s linear infinite;
}

@keyframes orbit{to{transform:rotate(360deg)}}

.hero-content{position:relative;z-index:2;max-width:650px}

.hero-tag{
background:#ffffff20;
border:1px solid #ffffff30;
padding:8px 13px;
border-radius:30px;
display:inline-block;
font-size:10px;
font-weight:800;
letter-spacing:1px;
margin-bottom:18px;
}

.hero h1{
font-family:'Plus Jakarta Sans';
font-size:clamp(27px,4vw,43px);
font-weight:800;
line-height:1.15;
letter-spacing:-1.5px;
margin-bottom:13px;
}

.hero h1 span{color:#ffe08a}

.hero p{
font-size:13px;
line-height:1.8;
max-width:540px;
opacity:.9;
}

.hero-actions{
display:flex;
gap:11px;
margin-top:23px;
flex-wrap:wrap;
}

.hero-actions .btn{
background:white;
color:var(--purple);
}

.hero-actions .btn:last-child{
background:#ffffff20;
color:white;
border:1px solid #ffffff60;
}

.hero-art{
position:absolute;
right:8%;
font-size:120px;
filter:drop-shadow(0 20px 25px #160d5a70);
animation:float 5s ease-in-out infinite;
}

@keyframes float{
0%,100%{transform:translateY(0) rotate(-5deg)}
50%{transform:translateY(-17px) rotate(5deg)}
}

/* CARDS */

.grid{
display:grid;
gap:17px;
}

.stats-grid{grid-template-columns:repeat(4,1fr)}

.card{
background:white;
border:1px solid var(--border);
border-radius:var(--radius);
padding:21px;
box-shadow:var(--shadow);
transition:.3s;
position:relative;
}

.card:hover{
transform:translateY(-5px);
box-shadow:0 18px 35px #5540a51b;
}

.stat-card{
overflow:hidden;
}

.stat-card:after{
content:'';
width:100px;
height:100px;
position:absolute;
right:-30px;
bottom:-35px;
border-radius:50%;
background:var(--glow);
opacity:.10;
}

.stat-top{
display:flex;
justify-content:space-between;
align-items:center;
}

.stat-icon{
width:43px;
height:43px;
display:grid;
place-items:center;
font-size:21px;
border-radius:14px;
background:var(--soft);
}

.stat-card h2{
font-size:29px;
font-weight:800;
margin-top:18px;
letter-spacing:-1px;
}

.stat-card p{font-size:11px;color:var(--muted);margin-top:5px}
.stat-change{font-size:10px;color:var(--green);font-weight:800}

.section-title{
display:flex;
justify-content:space-between;
align-items:center;
margin:27px 0 15px;
}

.section-title h2{
font-family:'Plus Jakarta Sans';
font-size:17px;
font-weight:800;
}

.section-title span{font-size:11px;color:var(--purple);font-weight:800;cursor:pointer}

/* QUICK ACTIONS */

.quick-grid{grid-template-columns:repeat(3,1fr)}

.quick-card{
padding:19px;
display:flex;
gap:14px;
align-items:center;
cursor:pointer;
}

.quick-icon{
width:45px;
height:45px;
border-radius:14px;
display:grid;
place-items:center;
font-size:21px;
flex-shrink:0;
}

.quick-card h3{font-size:12px;font-weight:800}
.quick-card p{font-size:10px;color:var(--muted);margin-top:5px}

/* DASHBOARD LOWER */

.lower-grid{
grid-template-columns:1.4fr 1fr;
}

.activity{
display:flex;
gap:13px;
padding:13px 0;
border-bottom:1px solid var(--border);
align-items:center;
}

.activity:last-child{border:0}

.activity-icon{
width:37px;
height:37px;
display:grid;
place-items:center;
background:#f1edff;
border-radius:12px;
}

.activity h4{font-size:11px}
.activity p{font-size:10px;color:var(--muted);margin-top:4px}

.progress-row{margin-top:17px}
.progress-row div:first-child{
display:flex;
justify-content:space-between;
font-size:11px;
margin-bottom:8px;
font-weight:700;
}

.progress{
height:8px;
background:#eeeef5;
border-radius:20px;
overflow:hidden;
}

.progress span{
display:block;
height:100%;
border-radius:20px;
background:linear-gradient(90deg,#7047eb,#397bff);
}

/* FORMS */

.form-grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:16px;
}

.field{margin-bottom:15px}

.field label{
display:block;
font-size:11px;
font-weight:800;
margin-bottom:8px;
}

.field input,.field textarea,.field select{
width:100%;
padding:13px;
border:1px solid #e7e7f1;
border-radius:11px;
outline:none;
background:#fafaff;
font-size:12px;
color:var(--navy);
transition:.2s;
}

.field input:focus,.field textarea:focus,.field select:focus{
border-color:var(--purple);
box-shadow:0 0 0 3px #7047eb15;
}

.field textarea{
resize:vertical;
min-height:110px;
line-height:1.7;
}

.output{
margin-top:20px;
padding:20px;
background:#faf9ff;
border:1px solid #e9e1ff;
border-radius:15px;
display:none;
}

.output.show{display:block;animation:pageIn .3s}

.output-head{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:13px;
}

.output-head h3{font-size:13px;color:var(--purple)}

.output-text{
white-space:pre-wrap;
font-size:12px;
line-height:1.9;
color:#4c506d;
}

/* TABLE */

.table-wrap{overflow-x:auto}

table{
width:100%;
border-collapse:collapse;
min-width:550px;
}

th,td{
padding:14px 12px;
border-bottom:1px solid var(--border);
text-align:left;
font-size:11px;
}

th{
color:var(--muted);
font-weight:800;
background:#fafaff;
}

td{font-weight:600}

.badge{
display:inline-block;
padding:6px 10px;
border-radius:20px;
background:#e9f8f0;
color:#179b67;
font-size:9px;
font-weight:800;
}

/* BOOK LIBRARY */

.book-grid{
grid-template-columns:repeat(3,1fr);
}

.book-cover{
height:175px;
border-radius:13px;
display:grid;
place-items:center;
background:linear-gradient(145deg,#7047eb,#397bff);
color:white;
font-size:43px;
margin-bottom:15px;
overflow:hidden;
}

.book-cover img{
width:100%;
height:100%;
object-fit:cover;
}

.book-card h3{font-size:13px;margin-bottom:6px}
.book-card p{font-size:10px;color:var(--muted);margin-bottom:12px}

.book-actions{display:flex;gap:7px;flex-wrap:wrap}

/* TOOL CARDS */

.tool-grid{grid-template-columns:repeat(3,1fr)}

.tool-card{
text-align:left;
cursor:pointer;
border:1px solid var(--border);
}

.tool-card .quick-icon{margin-bottom:15px}
.tool-card h3{font-size:13px;margin-bottom:7px}
.tool-card p{font-size:11px;color:var(--muted);line-height:1.6}

/* MARKETING */

.marketing-grid{grid-template-columns:repeat(3,1fr)}

.marketing-card{
text-align:center;
padding:27px 20px;
}

.marketing-card .big-icon{font-size:40px;margin-bottom:13px}
.marketing-card h3{font-size:14px;margin-bottom:8px}
.marketing-card p{font-size:11px;color:var(--muted);line-height:1.7;margin-bottom:15px}

/* COVER UPLOAD */

.upload-box{
border:2px dashed #cfc3ff;
border-radius:17px;
padding:35px;
text-align:center;
background:#faf8ff;
cursor:pointer;
}

.upload-box span{font-size:35px}
.upload-box h3{font-size:14px;margin:12px 0 5px}
.upload-box p{font-size:11px;color:var(--muted)}

.preview-image{
max-width:220px;
max-height:300px;
object-fit:contain;
border-radius:12px;
margin:20px auto;
display:none;
}

/* CHART */

.chart-box{height:210px;position:relative}
canvas{width:100%;height:100%}

/* TOAST */

.toast{
position:fixed;
bottom:25px;
right:25px;
background:#202448;
color:white;
padding:14px 20px;
border-radius:12px;
font-size:12px;
box-shadow:0 10px 30px #0003;
z-index:999;
transform:translateY(100px);
opacity:0;
transition:.3s;
}

.toast.show{transform:translateY(0);opacity:1}

/* FAQ */

.faq{
border-bottom:1px solid var(--border);
padding:16px 0;
}

.faq-question{
font-size:12px;
font-weight:800;
cursor:pointer;
display:flex;
justify-content:space-between;
}

.faq-answer{
font-size:11px;
line-height:1.8;
color:var(--muted);
padding-top:12px;
display:none;
}

.faq.open .faq-answer{display:block}

/* SETTINGS */

.setting-row{
display:flex;
justify-content:space-between;
align-items:center;
padding:17px 0;
border-bottom:1px solid var(--border);
gap:15px;
}

.setting-row h4{font-size:12px}
.setting-row p{font-size:10px;color:var(--muted);margin-top:5px}

/* FOOTER */

.footer{
padding:30px;
text-align:center;
font-size:10px;
color:var(--muted);
border-top:1px solid var(--border);
margin-top:40px;
}

.footer strong{color:var(--purple)}

/* MOBILE */

@media(max-width:1100px){
.stats-grid{grid-template-columns:repeat(2,1fr)}
.quick-grid{grid-template-columns:repeat(2,1fr)}
.book-grid,.tool-grid,.marketing-grid{grid-template-columns:repeat(2,1fr)}
}

@media(max-width:760px){

.sidebar{
transform:translateX(-100%);
width:275px;
box-shadow:10px 0 40px #0001;
}

.sidebar.open{transform:translateX(0)}

.main{margin-left:0;width:100%}

.mobile-menu{
display:grid;
place-items:center;
width:38px;
height:38px;
border:0;
background:#f0eaff;
border-radius:11px;
color:var(--purple);
font-size:20px;
}

.topbar{padding:0 13px;height:68px;gap:9px}
.search{width:38%}
.search input{font-size:10px;padding:11px 8px 11px 32px}
.search span{left:10px;top:9px;font-size:14px}
.top-actions{gap:7px}
.profile-info{display:none}
.top-btn{width:34px;height:34px}
.content{padding:17px}

.hero{padding:25px 20px;min-height:290px}
.hero-art{right:5%;bottom:5px;font-size:75px;opacity:.35}
.hero-content{max-width:100%}
.hero p{font-size:12px}

.lower-grid{grid-template-columns:1fr}
.form-grid{grid-template-columns:1fr}
.book-grid,.tool-grid,.marketing-grid{grid-template-columns:1fr 1fr}

.page-heading{align-items:flex-start;flex-direction:column}
}

@media(max-width:430px){
.stats-grid{gap:10px}
.stat-card{padding:14px}
.stat-card h2{font-size:24px}
.quick-grid{grid-template-columns:1fr}
.book-grid,.tool-grid,.marketing-grid{grid-template-columns:1fr}
.hero h1{font-size:27px}
}

@media(prefers-reduced-motion:reduce){
*,*:before,*:after{
animation:none!important;
transition:none!important;
scroll-behavior:auto!important;
}
}
button:disabled{opacity:.65;cursor:wait;transform:none!important;box-shadow:none!important}
@keyframes aiPulse{0%,100%{opacity:.55;transform:scale(.96)}50%{opacity:1;transform:scale(1.05)}}
</style>
</head>

<body>

<div class="app">

<!-- SIDEBAR -->

<aside class="sidebar" id="sidebar">

<div class="brand">
<div class="logo">📚</div>
<div>
<h2>SmartBook AI</h2>
<small>PUBLISHING INTELLIGENCE</small>
</div>
</div>

<div class="nav-label">WORKSPACE</div>

<button class="nav-item active" data-page="dashboard"><span class="nav-icon">🏠</span> Dashboard</button>
<button class="nav-item" data-page="research"><span class="nav-icon">🔍</span> Book Research</button>
<button class="nav-item" data-page="niche"><span class="nav-icon">💎</span> Niche Finder</button>
<button class="nav-item" data-page="keywords"><span class="nav-icon">🔑</span> Keyword Research</button>
<button class="nav-item" data-page="writing"><span class="nav-icon">✍️</span> AI Writing Studio</button>
<button class="nav-item" data-page="optimizer"><span class="nav-icon">🚀</span> Listing Optimizer</button>
<button class="nav-item" data-page="cover"><span class="nav-icon">🎨</span> Cover Analyzer</button>

<div class="nav-label">MARKETING</div>

<button class="nav-item" data-page="marketing"><span class="nav-icon">📣</span> Marketing Studio</button>
<button class="nav-item" data-page="facebook"><span class="nav-icon">📘</span> Facebook Marketing</button>
<button class="nav-item" data-page="pinterest"><span class="nav-icon">📌</span> Pinterest Marketing</button>
<button class="nav-item" data-page="instagram"><span class="nav-icon">📸</span> Instagram Marketing</button>

<div class="nav-label">MANAGEMENT</div>

<button class="nav-item" data-page="library"><span class="nav-icon">📚</span> Book Library</button>
<button class="nav-item" data-page="analytics"><span class="nav-icon">📊</span> Analytics</button>
<button class="nav-item" data-page="settings"><span class="nav-icon">⚙️</span> Settings</button>

<div class="sidebar-bottom">
<div class="sidebar-promo">
<h3>✨ Your AI Publishing Partner</h3>
<p>Discover opportunities, create better books and grow your publishing business.</p>
<button onclick="navigate('writing')">Start Creating →</button>
</div>
</div>

</aside>

<!-- MAIN -->

<main class="main">

<header class="topbar">

<button class="mobile-menu" id="mobileMenu">☰</button>

<div class="search">
<span>⌕</span>
<input id="globalSearch" placeholder="Search your workspace...">
</div>

<div class="top-actions">
<button class="top-btn" onclick="toast('You are all caught up!')">🔔</button>
<button class="top-btn" onclick="navigate('settings')">⚙️</button>
<div class="profile">
<div class="avatar">S</div>
<div class="profile-info">
<strong>Publisher</strong>
<small>Free Workspace</small>
</div>
</div>
</div>

</header>

<div class="content">
<!-- DASHBOARD -->

<section class="page active" id="dashboard">

<div class="hero">

<div class="hero-content">
<div class="hero-tag">✦ YOUR INTELLIGENT PUBLISHING STUDIO</div>
<h1>Welcome to Your <span>SmartBook</span> Publishing Studio!</h1>
<p>Research smarter. Create exceptional books. Optimise your Amazon listings. Build a publishing business with intelligent tools designed for independent authors.</p>

<div class="hero-actions">
<button class="btn" onclick="navigate('niche')">💎 Discover Niches</button>
<button class="btn" onclick="navigate('writing')">✍️ Start Writing</button>
</div>
</div>

<div class="hero-art">📚</div>

</div>

<div class="grid stats-grid">

<div class="card stat-card" style="--soft:#eee8ff;--glow:#7047eb">
<div class="stat-top">
<div class="stat-icon">📚</div>
<span class="stat-change">Your library</span>
</div>
<h2 id="statBooks">0</h2>
<p>Total Books Saved</p>
</div>

<div class="card stat-card" style="--soft:#e9f1ff;--glow:#397bff">
<div class="stat-top">
<div class="stat-icon">💡</div>
<span class="stat-change">Research tools</span>
</div>
<h2 id="statResearch">0</h2>
<p>Research Projects</p>
</div>

<div class="card stat-card" style="--soft:#fff0e9;--glow:#f04462">
<div class="stat-top">
<div class="stat-icon">✍️</div>
<span class="stat-change">AI Studio</span>
</div>
<h2 id="statContent">0</h2>
<p>Content Generated</p>
</div>

<div class="card stat-card" style="--soft:#e7f8ee;--glow:#24b47e">
<div class="stat-top">
<div class="stat-icon">📣</div>
<span class="stat-change">Marketing</span>
</div>
<h2 id="statMarketing">0</h2>
<p>Marketing Projects</p>
</div>

</div>

<div class="section-title">
<h2>⚡ Quick Actions</h2>
<span onclick="navigate('marketing')">Explore tools →</span>
</div>

<div class="grid quick-grid">

<div class="card quick-card" onclick="navigate('niche')">
<div class="quick-icon" style="background:#eee8ff">💎</div>
<div><h3>Discover Profitable Niches</h3><p>Explore book opportunities</p></div>
</div>

<div class="card quick-card" onclick="navigate('keywords')">
<div class="quick-icon" style="background:#e9f1ff">🔑</div>
<div><h3>Research Amazon Keywords</h3><p>Find relevant search phrases</p></div>
</div>

<div class="card quick-card" onclick="navigate('writing')">
<div class="quick-icon" style="background:#fff0e9">✍️</div>
<div><h3>Generate Book Content</h3><p>Create compelling manuscripts</p></div>
</div>

<div class="card quick-card" onclick="navigate('optimizer')">
<div class="quick-icon" style="background:#e7f8ee">🚀</div>
<div><h3>Optimize Amazon Listing</h3><p>Improve your book presentation</p></div>
</div>

<div class="card quick-card" onclick="navigate('facebook')">
<div class="quick-icon" style="background:#e8f1ff">📘</div>
<div><h3>Create Facebook Promotion</h3><p>Generate organic posts</p></div>
</div>

<div class="card quick-card" onclick="navigate('pinterest')">
<div class="quick-icon" style="background:#fff0f2">📌</div>
<div><h3>Create Pinterest Content</h3><p>Build attractive book pins</p></div>
</div>

</div>

<div class="section-title"><h2>📈 Publishing Overview</h2></div>

<div class="grid lower-grid">

<div class="card">
<div class="section-title" style="margin-top:0">
<h2>Publishing Activity</h2>
<span>Workspace data</span>
</div>
<div class="chart-box"><canvas id="activityChart"></canvas></div>
<p style="font-size:10px;color:var(--muted)">Illustrative activity based on your saved workspace actions, not Amazon sales data.</p>
</div>

<div class="card">
<h2 style="font-size:15px;margin-bottom:15px">Recent Activities</h2>
<div id="recentActivities">
<p style="font-size:11px;color:var(--muted);padding:20px 0">Your recent activities will appear here as you use the tools.</p>
</div>
</div>

</div>

</section>

<!-- BOOK RESEARCH -->

<section class="page" id="research">

<div class="page-heading">
<div>
<h1>🔍 Amazon Book Research</h1>
<p>Understand your competitors and discover opportunities.</p>
</div>
</div>

<div class="card">
<h3 style="font-size:15px;margin-bottom:18px">Research Workspace</h3>

<div class="form-grid">

<div class="field">
<label>Research Keyword or Book Topic</label>
<input id="researchTopic" placeholder="e.g. Kids Travel Guide to Japan">
</div>

<div class="field">
<label>Amazon Marketplace</label>
<select id="researchMarket">
<option>Amazon US</option>
<option>Amazon UK</option>
<option>Amazon Canada</option>
<option>Amazon Australia</option>
<option>Amazon Germany</option>
<option>Amazon France</option>
<option>Amazon Japan</option>
</select>
</div>

<div class="field">
<label>Book Category</label>
<select id="researchCategory">
<option>Children's Books</option>
<option>Travel Guides</option>
<option>Self-Help</option>
<option>Workbooks</option>
<option>Education</option>
<option>Business</option>
<option>Fiction</option>
</select>
</div>

<div class="field">
<label>Research Focus</label>
<select id="researchFocus">
<option>Competitor analysis</option>
<option>Market gaps</option>
<option>Reader needs</option>
<option>Book positioning</option>
</select>
</div>

</div>

<button class="btn primary" onclick="generateTool('research')">🔍 Analyse Book Opportunity</button>

<div class="output" id="researchOutput"></div>

</div>

<div class="section-title"><h2>Competitor Research Tracker</h2></div>

<div class="card">

<p style="font-size:11px;color:var(--muted);margin-bottom:18px">Add competitor information collected from actual Amazon listings. The application does not automatically retrieve live Amazon marketplace data.</p>

<div class="form-grid">
<div class="field"><label>Book Title</label><input id="compTitle" placeholder="Competitor book title"></div>
<div class="field"><label>Author</label><input id="compAuthor" placeholder="Author name"></div>
<div class="field"><label>Price</label><input id="compPrice" placeholder="e.g. £8.99"></div>
<div class="field"><label>Rating</label><input id="compRating" placeholder="e.g. 4.5"></div>
<div class="field"><label>Number of Reviews</label><input id="compReviews" type="number" placeholder="e.g. 125"></div>
<div class="field"><label>BSR</label><input id="compBSR" placeholder="Actual observed BSR"></div>
</div>

<button class="btn primary" onclick="addCompetitor()">+ Add Competitor</button>

<div class="table-wrap" style="margin-top:22px">
<table>
<thead><tr><th>Book Title</th><th>Author</th><th>Price</th><th>Rating</th><th>Reviews</th><th>BSR</th></tr></thead>
<tbody id="competitorTable"><tr><td colspan="6">No competitor records yet.</td></tr></tbody>
</table>
</div>
</div>

</section>

<!-- NICHE FINDER -->

<section class="page" id="niche">

<div class="page-heading">
<div>
<h1>💎 AI Niche Finder</h1>
<p>Discover book ideas and identify opportunities worth researching.</p>
</div>
</div>

<div class="card">

<div class="form-grid">

<div class="field">
<label>Book Category</label>
<select id="nicheCategory">
<option>Children's Books</option>
<option>Family Travel Guides</option>
<option>Travel Guides</option>
<option>Self-Help</option>
<option>Personal Development</option>
<option>Journals and Workbooks</option>
<option>Education</option>
<option>Business</option>
<option>Health and Lifestyle</option>
<option>Fiction</option>
<option>Religion and Inspirational Books</option>
<option>Senior Books</option>
</select>
</div>

<div class="field">
<label>Target Audience</label>
<input id="nicheAudience" placeholder="e.g. Parents with children aged 6–12">
</div>

<div class="field">
<label>Marketplace</label>
<select id="nicheMarket">
<option>Amazon US</option>
<option>Amazon UK</option>
<option>Amazon Canada</option>
<option>Amazon Australia</option>
<option>Amazon Germany</option>
<option>Amazon France</option>
<option>Amazon Japan</option>
</select>
</div>

<div class="field">
<label>Book Format</label>
<select id="nicheFormat">
<option>Paperback</option>
<option>Kindle eBook</option>
<option>Hardcover</option>
</select>
</div>

<div class="field">
<label>Publishing Period</label>
<select id="nichePeriod">
<option>Evergreen</option>
<option>Seasonal</option>
<option>Trending</option>
</select>
</div>

<div class="field">
<label>Competition Preference</label>
<select id="nicheCompetition">
<option>Low competition</option>
<option>Moderate competition</option>
<option>Any competition</option>
</select>
</div>

</div>

<button class="btn primary" onclick="generateTool('niche')">✨ Discover Book Opportunities</button>

<div class="output" id="nicheOutput"></div>

</div>

<div class="section-title"><h2>Research Reminders</h2></div>

<div class="grid quick-grid">
<div class="card"><div class="quick-icon" style="background:#eee8ff">📊</div><h3 style="font-size:13px">Validate Demand</h3><p style="font-size:11px;color:var(--muted);margin-top:8px">Check current marketplace listings and actual reader demand.</p></div>
<div class="card"><div class="quick-icon" style="background:#e9f1ff">🏆</div><h3 style="font-size:13px">Study Competitors</h3><p style="font-size:11px;color:var(--muted);margin-top:8px">Look for gaps in existing books and reader complaints.</p></div>
<div class="card"><div class="quick-icon" style="background:#e7f8ee">💡</div><h3 style="font-size:13px">Create Differently</h3><p style="font-size:11px;color:var(--muted);margin-top:8px">Develop a clear angle that makes your book useful.</p></div>
</div>

</section>

<!-- KEYWORDS -->

<section class="page" id="keywords">

<div class="page-heading">
<div>
<h1>🔑 Keyword Research Assistant</h1>
<p>Generate relevant keyword ideas for your publishing projects.</p>
</div>
</div>

<div class="card">

<div class="form-grid">

<div class="field">
<label>Main Book Topic</label>
<input id="keywordTopic" placeholder="e.g. Kids Travel Guide to Belize">
</div>

<div class="field">
<label>Target Reader</label>
<input id="keywordAudience" placeholder="e.g. Parents and families">
</div>

<div class="field">
<label>Amazon Marketplace</label>
<select id="keywordMarket">
<option>Amazon US</option>
<option>Amazon UK</option>
<option>Amazon Canada</option>
<option>Amazon Australia</option>
<option>Amazon Germany</option>
</select>
</div>

<div class="field">
<label>Book Category</label>
<select id="keywordCategory">
<option>Travel</option>
<option>Children's Books</option>
<option>Self-Help</option>
<option>Education</option>
<option>Business</option>
</select>
</div>

</div>

<button class="btn primary" onclick="generateTool('keywords')">🔑 Generate Keywords</button>

<div class="output" id="keywordsOutput"></div>

</div>

</section>

<!-- WRITING STUDIO -->

<section class="page" id="writing">

<div class="page-heading">
<div>
<h1>✍️ AI Writing Studio</h1>
<p>Your creative workspace for professional book content.</p>
</div>
</div>

<div class="card">

<div class="form-grid">

<div class="field">
<label>Writing Tool</label>
<select id="writingTool">
<option>Book Title Generator</option>
<option>Subtitle Generator</option>
<option>Book Description Generator</option>
<option>Book Introduction</option>
<option>Chapter Outline</option>
<option>Chapter Writing Assistant</option>
<option>Table of Contents</option>
<option>Author Biography</option>
<option>Back Cover Description</option>
<option>Marketing Copy</option>
</select>
</div>

<div class="field">
<label>Book Topic</label>
<input id="writingTopic" placeholder="Enter your book topic">
</div>

<div class="field">
<label>Writing Tone</label>
<select id="writingTone">
<option>Emotional</option>
<option>Conversational</option>
<option>Professional</option>
<option>Persuasive</option>
<option>Storytelling</option>
<option>Educational</option>
<option>Friendly</option>
<option>Inspirational</option>
</select>
</div>

<div class="field">
<label>Target Audience</label>
<input id="writingAudience" placeholder="Who will read this book?">
</div>

<div class="field">
<label>Writing Language</label>
<select id="writingLanguage">
<option>English</option>
<option>French</option>
<option>German</option>
<option>Spanish</option>
<option>Japanese</option>
<option>Italian</option>
<option>Portuguese</option>
</select>
</div>

<div class="field">
<label>Approximate Word Count</label>
<select id="writingWords">
<option>200 words</option>
<option>500 words</option>
<option>800 words</option>
<option>1000 words</option>
<option>1500 words</option>
</select>
</div>

</div>

<div class="field">
<label>Additional Instructions</label>
<textarea id="writingInstructions" placeholder="Describe exactly what you want the AI to create..."></textarea>
</div>

<button class="btn primary" onclick="generateTool('writing')">✨ Generate Content</button>

<div class="output" id="writingOutput"></div>

</div>

<div class="section-title"><h2>Writing Preferences</h2></div>

<div class="grid quick-grid">
<div class="card"><h3 style="font-size:13px">❤️ Human Storytelling</h3><p style="font-size:11px;color:var(--muted);margin-top:8px">Create natural, engaging content that connects with readers.</p></div>
<div class="card"><h3 style="font-size:13px">🎯 Reader Focus</h3><p style="font-size:11px;color:var(--muted);margin-top:8px">Write with a clear audience and practical reader benefits.</p></div>
<div class="card"><h3 style="font-size:13px">📖 Original Content</h3><p style="font-size:11px;color:var(--muted);margin-top:8px">Review and fact-check generated material before publishing.</p></div>
</div>

</section>

<!-- OPTIMIZER -->

<section class="page" id="optimizer">

<div class="page-heading">
<div>
<h1>🚀 Amazon Listing Optimizer</h1>
<p>Improve your book listing's clarity, relevance and reader appeal.</p>
</div>
</div>

<div class="card">

<div class="field"><label>Book Title</label><input id="optTitle" placeholder="Enter your book title"></div>
<div class="field"><label>Subtitle</label><input id="optSubtitle" placeholder="Enter your subtitle"></div>
<div class="field"><label>Target Audience</label><input id="optAudience" placeholder="Describe your ideal reader"></div>
<div class="field"><label>Book Description</label><textarea id="optDescription" style="min-height:190px" placeholder="Paste your current Amazon book description..."></textarea></div>
<div class="field"><label>Seven Backend Keyword Fields</label><textarea id="optKeywords" placeholder="Enter your backend keyword phrases, one per line"></textarea></div>

<button class="btn primary" onclick="generateTool('optimizer')">🚀 Analyse and Improve Listing</button>

<div class="output" id="optimizerOutput"></div>

</div>

</section>

<!-- COVER ANALYZER -->

<section class="page" id="cover">

<div class="page-heading">
<div>
<h1>🎨 Book Cover Analyzer</h1>
<p>Review your book cover and identify visual improvements.</p>
</div>
</div>

<div class="card">

<div class="upload-box" onclick="document.getElementById('coverFile').click()">
<span>🖼️</span>
<h3>Upload Your Book Cover</h3>
<p>Choose a JPG, PNG or WebP image from your device.</p>
<input type="file" id="coverFile" accept="image/*" hidden>
</div>

<img id="coverPreview" class="preview-image" alt="Uploaded book cover">

<div class="field" style="margin-top:20px">
<label>Book Audience</label>
<input id="coverAudience" placeholder="e.g. Parents, children, adult readers">
</div>

<div class="field">
<label>Book Category</label>
<input id="coverCategory" placeholder="e.g. Children's Travel Guide">
</div>

<button class="btn primary" onclick="analyzeCover()">✨ Analyse Cover</button>

<div class="output" id="coverOutput"></div>

</div>

</section>

<!-- MARKETING STUDIO -->

<section class="page" id="marketing">

<div class="page-heading">
<div>
<h1>📣 Marketing Studio</h1>
