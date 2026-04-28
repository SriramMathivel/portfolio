<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vidhya — Product Designer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
:root{
  --rose:#c9607a; --rose-deep:#a03050;
  --blush:#f5dde3; --blush-mid:#eecad2;
  --cream:#faf6f2; --warm-white:#fefcfa; --paper:#f7f2ee;
  --text-dark:#1a1614; --text-mid:#4a3f3a; --text-light:#9a8880;
  --lavender:#b5a8d0; --sage:#8aab8c; --peach:#e8b89a;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{font-family:'DM Sans',sans-serif;background:var(--warm-white);color:var(--text-dark);overflow-x:hidden;cursor:none;}

/* ── CURSOR ── */
#cursor{position:fixed;width:10px;height:10px;background:var(--rose);border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);transition:width .25s,height .25s;}
#cursor-ring{position:fixed;width:32px;height:32px;border:1.5px solid rgba(201,96,122,.45);border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:width .3s,height .3s,border-color .3s;}

/* ── NAV ── */
nav{position:fixed;top:0;left:0;right:0;z-index:500;display:flex;align-items:center;justify-content:space-between;padding:1.4rem 3.5rem;background:rgba(254,252,250,0);transition:background .4s,backdrop-filter .4s,box-shadow .4s;}
nav.scrolled{background:rgba(254,252,250,.92);backdrop-filter:blur(16px);box-shadow:0 2px 20px rgba(201,96,122,.07);border-bottom:1px solid rgba(201,96,122,.08);}
.nav-logo{font-family:'Playfair Display',serif;font-size:1.5rem;font-style:italic;color:var(--rose);}
.nav-links{display:flex;gap:2.5rem;align-items:center;}
.nav-links a{text-decoration:none;font-size:.82rem;font-weight:400;color:var(--text-mid);letter-spacing:.06em;text-transform:uppercase;transition:color .2s;position:relative;}
.nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;width:0;height:1px;background:var(--rose);transition:width .3s;}
.nav-links a:hover{color:var(--rose);}
.nav-links a:hover::after,.nav-links a.active::after{width:100%;}
.nav-links a.active{color:var(--rose);}
.nav-cta{background:var(--rose)!important;color:white!important;padding:.5rem 1.3rem;border-radius:2rem;text-transform:uppercase!important;font-size:.78rem!important;transition:background .2s,transform .2s!important;}
.nav-cta::after{display:none!important;}
.nav-cta:hover{background:#a03050!important;transform:translateY(-1px)!important;}

/* ── HERO ── */
#hero{
  position:relative;width:100%;height:100vh;overflow:hidden;
  background:linear-gradient(145deg, #faf6f2 0%, #f9eef4 40%, #f5eaf8 75%, #f8ede8 100%);
}
/* soft radial blobs */
#hero::before{
  content:'';position:absolute;inset:0;
  background:
    radial-gradient(ellipse 60% 55% at 70% 60%, rgba(245,221,227,.55) 0%, transparent 70%),
    radial-gradient(ellipse 45% 40% at 20% 30%, rgba(232,224,248,.45) 0%, transparent 65%),
    radial-gradient(ellipse 35% 30% at 85% 15%, rgba(232,184,154,.25) 0%, transparent 60%);
  pointer-events:none;z-index:0;
}

/* floating hearts field */
#hearts-field{position:absolute;inset:0;z-index:1;pointer-events:none;overflow:hidden;}
.fheart{
  position:absolute;bottom:-5%;
  font-size:var(--fs,14px);color:var(--col,var(--rose));
  opacity:0;
  animation:heartFloat var(--dur,10s) var(--delay,0s) infinite linear;
  user-select:none;will-change:transform,opacity;
}
@keyframes heartFloat{
  0%  {transform:translateX(0px) translateY(0vh) rotate(-12deg) scale(.85);opacity:0;}
  8%  {opacity:.6;}
  35% {transform:translateX(var(--sx,12px)) translateY(-45vh) rotate(9deg) scale(1.05);}
  65% {transform:translateX(var(--sx2,-8px)) translateY(-75vh) rotate(-7deg) scale(.97);opacity:.35;}
  90% {opacity:.1;}
  100%{transform:translateX(4px) translateY(-108vh) rotate(-4deg) scale(.8);opacity:0;}
}

.hero-content{
  position:absolute;top:50%;left:50%;
  transform:translate(-50%,-50%);
  text-align:center;z-index:10;pointer-events:none;
}
.hero-tag{display:inline-block;font-size:.7rem;letter-spacing:.22em;text-transform:uppercase;color:var(--rose);margin-bottom:1.2rem;opacity:0;animation:fadeUp .8s .3s forwards;}
.hero-name{font-family:'Playfair Display',serif;font-size:clamp(4rem,9vw,8rem);font-weight:900;line-height:.95;color:var(--text-dark);opacity:0;animation:fadeUp .9s .5s forwards;text-shadow:0 4px 40px rgba(201,96,122,.15);}
.hero-name em{font-style:italic;color:var(--rose);display:block;font-size:.52em;font-weight:400;letter-spacing:.06em;}
.hero-sub{font-size:1rem;font-weight:300;color:var(--text-light);margin:1.2rem 0 2.5rem;letter-spacing:.04em;opacity:0;animation:fadeUp .8s .9s forwards;}
.hero-btn{
  display:inline-flex;align-items:center;gap:.6rem;background:var(--rose);color:white;text-decoration:none;
  padding:.9rem 2.2rem;border-radius:3rem;font-size:.82rem;font-weight:500;letter-spacing:.06em;text-transform:uppercase;
  pointer-events:all;cursor:none;box-shadow:0 8px 28px rgba(201,96,122,.3);
  transition:background .2s,transform .2s,box-shadow .2s;opacity:0;animation:fadeUp .8s 1.1s forwards;
}
.hero-btn:hover{background:#a03050;transform:translateY(-2px);box-shadow:0 12px 36px rgba(201,96,122,.4);}
.scroll-hint{
  position:absolute;bottom:2.5rem;left:0;right:0;
  display:flex;flex-direction:column;align-items:center;gap:.5rem;
  color:var(--text-light);font-size:.65rem;letter-spacing:.18em;text-transform:uppercase;
  opacity:0;animation:fadeUp 1s 1.5s forwards;z-index:10;
  text-align:center;
}
.scroll-hint .line{width:1px;height:44px;background:linear-gradient(to bottom,var(--rose),transparent);animation:scrollLine 2s ease-in-out infinite;}
@keyframes scrollLine{0%{transform:scaleY(0);transform-origin:top;}50%{transform:scaleY(1);transform-origin:top;}51%{transform:scaleY(1);transform-origin:bottom;}100%{transform:scaleY(0);transform-origin:bottom;}}

section{position:relative;overflow:hidden;}
.container{max-width:1100px;margin:0 auto;padding:0 3.5rem;}

/* ── ABOUT (compact) ── */
.about{padding:6rem 0;background:var(--warm-white);}
.about-inner{display:grid;grid-template-columns:1fr 1.5fr;gap:5rem;align-items:center;}
.about-3d-card{perspective:1000px;}
.about-card-inner{background:linear-gradient(135deg,var(--blush),#f0e4f0);border:1px solid rgba(201,96,122,.12);border-radius:22px;padding:2.8rem;position:relative;box-shadow:0 8px 40px rgba(201,96,122,.08);will-change:transform;transition:box-shadow .35s ease;}
.about-card-inner::before{content:'';position:absolute;inset:0;border-radius:22px;background:radial-gradient(circle at 25% 25%,rgba(255,255,255,.6),transparent 60%);pointer-events:none;}
.about-quote{font-family:'Playfair Display',serif;font-size:1.2rem;font-style:italic;line-height:1.7;color:var(--text-mid);position:relative;z-index:1;}
.about-quote em{color:var(--rose);font-style:normal;}
.about-quote::before{content:'"';position:absolute;top:-1.5rem;left:-.5rem;font-size:5rem;color:var(--rose);opacity:.12;font-family:'Playfair Display',serif;line-height:1;pointer-events:none;}
.about-badges{display:flex;flex-wrap:wrap;gap:.5rem;margin-top:1.8rem;position:relative;z-index:1;}
.about-badge{padding:.3rem .9rem;border-radius:2rem;font-size:.72rem;font-weight:500;background:white;color:var(--rose);border:1px solid rgba(201,96,122,.2);}
/* right side — compact bio */
.about-bio{display:flex;flex-direction:column;gap:.5rem;}
.sec-label{font-size:.68rem;letter-spacing:.2em;text-transform:uppercase;color:var(--rose);margin-bottom:.6rem;display:block;}
.about-bio h2{font-family:'Playfair Display',serif;font-size:clamp(1.8rem,3vw,2.4rem);line-height:1.1;color:var(--text-dark);}
.about-bio h2 span{font-style:italic;color:var(--rose);}
.about-rule{width:36px;height:2px;background:var(--rose);margin:.9rem 0;}
.about-bio p{font-size:.92rem;line-height:1.8;color:var(--text-mid);font-weight:300;}
.about-bio p strong{color:var(--text-dark);font-weight:500;}
.about-sig{font-family:'Playfair Display',serif;font-style:italic;color:var(--text-light);font-size:.95rem;margin-top:.8rem;display:block;}

/* ── PROJECTS — EQUAL CARDS ── */
.projects{ background:var(--paper); padding:5rem 0 6rem; }
.projects-header{ margin-bottom:3rem; }
.projects-header span{ font-size:.68rem;letter-spacing:.2em;text-transform:uppercase;color:var(--rose);display:block;margin-bottom:.5rem; }
.projects-header h2{ font-family:'Playfair Display',serif;font-size:clamp(1.8rem,3vw,2.4rem);color:var(--text-dark); }
.projects-grid{ display:grid;grid-template-columns:repeat(3,1fr);gap:1.5rem; }
.proj-card{
  background:white;border-radius:16px;overflow:hidden;
  border:1px solid rgba(0,0,0,.05);
  box-shadow:0 4px 20px rgba(0,0,0,.05);
  display:flex;flex-direction:column;
  will-change:transform;
  transition:transform .35s cubic-bezier(.23,1,.32,1),box-shadow .35s ease;
  cursor:none;
}
.proj-card:hover{
  transform:translateY(-6px);
  box-shadow:0 20px 48px rgba(201,96,122,.13),0 4px 16px rgba(0,0,0,.06);
}
.proj-thumb{
  aspect-ratio:16/9;width:100%;
  display:flex;align-items:center;justify-content:center;
  flex-direction:column;gap:.4rem;
  font-size:.72rem;font-style:italic;color:rgba(0,0,0,.22);
  position:relative;overflow:hidden;
}
.proj-thumb::after{
  content:'';position:absolute;inset:0;
  background:linear-gradient(to bottom,transparent 60%,rgba(0,0,0,.04));
}
.proj-thumb.rose{ background:linear-gradient(135deg,#fde8ed,#f5d8e8); }
.proj-thumb.lav{  background:linear-gradient(135deg,#eee8f8,#e4d8f4); }
.proj-thumb.grn{  background:linear-gradient(135deg,#e8f4e8,#d8eed8); }
.proj-thumb-icon{ font-size:1.6rem;opacity:.28; }
.proj-body{ padding:1.5rem;display:flex;flex-direction:column;flex:1;gap:.4rem; }
.proj-tag{
  font-size:.6rem;font-weight:500;letter-spacing:.14em;text-transform:uppercase;
  color:var(--rose);display:flex;align-items:center;gap:.4rem;
}
.proj-tag span{ color:var(--text-light); }
.proj-title{
  font-family:'Playfair Display',serif;
  font-size:1rem;font-weight:700;line-height:1.3;
  color:var(--text-dark);margin-top:.1rem;
}
.proj-desc{
  font-size:.8rem;line-height:1.65;
  color:var(--text-light);font-weight:300;
  flex:1;margin-top:.2rem;
}
.proj-footer{
  display:flex;align-items:center;justify-content:space-between;
  margin-top:1rem;padding-top:1rem;
  border-top:1px solid rgba(0,0,0,.05);
}
.proj-year{ font-size:.62rem;color:var(--text-light);letter-spacing:.06em; }
.proj-link{
  display:inline-flex;align-items:center;gap:.35rem;
  font-size:.7rem;font-weight:500;letter-spacing:.06em;text-transform:uppercase;
  color:var(--rose);text-decoration:none;
  transition:gap .2s;cursor:none;
}
.proj-link:hover{ gap:.6rem; }
.proj-link svg{ transition:transform .2s; }
.proj-link:hover svg{ transform:translateX(2px); }

/* ── GALLERY ── */
.gallery{padding:9rem 0;background:var(--cream);}
.gallery-hdr{display:flex;justify-content:space-between;align-items:flex-end;margin-bottom:4rem;}
.gallery-hdr-l h2{font-family:'Playfair Display',serif;font-size:clamp(2rem,3.5vw,2.8rem);color:var(--text-dark);line-height:1.1;}
.gallery-hdr-l h2 em{color:var(--rose);font-style:italic;}
.gallery-hdr-l p{font-size:.85rem;color:var(--text-light);margin-top:.6rem;font-weight:300;max-width:300px;line-height:1.6;}
.gfilter{display:flex;gap:.5rem;flex-wrap:wrap;}
.gfbtn{padding:.38rem .95rem;border-radius:2rem;font-size:.72rem;font-weight:500;background:transparent;border:1px solid rgba(0,0,0,.1);color:var(--text-mid);cursor:none;transition:all .2s;}
.gfbtn.active,.gfbtn:hover{background:var(--rose);color:white;border-color:var(--rose);}
.gallery-grid{columns:3;column-gap:1.2rem;}
.gitem{break-inside:avoid;margin-bottom:1.2rem;border-radius:14px;overflow:hidden;position:relative;cursor:none;border:1px solid rgba(0,0,0,.05);background:white;box-shadow:0 2px 12px rgba(0,0,0,.04);transition:transform .35s cubic-bezier(.34,1.56,.64,1),box-shadow .35s;}
.gitem:hover{transform:translateY(-8px) scale(1.01);box-shadow:0 24px 50px rgba(201,96,122,.14);}
.gitem:hover .g-overlay{opacity:1;}
.gph{width:100%;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:.4rem;font-size:.72rem;color:rgba(0,0,0,.25);font-style:italic;}
.gph-icon{font-size:1.6rem;opacity:.4;}
.g1 .gph{height:240px;background:linear-gradient(135deg,#fde8ed,#f5d8e8);}
.g2 .gph{height:170px;background:linear-gradient(135deg,#e8edf8,#d8e0f4);}
.g3 .gph{height:200px;background:linear-gradient(135deg,#e8f4e8,#d4ecd4);}
.g4 .gph{height:290px;background:linear-gradient(135deg,#fdf0e4,#f5e4cc);}
.g5 .gph{height:185px;background:linear-gradient(135deg,#f4e8f8,#ecd8f4);}
.g6 .gph{height:225px;background:linear-gradient(135deg,#fde8f0,#f8d4e4);}
.g7 .gph{height:160px;background:linear-gradient(135deg,#e8f8f0,#d4f0e4);}
.g8 .gph{height:265px;background:linear-gradient(135deg,#fdf4e4,#f8ecd4);}
.g9 .gph{height:190px;background:linear-gradient(135deg,#f0e8f8,#e4d4f4);}
.g-meta{padding:.9rem 1rem 1rem;background:white;}
.g-meta h4{font-size:.85rem;font-weight:500;color:var(--text-dark);margin-bottom:.2rem;}
.g-meta span{font-size:.72rem;color:var(--text-light);}
.g-overlay{position:absolute;inset:0;background:rgba(201,96,122,.82);display:flex;align-items:center;justify-content:center;opacity:0;transition:opacity .3s;flex-direction:column;gap:.4rem;color:white;font-size:.78rem;font-weight:500;}
.g-overlay-icon{font-size:1.5rem;}
.g-note{text-align:center;margin-top:2.5rem;font-size:.78rem;color:var(--text-light);font-style:italic;}

/* ── LIGHTBOX ── */
.lightbox{position:fixed;inset:0;z-index:800;background:rgba(26,22,20,.88);backdrop-filter:blur(12px);display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .3s;}
.lightbox.open{opacity:1;pointer-events:all;}
.lb-inner{max-width:640px;width:90vw;position:relative;}
.lb-close{position:absolute;top:-3.2rem;right:0;background:none;border:none;color:rgba(255,255,255,.4);font-size:1.4rem;cursor:none;transition:color .2s;line-height:1;}
.lb-close:hover{color:white;}
.lb-img{width:100%;border-radius:12px;overflow:hidden;}
.lb-cap{margin-top:1rem;text-align:center;font-size:.78rem;color:rgba(255,255,255,.35);font-style:italic;}

/* ── FOOTER CTA ── */
.footer-cta{padding:9rem 0 7rem;background:radial-gradient(ellipse at 50% 0%,rgba(201,96,122,.1) 0%,transparent 60%),linear-gradient(180deg,var(--blush),var(--cream));text-align:center;}
.footer-cta h2{font-family:'Playfair Display',serif;font-size:clamp(2.5rem,5vw,4.5rem);margin-bottom:1rem;line-height:1.1;color:var(--text-dark);}
.footer-cta h2 em{font-style:italic;color:var(--rose);}
.ftr-sub{font-size:.95rem;color:var(--text-light);margin-bottom:3rem;font-weight:300;}
.ftr-btns{display:flex;gap:1.2rem;justify-content:center;flex-wrap:wrap;}
.btn-rose{display:inline-flex;align-items:center;gap:.5rem;background:var(--rose);color:white;text-decoration:none;padding:.9rem 2.2rem;border-radius:3rem;font-size:.85rem;font-weight:500;transition:background .2s,transform .2s,box-shadow .2s;cursor:none;box-shadow:0 8px 28px rgba(201,96,122,.25);}
.btn-rose:hover{background:#a03050;transform:translateY(-2px);box-shadow:0 12px 36px rgba(201,96,122,.4);}
.btn-outline{display:inline-flex;align-items:center;gap:.5rem;background:white;color:var(--text-mid);text-decoration:none;padding:.9rem 2.2rem;border-radius:3rem;font-size:.85rem;font-weight:400;border:1px solid rgba(0,0,0,.1);transition:border-color .2s,transform .2s;cursor:none;}
.btn-outline:hover{border-color:var(--rose);transform:translateY(-2px);}
.footer-bar{padding:2rem 3.5rem;background:var(--blush);display:flex;justify-content:space-between;align-items:center;font-size:.75rem;color:var(--text-light);border-top:1px solid rgba(201,96,122,.1);}

/* ── REVEAL ── */
.reveal{opacity:0;transform:translateY(40px);transition:opacity .8s ease,transform .8s ease;}
.reveal.visible{opacity:1;transform:translateY(0);}
.reveal-l{opacity:0;transform:translateX(-50px);transition:opacity .8s ease,transform .8s ease;}
.reveal-l.visible{opacity:1;transform:translateX(0);}
.reveal-r{opacity:0;transform:translateX(50px);transition:opacity .8s ease,transform .8s ease;}
.reveal-r.visible{opacity:1;transform:translateX(0);}
@keyframes fadeUp{from{opacity:0;transform:translateY(22px);}to{opacity:1;transform:translateY(0);}}

@media(max-width:960px){
  nav{padding:1rem 1.5rem;}
  .container{padding:0 1.5rem;}
  .about-inner{grid-template-columns:1fr;gap:3rem;}
  .projects-grid{grid-template-columns:1fr;}
  .gallery-grid{columns:2;}
  .gallery-hdr{flex-direction:column;align-items:flex-start;gap:1.5rem;}
  .ftr-btns{flex-direction:column;align-items:center;}
  .footer-bar{flex-direction:column;gap:.5rem;text-align:center;}
}
@media(max-width:560px){.gallery-grid{columns:1;}}
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- NAV -->
<nav id="nav">
  <div class="nav-logo">δλε</div>
  <div class="nav-links">
    <a href="#projects">Work</a>
    <a href="#about">About</a>
    <a href="#gallery">Art</a>
    <a href="#contact">Contact</a>
    <a href="vidhya-resume.pdf" target="_blank" rel="noopener" class="nav-cta">Resume</a>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div id="hearts-field"></div>
  <div class="hero-content">
    <p class="hero-tag">Product Designer · Coimbatore · 2024</p>
    <h1 class="hero-name">It's Vidhya<em>Designing systems for humans</em></h1>
    <p class="hero-sub">Where logic meets empathy — and systems become stories.</p>
    <a href="#projects" class="hero-btn">
      Explore My Work
      <svg width="14" height="14" viewBox="0 0 14 14" fill="none"><path d="M2 7h10M8 3l4 4-4 4" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
    </a>
  </div>
  <div class="scroll-hint"><div class="line"></div><span>Scroll</span></div>
</section>

<!-- PROJECTS -->
<section class="projects" id="projects">
  <div class="container">
    <div class="projects-header reveal">
      <span>Selected Works</span>
      <h2>Three projects. One designer.</h2>
    </div>
    <div class="projects-grid">

      <!-- Card 1 -->
      <div class="proj-card reveal" style="transition-delay:.08s">
        <div class="proj-thumb rose">
          <img src="Zoom.jpg" alt="Zoom Redesign project thumbnail" style="width:100%;height:100%;object-fit:cover;display:block;">
        </div>
        <div class="proj-body">
          <p class="proj-tag">Education <span>·</span> UX Design</p>
          <h3 class="proj-title">Why Does Learning Online Feel So Lonely?</h3>
          <p class="proj-desc">Redesigning Zoom's educational experience — from meetings built for adults to spaces that actually support learning.</p>
          <div class="proj-footer">
            <span class="proj-year">2026</span>
            <a href="zoom-case-study.html" class="proj-link">
              Case Study
              <svg width="12" height="12" viewBox="0 0 12 12" fill="none"><path d="M2 6h8M6 2l4 4-4 4" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
            </a>
          </div>
        </div>
      </div>

      <!-- Card 2 -->
      <div class="proj-card reveal" style="transition-delay:.16s">
        <div class="proj-thumb lav">
          <img src="Ajio.png" alt="Project 2 thumbnail" style="width:100%;height:100%;object-fit:cover;display:block;">
        </div>
        <div class="proj-body">
          <p class="proj-tag">Case Study <span>·</span> Product Design</p>
          <h3 class="proj-title">AJIO iOS — Redesigned</h3>
          <p class="proj-desc">From back-tapping frustration to smart contextual navigation — a focused UX case study.</p>
          <div class="proj-footer">
            <span class="proj-year">2026</span>
            <a href="#" class="proj-link">
              Case Study
              <svg width="12" height="12" viewBox="0 0 12 12" fill="none"><path d="M2 6h8M6 2l4 4-4 4" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
            </a>
          </div>
        </div>
      </div>

      <!-- Card 3 -->
      <div class="proj-card reveal" style="transition-delay:.24s">
        <div class="proj-thumb grn">
          <img src="DailyHire.png" alt="Project 3 thumbnail" style="width:100%;height:100%;object-fit:cover;display:block;">
        </div>
        <div class="proj-body">
          <p class="proj-tag">Visual Design <span>·</span> Systems</p>
          <h3 class="proj-title">DailyHire — Designed</h3>
          <p class="proj-desc">From street-corner hiring to smart local discovery — a UX case study for India's daily wage workforce.</p>
          <div class="proj-footer">
            <span class="proj-year">2026</span>
            <a href="#" class="proj-link">
              Case Study
              <svg width="12" height="12" viewBox="0 0 12 12" fill="none"><path d="M2 6h8M6 2l4 4-4 4" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>
            </a>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ABOUT -->
<section class="about" id="about">
  <div class="container">
    <div class="about-inner">
      <div class="about-3d-card reveal-l">
        <div class="about-card-inner" id="aboutCard">
          <p class="about-quote">A <em>Product Designer</em> who spent 6+ years as a System Admin — because every great experience starts with <em>understanding the system behind it.</em></p>
          <div class="about-badges">
            <span class="about-badge">6+ Years in Tech</span>
            <span class="about-badge">ITSM · L2 Support</span>
            <span class="about-badge">Coimbatore</span>
            <span class="about-badge">2024</span>
          </div>
        </div>
      </div>
      <div class="about-bio reveal-r">
        <span class="sec-label">About</span>
        <h2>From Systems <span>to Stories.</span></h2>
        <div class="about-rule"></div>
        <p>I'm <strong>Vidhya</strong> — a Product Designer with a System Admin's brain. I spent 6+ years ensuring systems never missed a beat. Now I design experiences that ensure <strong>humans</strong> don't get left behind.</p>
        <span class="about-sig">— Vid</span>
      </div>
    </div>
  </div>
</section>

<!-- GALLERY -->
<section class="gallery" id="gallery">
  <div class="container">
    <div class="gallery-hdr">
      <div class="gallery-hdr-l"><h2>Beyond the Screen —<br><em>Drawings &amp; Art</em></h2><p>A quiet space for things made by hand. Sketches, illustrations, and visual experiments.</p></div>
      <div class="gfilter"><button class="gfbtn active" data-filter="all">All</button><button class="gfbtn" data-filter="sketch">Sketches</button><button class="gfbtn" data-filter="digital">Digital</button><button class="gfbtn" data-filter="portrait">Portraits</button></div>
    </div>
    <div class="gallery-grid">
      <div class="gitem g1 reveal" data-cat="sketch"><img src="Potrait1.jpeg" alt="Sketch I" class="gph" style="width:100%;height:350px;object-fit:cover;display:block;"><div class="g-meta"><h4>Portrait Sketch </h4><span>Pencil · 2023</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g2 reveal" style="transition-delay:.07s" data-cat="digital"><img src="Eyes.jpeg" alt="Emotions" class="gph" style="width:100%;height:170px;object-fit:cover;display:block;"><div class="g-meta"><h4>Emotions</h4><span>Pencil · 2023</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g3 reveal" style="transition-delay:.14s" data-cat="portrait"><img src="Potrait4.jpeg" alt="Couple Portrait" class="gph" style="width:100%;height:400px;object-fit:cover;display:block;"><div class="g-meta"><h4>Couple Portrait</h4><span>Pencil · 2021</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g4 reveal" style="transition-delay:.21s" data-cat="sketch"><img src="Zen.jpeg" alt="OG Character" class="gph" style="width:100%;height:400px;object-fit:cover;display:block;"><div class="g-meta"><h4>Digital Art</h4><span>Clip Studio · 2024</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g5 reveal" style="transition-delay:.28s" data-cat="digital"><img src="Tengen.jpeg" alt="Anime Experiment" class="gph" style="width:100%;height:250px;object-fit:cover;display:block;"><div class="g-meta"><h4>Demon Slayer</h4><span>Pencil · 2025</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g6 reveal" style="transition-delay:.35s" data-cat="portrait"><img src="Potrait3.jpeg" alt="Women Portrait" class="gph" style="width:100%;height:250px;object-fit:cover;display:block;"><div class="g-meta"><h4>Commissioned Art</h4><span>Pencil · 2022</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g7 reveal" style="transition-delay:.42s" data-cat="sketch"><img src="Potrait2.jpeg" alt="Kim's Portrait" class="gph" style="width:100%;height:350px;object-fit:cover;display:block;"><div class="g-meta"><h4>Korean Women Portrait</h4><span>Pencil · 2020</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g8 reveal" style="transition-delay:.49s" data-cat="digital"><img src="Vampire.jpeg" alt="Abstract Mood" class="gph" style="width:100%;height:250px;object-fit:cover;display:block;"><div class="g-meta"><h4>Vampire</h4><span>Pencil · 2024</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
      <div class="gitem g9 reveal" style="transition-delay:.56s" data-cat="portrait"><img src="Leo.jpeg" alt="Evening Study" class="gph" style="width:100%;height:250px;object-fit:cover;display:block;"><div class="g-meta"><h4>Evening Study</h4><span>Ink · 2026</span></div><div class="g-overlay"><span class="g-overlay-icon">🔍</span><span>View</span></div></div>
    </div>
   <!-- <p class="g-note">Placeholder slots — replace each card with your actual drawings.</p> --> 
  </div>
</section>

<div class="lightbox" id="lightbox">
  <div class="lb-inner"><button class="lb-close" id="lbClose">✕</button><div class="lb-img" id="lbContent"></div><p class="lb-cap" id="lbCap"></p></div>
</div>

<!-- FOOTER -->
<section class="footer-cta" id="contact">
  <div class="container">
    <h2 class="reveal">Let's design<br><em>something meaningful.</em></h2>
    <p class="ftr-sub reveal">Open to full-time, contract &amp; freelance opportunities.</p>
    <div class="ftr-btns reveal"><a href="mailto:hello@vidhya.design" class="btn-rose">✉️ Get in Touch</a><a href="vidhya-resume.pdf" target="_blank" rel="noopener" class="btn-outline">View Resume ↗</a></div>
  </div>
</section>
<footer class="footer-bar"><span>© 2024 Vidhya. All rights reserved.</span><span>Designed with ♥ and structured thinking</span></footer>

<script>
/* ── CURSOR ── */
var cur = document.getElementById('cursor');
var ring = document.getElementById('cursor-ring');
var mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',function(e){mx=e.clientX;my=e.clientY;cur.style.left=mx+'px';cur.style.top=my+'px';});
(function lerp(){rx+=(mx-rx)*0.12;ry+=(my-ry)*0.12;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(lerp);})();
document.querySelectorAll('a,button,.gitem').forEach(function(el){
  el.addEventListener('mouseenter',function(){cur.style.width='18px';cur.style.height='18px';ring.style.width='46px';ring.style.height='46px';ring.style.borderColor='rgba(201,96,122,0.7)';});
  el.addEventListener('mouseleave',function(){cur.style.width='10px';cur.style.height='10px';ring.style.width='32px';ring.style.height='32px';ring.style.borderColor='rgba(201,96,122,0.45)';});
});

/* ── FLOATING HEARTS & FLOWERS ── */
(function(){
  var field = document.getElementById('hearts-field');
  var symbols = ['♥','♡','✦','✿','❋','❀','♡','♥','✦','✿'];
  var colors  = [
    'var(--rose)',
    'var(--lavender)',
    'var(--peach)',
    'rgba(201,96,122,0.55)',
    'var(--blush-mid)',
    'rgba(181,168,208,0.7)',
    'rgba(232,184,154,0.75)'
  ];
  for (var i = 0; i < 26; i++) {
    var h = document.createElement('span');
    h.className = 'fheart';
    h.textContent = symbols[Math.floor(Math.random()*symbols.length)];
    h.style.left    = (Math.random()*100)+'%';
    h.style.setProperty('--fs',   (9 + Math.random()*20)+'px');
    h.style.setProperty('--col',  colors[Math.floor(Math.random()*colors.length)]);
    h.style.setProperty('--dur',  (9 + Math.random()*13)+'s');
    h.style.setProperty('--delay',(Math.random()*16)+'s');
    h.style.setProperty('--sx',   ((Math.random()-0.5)*40)+'px');
    h.style.setProperty('--sx2',  ((Math.random()-0.5)*30)+'px');
    field.appendChild(h);
  }
})();

/* ── HERO SCROLL FADE ── */
window.addEventListener('scroll',function(){
  var s = window.scrollY;
  var hc = document.querySelector('.hero-content');
  var sh = document.querySelector('.scroll-hint');
  var hf = document.getElementById('hearts-field');
  if(hc){ hc.style.opacity = Math.max(0, 1 - s/450); }
  if(sh) sh.style.opacity  = Math.max(0, (1 - s/180) * 0.7);
  if(hf) hf.style.opacity  = Math.max(0, 1 - s/380);
},{passive:true});

/* ── NAV ── */
window.addEventListener('scroll',function(){
  document.getElementById('nav').classList.toggle('scrolled',window.scrollY>60);
},{passive:true});

/* ── SCROLL REVEAL ── */
var ro = new IntersectionObserver(function(es){
  es.forEach(function(e){if(e.isIntersecting){e.target.classList.add('visible');ro.unobserve(e.target);}});
},{threshold:0.1});
document.querySelectorAll('.reveal,.reveal-l,.reveal-r').forEach(function(el){ro.observe(el);});

/* ── SMOOTH RAF CARD TILT ── */
document.querySelectorAll('.about-card-inner').forEach(function(card){
  var raf=null, tRX=0, tRY=0, cRX=0, cRY=0, inside=false;

  function tick(){
    cRX += (tRX-cRX)*0.1;
    cRY += (tRY-cRY)*0.1;
    var tY = inside ? -5 : 0;
    card.style.transform = 'perspective(700px) rotateX('+cRX+'deg) rotateY('+cRY+'deg) translateY('+tY+'px)';
    card.style.boxShadow = inside
      ? '0 18px 40px rgba(201,96,122,0.13),0 4px 12px rgba(0,0,0,0.06)'
      : '';
    var diff = Math.abs(tRX-cRX)+Math.abs(tRY-cRY);
    if(diff > 0.03 || inside){ raf=requestAnimationFrame(tick); }
    else { raf=null; card.style.transform=''; card.style.boxShadow=''; }
  }

  card.addEventListener('mouseenter',function(){ inside=true; if(!raf) tick(); });
  card.addEventListener('mousemove',function(e){
    var r=card.getBoundingClientRect();
    tRY = ((e.clientX-r.left)/r.width  - 0.5)*12;
    tRX = -((e.clientY-r.top) /r.height - 0.5)*8;
    if(!raf) tick();
  });
  card.addEventListener('mouseleave',function(){
    inside=false; tRX=0; tRY=0;
    if(!raf) tick();
  });
});

/* ── ACTIVE NAV ── */
document.querySelectorAll('section[id]').forEach(function(sec){
  new IntersectionObserver(function(es){
    es.forEach(function(e){
      if(e.isIntersecting){
        document.querySelectorAll('.nav-links a').forEach(function(a){a.classList.remove('active');});
        var a=document.querySelector('.nav-links a[href="#'+e.target.id+'"]');
        if(a) a.classList.add('active');
      }
    });
  },{threshold:0.35}).observe(sec);
});

/* ── GALLERY FILTER ── */
document.querySelectorAll('.gfbtn').forEach(function(btn){
  btn.addEventListener('click',function(){
    document.querySelectorAll('.gfbtn').forEach(function(b){b.classList.remove('active');});
    btn.classList.add('active');
    var f=btn.dataset.filter;
    document.querySelectorAll('.gitem').forEach(function(item){
      var show=f==='all'||item.dataset.cat===f;
      item.style.transition='opacity 0.3s,transform 0.3s';
      item.style.opacity=show?'1':'0.15';
      item.style.transform=show?'':'scale(0.93)';
      item.style.pointerEvents=show?'':'none';
    });
  });
});

/* ── LIGHTBOX ── */
var lb=document.getElementById('lightbox'),lbC=document.getElementById('lbContent'),lbCap=document.getElementById('lbCap');
document.querySelectorAll('.gitem').forEach(function(item){
  item.addEventListener('click',function(){
    var ph=item.querySelector('.gph');
    var bg=ph?getComputedStyle(ph).background:'#fde8ed';
    lbC.innerHTML='<div style="aspect-ratio:4/3;background:'+bg+';border-radius:10px;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:1rem;color:rgba(0,0,0,0.25);font-style:italic;font-size:.9rem;">'+(ph?ph.innerHTML:'')+'</div>';
    lbCap.textContent=(item.querySelector('h4')?item.querySelector('h4').textContent:'')+' — '+(item.querySelector('span')?item.querySelector('span').textContent:'');
    lb.classList.add('open');
  });
});
document.getElementById('lbClose').addEventListener('click',function(){lb.classList.remove('open');});
lb.addEventListener('click',function(e){if(e.target===lb)lb.classList.remove('open');});
document.addEventListener('keydown',function(e){if(e.key==='Escape')lb.classList.remove('open');});
</script>
</body>
</html>
