<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Orbix — Share Your World</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800;900&family=Instrument+Serif:ital@0;1&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&display=swap" rel="stylesheet">
<style>
/* ========== CSS RESET & VARIABLES ========== */
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
::-webkit-scrollbar{width:5px;}
::-webkit-scrollbar-track{background:var(--bg2);}
::-webkit-scrollbar-thumb{background:var(--accent);border-radius:3px;}

[data-theme="dark"]{
  --bg:#07070f;--bg2:#0d0d1a;--surface:#111120;--card:#17172a;--card2:#1e1e30;
  --border:#252538;--border2:#32324a;--text:#eeeeff;--text2:#9595bb;--text3:#555570;
  --accent:#7c5cfc;--accent2:#fc5c9c;--accent3:#5cf0d8;
  --glow:rgba(124,92,252,0.4);--glow2:rgba(252,92,156,0.3);
  --nav-bg:rgba(7,7,15,0.88);--shadow:0 12px 40px rgba(0,0,0,0.7);
}
[data-theme="light"]{
  --bg:#f2f0ff;--bg2:#e8e4ff;--surface:#fff;--card:#fff;--card2:#f7f5ff;
  --border:#dbd4ff;--border2:#c5bcff;--text:#160f35;--text2:#4a3a78;--text3:#9585c0;
  --accent:#7c5cfc;--accent2:#e8347a;--accent3:#00b8a0;
  --glow:rgba(124,92,252,0.18);--glow2:rgba(232,52,122,0.15);
  --nav-bg:rgba(242,240,255,0.92);--shadow:0 8px 32px rgba(124,92,252,0.14);
}

body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden;transition:background .4s,color .4s;}

/* ========== AUTH SCREEN ========== */
#auth-screen{position:fixed;inset:0;z-index:9999;background:var(--bg);display:flex;align-items:center;justify-content:center;}
.auth-bg-orbs{position:absolute;inset:0;overflow:hidden;pointer-events:none;}
.orb{position:absolute;border-radius:50%;filter:blur(80px);opacity:0.45;animation:orbFloat 8s ease-in-out infinite;}
.orb1{width:400px;height:400px;background:var(--accent);top:-100px;left:-80px;animation-delay:0s;}
.orb2{width:300px;height:300px;background:var(--accent2);bottom:-80px;right:-60px;animation-delay:-3s;}
.orb3{width:200px;height:200px;background:var(--accent3);top:50%;left:60%;animation-delay:-5s;}
@keyframes orbFloat{0%,100%{transform:translate(0,0) scale(1);}50%{transform:translate(20px,-20px) scale(1.05);}}

.auth-box{position:relative;z-index:1;background:rgba(17,17,32,0.85);backdrop-filter:blur(30px);border:1px solid var(--border2);border-radius:28px;padding:48px 42px;width:430px;max-width:95vw;box-shadow:0 24px 80px rgba(0,0,0,0.6),0 0 0 1px rgba(255,255,255,0.05);}
[data-theme="light"] .auth-box{background:rgba(255,255,255,0.9);}
.auth-logo{font-family:'Syne',sans-serif;font-size:2.4rem;font-weight:900;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;letter-spacing:-0.03em;}
.auth-tagline{color:var(--text2);font-size:0.88rem;margin-bottom:36px;margin-top:4px;}
.auth-tabs{display:flex;gap:4px;background:var(--bg2);border-radius:14px;padding:4px;margin-bottom:28px;}
.auth-tab{flex:1;padding:11px;border:none;border-radius:11px;cursor:pointer;font-family:'DM Sans',sans-serif;font-size:0.9rem;font-weight:600;background:transparent;color:var(--text2);transition:all .25s;}
.auth-tab.active{background:var(--accent);color:#fff;box-shadow:0 4px 16px var(--glow);}
.auth-label{display:block;font-size:0.82rem;font-weight:600;color:var(--text2);margin-bottom:7px;}
.auth-input{width:100%;padding:13px 16px;background:var(--bg2);border:1.5px solid var(--border);border-radius:13px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.95rem;outline:none;transition:all .2s;margin-bottom:14px;}
.auth-input:focus{border-color:var(--accent);box-shadow:0 0 0 4px var(--glow);}
.auth-btn{width:100%;padding:14px;background:linear-gradient(135deg,var(--accent),var(--accent2));border:none;border-radius:14px;color:#fff;font-family:'Syne',sans-serif;font-size:1rem;font-weight:800;cursor:pointer;transition:all .2s;letter-spacing:0.04em;margin-top:4px;}
.auth-btn:hover{transform:translateY(-2px);box-shadow:0 10px 30px var(--glow);}
.auth-divider{text-align:center;color:var(--text3);font-size:0.82rem;margin:18px 0;position:relative;}
.auth-divider::before,.auth-divider::after{content:'';position:absolute;top:50%;width:42%;height:1px;background:var(--border);}
.auth-divider::before{left:0;}
.auth-divider::after{right:0;}
.auth-guest-btn{width:100%;padding:13px;background:none;border:1.5px solid var(--border2);border-radius:14px;color:var(--text2);font-family:'DM Sans',sans-serif;font-size:0.93rem;font-weight:600;cursor:pointer;transition:all .2s;}
.auth-guest-btn:hover{border-color:var(--accent);color:var(--accent);}
.auth-error{color:#ff4d6d;font-size:0.83rem;margin-top:6px;margin-bottom:4px;display:none;}
.auth-success{color:#2dd4bf;font-size:0.83rem;margin-top:6px;margin-bottom:4px;display:none;}
.auth-footer{text-align:center;margin-top:20px;font-size:0.82rem;color:var(--text3);}
.auth-footer span{color:var(--accent);cursor:pointer;font-weight:600;}

/* ========== TOAST ========== */
#toast{position:fixed;bottom:28px;right:28px;z-index:9998;display:flex;flex-direction:column;gap:10px;}
.toast-item{padding:14px 20px;border-radius:14px;background:var(--card);border:1px solid var(--border2);color:var(--text);font-size:0.9rem;font-weight:500;box-shadow:var(--shadow);display:flex;align-items:center;gap:10px;animation:toastIn .3s ease;max-width:320px;}
.toast-item.success{border-color:rgba(93,224,163,0.4);}
.toast-item.error{border-color:rgba(255,77,109,0.4);}
@keyframes toastIn{from{opacity:0;transform:translateX(40px);}to{opacity:1;transform:translateX(0);}}

/* ========== MAIN APP ========== */
#app{display:none;}

/* ========== TOP NAV ========== */
.top-nav{position:fixed;top:0;left:0;right:0;z-index:200;height:62px;background:var(--nav-bg);backdrop-filter:blur(24px);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 20px;gap:14px;}
.nav-logo{font-family:'Syne',sans-serif;font-weight:900;font-size:1.5rem;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;letter-spacing:-0.02em;flex-shrink:0;cursor:pointer;}
.nav-search-wrap{flex:1;max-width:340px;position:relative;}
.nav-search-wrap input{width:100%;padding:9px 16px 9px 40px;background:var(--card2);border:1.5px solid var(--border);border-radius:100px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.88rem;outline:none;transition:all .2s;}
.nav-search-wrap input:focus{border-color:var(--accent);background:var(--card);}
.nav-search-icon{position:absolute;left:13px;top:50%;transform:translateY(-50%);color:var(--text3);font-size:0.95rem;}
.nav-right{margin-left:auto;display:flex;align-items:center;gap:10px;}
.nav-btn{width:38px;height:38px;border:1.5px solid var(--border);border-radius:50%;background:var(--card2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:1rem;color:var(--text2);transition:all .2s;position:relative;}
.nav-btn:hover{background:var(--accent);border-color:var(--accent);color:#fff;}
.nav-badge{position:absolute;top:-3px;right:-3px;width:17px;height:17px;background:var(--accent2);border-radius:50%;font-size:0.6rem;color:#fff;display:flex;align-items:center;justify-content:center;font-weight:700;border:2px solid var(--bg);}
.nav-avatar{width:38px;height:38px;border-radius:50%;background:linear-gradient(135deg,var(--accent),var(--accent2));border:2px solid var(--accent);cursor:pointer;display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-size:0.9rem;font-weight:800;color:#fff;position:relative;}

/* Dropdown */
.nav-dropdown{position:absolute;top:50px;right:0;width:220px;background:var(--card);border:1px solid var(--border2);border-radius:16px;padding:8px;box-shadow:var(--shadow);display:none;z-index:300;}
.nav-dropdown.open{display:block;animation:fadeDown .2s ease;}
@keyframes fadeDown{from{opacity:0;transform:translateY(-8px);}to{opacity:1;transform:translateY(0);}}
.dd-item{display:flex;align-items:center;gap:11px;padding:10px 13px;border-radius:10px;cursor:pointer;font-size:0.9rem;color:var(--text2);transition:all .15s;border:none;background:none;width:100%;text-align:left;}
.dd-item:hover{background:var(--bg2);color:var(--text);}
.dd-sep{height:1px;background:var(--border);margin:5px 0;}
.dd-badge{margin-left:auto;font-size:0.7rem;padding:2px 7px;border-radius:20px;background:linear-gradient(135deg,var(--accent),var(--accent2));color:#fff;font-weight:700;}

/* ========== SIDE NAV ========== */
.side-nav{position:fixed;top:62px;left:0;bottom:0;width:218px;background:var(--surface);border-right:1px solid var(--border);padding:16px 10px;overflow-y:auto;z-index:100;display:flex;flex-direction:column;gap:2px;}
.snav-section{margin-bottom:6px;}
.snav-label{font-size:0.68rem;font-weight:700;color:var(--text3);letter-spacing:0.12em;text-transform:uppercase;padding:0 11px 6px;}
.snav-item{display:flex;align-items:center;gap:11px;padding:11px 13px;border-radius:13px;cursor:pointer;font-size:0.9rem;font-weight:500;color:var(--text2);transition:all .2s;border:none;background:none;width:100%;text-align:left;position:relative;}
.snav-item:hover{background:var(--card);color:var(--text);}
.snav-item.active{background:linear-gradient(135deg,rgba(124,92,252,0.18),rgba(252,92,156,0.1));color:var(--accent);border:1.5px solid rgba(124,92,252,0.25);}
.snav-icon{font-size:1.1rem;width:20px;text-align:center;flex-shrink:0;}
.snav-badge{margin-left:auto;font-size:0.7rem;padding:2px 7px;border-radius:20px;background:var(--accent2);color:#fff;font-weight:700;}
.snav-item.admin-item{color:var(--accent2);}
.snav-item.admin-item.active{border-color:rgba(252,92,156,0.3);background:linear-gradient(135deg,rgba(252,92,156,0.12),rgba(124,92,252,0.08));}
.snav-divider{height:1px;background:var(--border);margin:8px 0;}
.snav-user-status{display:flex;align-items:center;gap:9px;padding:10px 13px;font-size:0.82rem;color:var(--text3);}
.online-dot{width:8px;height:8px;border-radius:50%;background:#3dd68c;box-shadow:0 0 8px rgba(61,214,140,0.6);flex-shrink:0;}

/* ========== MAIN CONTENT ========== */
.main{margin-left:218px;margin-top:62px;min-height:calc(100vh - 62px);padding:28px 28px 80px;}

/* ========== PAGES ========== */
.page{display:none;}
.page.active{display:block;animation:pageIn .35s ease;}
@keyframes pageIn{from{opacity:0;transform:translateY(16px);}to{opacity:1;transform:translateY(0);}}

/* ========== PAGE HEADER ========== */
.page-header{margin-bottom:28px;}
.page-header h1{font-family:'Syne',sans-serif;font-size:1.9rem;font-weight:900;letter-spacing:-0.02em;}
.page-header p{color:var(--text2);margin-top:5px;font-size:0.92rem;}

/* ========== BUTTONS ========== */
.btn{padding:10px 22px;border-radius:12px;border:none;cursor:pointer;font-family:'DM Sans',sans-serif;font-size:0.9rem;font-weight:600;transition:all .2s;display:inline-flex;align-items:center;gap:7px;}
.btn-primary{background:linear-gradient(135deg,var(--accent),var(--accent2));color:#fff;}
.btn-primary:hover{transform:translateY(-1px);box-shadow:0 8px 24px var(--glow);}
.btn-outline{background:none;border:1.5px solid var(--border2);color:var(--text2);}
.btn-outline:hover{border-color:var(--accent);color:var(--accent);}
.btn-sm{padding:7px 15px;font-size:0.83rem;border-radius:9px;}

/* ========== CARDS ========== */
.card{background:var(--card);border:1px solid var(--border);border-radius:20px;overflow:hidden;}

/* ============================================================
   PAGE 1 — FEED
============================================================ */
.feed-layout{display:grid;grid-template-columns:1fr 290px;gap:24px;max-width:1060px;}
.feed-col{display:flex;flex-direction:column;gap:18px;}

/* Stories */
.stories-bar{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:14px 16px;}
.stories-bar h3{font-size:0.8rem;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:12px;}
.stories-row{display:flex;gap:12px;overflow-x:auto;padding-bottom:4px;scrollbar-width:none;}
.stories-row::-webkit-scrollbar{display:none;}
.story{display:flex;flex-direction:column;align-items:center;gap:6px;cursor:pointer;flex-shrink:0;}
.story-ring{width:56px;height:56px;border-radius:50%;padding:2.5px;background:linear-gradient(135deg,var(--accent),var(--accent2));transition:transform .2s;}
.story-ring:hover{transform:scale(1.06);}
.story-ring.add{background:var(--border2);}
.story-inner{width:100%;height:100%;border-radius:50%;background:var(--bg2);display:flex;align-items:center;justify-content:center;font-size:1.2rem;border:2.5px solid var(--bg);}
.story-name{font-size:0.72rem;color:var(--text2);font-weight:500;text-align:center;max-width:60px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}

/* Post Card */
.post-card{background:var(--card);border:1px solid var(--border);border-radius:20px;transition:box-shadow .2s;}
.post-card:hover{box-shadow:0 6px 32px var(--glow);}
.post-head{display:flex;align-items:center;gap:12px;padding:16px 18px 10px;}
.post-avatar{width:42px;height:42px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-size:0.95rem;font-weight:800;color:#fff;flex-shrink:0;}
.av-purple{background:linear-gradient(135deg,#7c5cfc,#9b6dff);}
.av-pink{background:linear-gradient(135deg,#fc5c9c,#ff8fb1);}
.av-teal{background:linear-gradient(135deg,#5cf0d8,#00b8a0);}
.av-orange{background:linear-gradient(135deg,#fd9f5a,#e06c2e);}
.av-blue{background:linear-gradient(135deg,#5b9cf6,#1a6ddc);}
.av-green{background:linear-gradient(135deg,#3dd68c,#1aad6a);}
.post-meta{flex:1;}
.post-author-name{font-weight:700;font-size:0.93rem;display:flex;align-items:center;gap:6px;}
.verified{color:var(--accent);font-size:0.85rem;}
.post-time-tag{font-size:0.78rem;color:var(--text3);}
.post-more{width:34px;height:34px;border:none;background:none;cursor:pointer;color:var(--text3);border-radius:50%;font-size:1.1rem;display:flex;align-items:center;justify-content:center;transition:background .2s;}
.post-more:hover{background:var(--bg2);color:var(--text);}
.post-body{padding:0 18px 12px;}
.post-title{font-family:'Syne',sans-serif;font-size:1.08rem;font-weight:800;margin-bottom:7px;letter-spacing:-0.01em;}
.post-text{color:var(--text2);font-size:0.9rem;line-height:1.68;}
.post-tags-row{display:flex;flex-wrap:wrap;gap:5px;margin-top:10px;}
.ptag{font-size:0.77rem;padding:3px 10px;border-radius:100px;background:rgba(124,92,252,0.12);color:var(--accent);border:1px solid rgba(124,92,252,0.22);}
.post-media{line-height:0;}
.post-media-img{width:100%;max-height:400px;object-fit:cover;}
.post-media-emoji{width:100%;height:220px;background:var(--bg2);display:flex;align-items:center;justify-content:center;font-size:5rem;}
.post-actions-bar{display:flex;align-items:center;padding:6px 10px 10px;border-top:1px solid var(--border);margin-top:2px;}
.pact{display:flex;align-items:center;gap:5px;padding:8px 12px;border:none;background:none;cursor:pointer;color:var(--text3);border-radius:10px;font-size:0.87rem;transition:all .2s;font-family:'DM Sans',sans-serif;}
.pact:hover{background:var(--bg2);color:var(--text);}
.pact .pi{font-size:1.05rem;}
.pact.liked{color:#fc5c9c;}
.pact.liked .pi{animation:heartPop .3s ease;}
@keyframes heartPop{0%{transform:scale(1);}50%{transform:scale(1.5);}100%{transform:scale(1);}}
.pact-share{margin-left:auto;}
.pact-save{margin-right:0;}

/* Comments */
.comments-box{border-top:1px solid var(--border);}
.comments-box.hidden{display:none;}
.comments-inner{padding:14px 18px;}
.comments-ttl{font-size:0.78rem;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:12px;}
.cmt{display:flex;gap:9px;margin-bottom:10px;}
.cmt-av{width:30px;height:30px;border-radius:50%;background:linear-gradient(135deg,var(--accent3),var(--accent));display:flex;align-items:center;justify-content:center;font-size:0.72rem;font-weight:700;color:#fff;flex-shrink:0;}
.cmt-bubble{background:var(--bg2);border-radius:12px;padding:9px 13px;flex:1;}
.cmt-name{font-size:0.8rem;font-weight:700;margin-bottom:2px;}
.cmt-text{font-size:0.86rem;color:var(--text2);line-height:1.5;}
.cmt-input-row{display:flex;gap:9px;margin-top:12px;}
.cmt-input{flex:1;padding:9px 14px;background:var(--bg2);border:1.5px solid var(--border);border-radius:100px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.88rem;outline:none;transition:border-color .2s;}
.cmt-input:focus{border-color:var(--accent);}
.cmt-send{padding:9px 18px;background:var(--accent);border:none;border-radius:100px;color:#fff;font-size:0.85rem;font-weight:700;cursor:pointer;transition:opacity .2s;font-family:'DM Sans',sans-serif;}
.cmt-send:hover{opacity:.85;}

/* Feed Sidebar */
.feed-sidebar{display:flex;flex-direction:column;gap:16px;}
.sw{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:18px;}
.sw-title{font-family:'Syne',sans-serif;font-size:0.8rem;font-weight:800;color:var(--text3);text-transform:uppercase;letter-spacing:0.1em;margin-bottom:14px;}
.trend-item{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border);cursor:pointer;}
.trend-item:last-child{border-bottom:none;}
.trend-num{font-family:'Syne',sans-serif;font-size:1rem;font-weight:900;color:var(--accent);width:22px;}
.trend-info{flex:1;}
.trend-tag{font-size:0.88rem;font-weight:600;}
.trend-cnt{font-size:0.76rem;color:var(--text3);}
.sug-user{display:flex;align-items:center;gap:10px;padding:8px 0;}
.sug-av{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:0.8rem;font-weight:700;color:#fff;}
.sug-info{flex:1;}
.sug-name{font-size:0.88rem;font-weight:600;}
.sug-handle{font-size:0.76rem;color:var(--text3);}
.follow-btn{padding:6px 15px;border:1.5px solid var(--accent);border-radius:100px;background:none;color:var(--accent);font-size:0.79rem;font-weight:700;cursor:pointer;transition:all .2s;font-family:'DM Sans',sans-serif;}
.follow-btn:hover{background:var(--accent);color:#fff;}
.follow-btn.following{background:var(--accent);color:#fff;}

/* ============================================================
   PAGE 2 — REELS
============================================================ */
.reels-page-layout{display:flex;height:calc(100vh - 62px - 56px);gap:20px;max-width:900px;}
.reels-main{flex:1;display:flex;align-items:center;justify-content:center;position:relative;}
.reels-feed{width:100%;max-width:400px;height:100%;overflow-y:scroll;scroll-snap-type:y mandatory;-ms-overflow-style:none;scrollbar-width:none;border-radius:20px;}
.reels-feed::-webkit-scrollbar{display:none;}
.reel{height:100%;scroll-snap-align:start;position:relative;background:#000;border-radius:20px;overflow:hidden;margin-bottom:12px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.reel-bg-emoji{font-size:6rem;position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);opacity:0.5;}
.reel-gradient{position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,0.9) 40%,rgba(0,0,0,0.2) 75%,transparent 100%);}
.reel-info-area{position:absolute;bottom:0;left:0;right:60px;padding:22px 18px;}
.reel-author-row{display:flex;align-items:center;gap:9px;margin-bottom:10px;}
.reel-av{width:34px;height:34px;border-radius:50%;background:linear-gradient(135deg,var(--accent),var(--accent2));display:flex;align-items:center;justify-content:center;font-size:0.8rem;font-weight:800;color:#fff;border:2px solid rgba(255,255,255,0.6);}
.reel-author-name{font-size:0.9rem;font-weight:700;color:#fff;}
.reel-follow-pill{padding:4px 12px;border:1.5px solid rgba(255,255,255,0.7);border-radius:100px;font-size:0.75rem;font-weight:700;color:#fff;background:none;cursor:pointer;}
.reel-title{font-family:'Syne',sans-serif;font-size:1rem;font-weight:800;color:#fff;margin-bottom:5px;}
.reel-desc{font-size:0.83rem;color:rgba(255,255,255,0.75);line-height:1.5;}
.reel-hashtags{margin-top:7px;display:flex;gap:6px;flex-wrap:wrap;}
.reel-hash{font-size:0.78rem;color:rgba(255,255,255,0.85);font-weight:500;}
.reel-music{display:flex;align-items:center;gap:6px;margin-top:10px;font-size:0.78rem;color:rgba(255,255,255,0.7);}
.music-icon{animation:spin 3s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.reel-side-actions{position:absolute;bottom:22px;right:10px;display:flex;flex-direction:column;gap:18px;align-items:center;}
.reel-act{display:flex;flex-direction:column;align-items:center;gap:4px;}
.reel-act-btn{width:44px;height:44px;border-radius:50%;background:rgba(255,255,255,0.14);backdrop-filter:blur(10px);border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:1.2rem;color:#fff;transition:all .2s;}
.reel-act-btn:hover{background:rgba(255,255,255,0.28);transform:scale(1.1);}
.reel-act-btn.reel-liked{color:#ff4d6d;background:rgba(255,77,109,0.25);}
.reel-act-cnt{font-size:0.75rem;color:rgba(255,255,255,0.9);font-weight:700;}
.reels-info-panel{width:280px;display:flex;flex-direction:column;gap:14px;padding-top:8px;}
.reels-panel-card{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:18px;}
.reels-panel-title{font-family:'Syne',sans-serif;font-size:0.78rem;font-weight:800;color:var(--text3);text-transform:uppercase;letter-spacing:0.1em;margin-bottom:12px;}
.up-next-item{display:flex;align-items:center;gap:10px;padding:9px 0;border-bottom:1px solid var(--border);cursor:pointer;}
.up-next-item:last-child{border-bottom:none;}
.up-next-thumb{width:44px;height:44px;border-radius:10px;background:var(--bg2);display:flex;align-items:center;justify-content:center;font-size:1.4rem;flex-shrink:0;}
.up-next-info{flex:1;}
.up-next-name{font-size:0.85rem;font-weight:600;}
.up-next-meta{font-size:0.76rem;color:var(--text3);}

/* ============================================================
   PAGE 3 — ARTICLES
============================================================ */
.art-toolbar{display:flex;align-items:center;gap:12px;margin-bottom:24px;flex-wrap:wrap;}
.art-toolbar h1{font-family:'Syne',sans-serif;font-size:1.8rem;font-weight:900;letter-spacing:-0.02em;flex:1;}
.filter-pills{display:flex;gap:6px;flex-wrap:wrap;}
.fpill{padding:7px 16px;border-radius:100px;border:1.5px solid var(--border);background:none;color:var(--text2);font-size:0.85rem;cursor:pointer;transition:all .2s;font-family:'DM Sans',sans-serif;font-weight:500;}
.fpill.active{background:var(--accent);border-color:var(--accent);color:#fff;}
.fpill:hover:not(.active){background:var(--card);}
.art-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(290px,1fr));gap:18px;}
.art-card{background:var(--card);border:1px solid var(--border);border-radius:18px;overflow:hidden;cursor:pointer;transition:transform .25s,box-shadow .25s;}
.art-card:hover{transform:translateY(-4px);box-shadow:0 16px 44px var(--glow);}
.art-cover{height:170px;display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden;}
.art-cover-inner{font-size:4rem;position:relative;z-index:1;}
.art-cover-overlay{position:absolute;inset:0;opacity:0.6;}
.ac-blue{background:linear-gradient(135deg,#1a1a60,#1a4080);}
.ac-pink{background:linear-gradient(135deg,#60102a,#401040);}
.ac-teal{background:linear-gradient(135deg,#0a3040,#0a4030);}
.ac-orange{background:linear-gradient(135deg,#503010,#604020);}
.ac-purple{background:linear-gradient(135deg,#2a1060,#401080);}
.art-cat-pill{position:absolute;top:12px;left:12px;z-index:2;font-size:0.7rem;font-weight:800;text-transform:uppercase;letter-spacing:0.08em;padding:4px 10px;border-radius:100px;background:var(--accent);color:#fff;}
.art-cat-pink{background:var(--accent2);}
.art-cat-teal{background:var(--accent3);color:#000;}
.art-body{padding:16px;}
.art-title{font-family:'Syne',sans-serif;font-size:1.02rem;font-weight:800;margin-bottom:7px;line-height:1.4;letter-spacing:-0.01em;}
.art-excerpt{font-size:0.85rem;color:var(--text2);line-height:1.6;margin-bottom:13px;}
.art-footer{display:flex;align-items:center;justify-content:space-between;}
.art-author{display:flex;align-items:center;gap:7px;}
.art-av{width:26px;height:26px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:0.68rem;font-weight:800;color:#fff;}
.art-author-name{font-size:0.8rem;font-weight:600;}
.art-stats{display:flex;gap:10px;}
.art-stat{font-size:0.76rem;color:var(--text3);display:flex;align-items:center;gap:3px;}
.art-featured{grid-column:1/-1;display:grid;grid-template-columns:1fr 1fr;background:var(--card);border:1px solid var(--border);border-radius:18px;overflow:hidden;cursor:pointer;transition:box-shadow .25s;}
.art-featured:hover{box-shadow:0 12px 40px var(--glow);}
.art-featured-cover{height:100%;min-height:240px;display:flex;align-items:center;justify-content:center;font-size:6rem;position:relative;}
.art-featured-body{padding:28px 24px;display:flex;flex-direction:column;justify-content:center;}
.art-featured-body .art-title{font-size:1.3rem;margin-bottom:10px;}
.art-featured-body .art-excerpt{font-size:0.9rem;margin-bottom:16px;}

/* ============================================================
   PAGE 4 — UPLOAD
============================================================ */
.upload-layout{display:grid;grid-template-columns:1fr 320px;gap:24px;max-width:980px;}
.upload-form-card{background:var(--card);border:1px solid var(--border);border-radius:22px;padding:28px;}
.upload-form-card h2{font-family:'Syne',sans-serif;font-size:1.55rem;font-weight:900;margin-bottom:6px;letter-spacing:-0.02em;}
.upload-form-card .sub{color:var(--text2);font-size:0.9rem;margin-bottom:26px;}
.type-tabs{display:flex;gap:8px;margin-bottom:22px;}
.type-tab{flex:1;padding:14px 8px;border:1.5px solid var(--border);border-radius:14px;background:none;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:5px;color:var(--text2);transition:all .2s;font-family:'DM Sans',sans-serif;}
.type-tab-icon{font-size:1.5rem;}
.type-tab-label{font-size:0.8rem;font-weight:700;}
.type-tab.active{border-color:var(--accent);background:rgba(124,92,252,0.12);color:var(--accent);}
.form-group{margin-bottom:18px;}
.form-label{display:block;font-size:0.83rem;font-weight:700;color:var(--text2);margin-bottom:8px;letter-spacing:0.01em;}
.form-input,.form-textarea,.form-select{width:100%;padding:12px 15px;background:var(--bg2);border:1.5px solid var(--border);border-radius:13px;color:var(--text);font-family:'DM Sans',sans-serif;font-size:0.93rem;outline:none;transition:all .2s;}
.form-input:focus,.form-textarea:focus,.form-select:focus{border-color:var(--accent);box-shadow:0 0 0 4px var(--glow);}
.form-textarea{resize:vertical;min-height:110px;line-height:1.65;}
.form-select option{background:var(--card);}
.drop-zone{border:2px dashed var(--border2);border-radius:16px;padding:38px 20px;text-align:center;cursor:pointer;transition:all .25s;background:var(--bg2);}
.drop-zone:hover,.drop-zone.over{border-color:var(--accent);background:rgba(124,92,252,0.07);}
.drop-icon{font-size:2.8rem;margin-bottom:11px;}
.drop-main{font-size:0.93rem;font-weight:600;margin-bottom:5px;}
.drop-hint{font-size:0.8rem;color:var(--text3);}
.file-preview-bar{margin-top:12px;background:var(--bg);border-radius:12px;padding:13px;display:none;align-items:center;gap:11px;}
.file-preview-bar.show{display:flex;}
.file-preview-icon{font-size:1.8rem;}
.file-preview-info{flex:1;}
.file-preview-name{font-size:0.9rem;font-weight:600;}
.file-preview-size{font-size:0.78rem;color:var(--text3);}
.file-rm{cursor:pointer;font-size:1.1rem;color:var(--text3);background:none;border:none;padding:4px;}
.tags-input-wrap{display:flex;gap:8px;}
.tags-display{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px;}
.tag-chip{font-size:0.8rem;padding:4px 11px;border-radius:100px;background:rgba(124,92,252,0.14);color:var(--accent);border:1px solid rgba(124,92,252,0.28);display:flex;align-items:center;gap:4px;}
.tag-rm{cursor:pointer;opacity:0.7;background:none;border:none;color:var(--accent);font-size:0.9rem;}
.submit-btn{width:100%;padding:15px;background:linear-gradient(135deg,var(--accent),var(--accent2));border:none;border-radius:15px;color:#fff;font-family:'Syne',sans-serif;font-size:1rem;font-weight:900;cursor:pointer;transition:all .2s;letter-spacing:0.04em;margin-top:8px;}
.submit-btn:hover{transform:translateY(-2px);box-shadow:0 10px 32px var(--glow);}
.upload-sidebar .sw{margin-bottom:16px;}
.tip-item{display:flex;gap:10px;padding:9px 0;border-bottom:1px solid var(--border);font-size:0.86rem;color:var(--text2);}
.tip-item:last-child{border-bottom:none;}
.tip-icon{font-size:1rem;flex-shrink:0;}
.upl-stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.upl-stat-box{background:var(--bg2);border-radius:12px;padding:14px;text-align:center;}
.upl-stat-num{font-family:'Syne',sans-serif;font-size:1.5rem;font-weight:900;color:var(--accent);}
.upl-stat-lbl{font-size:0.76rem;color:var(--text3);margin-top:2px;}
.char-count{font-size:0.76rem;color:var(--text3);text-align:right;margin-top:4px;}

/* ============================================================
   PAGE 5 — EXPLORE
============================================================ */
.explore-hero{background:linear-gradient(135deg,var(--accent),var(--accent2),var(--accent3));border-radius:22px;padding:36px 32px;margin-bottom:24px;position:relative;overflow:hidden;}
.explore-hero-pattern{position:absolute;inset:0;opacity:0.15;background:repeating-linear-gradient(45deg,transparent,transparent 15px,rgba(255,255,255,0.1) 15px,rgba(255,255,255,0.1) 30px);}
.explore-hero h2{font-family:'Syne',sans-serif;font-size:1.8rem;font-weight:900;color:#fff;position:relative;z-index:1;}
.explore-hero p{color:rgba(255,255,255,0.85);margin-top:6px;position:relative;z-index:1;font-size:0.92rem;}
.explore-search-big{position:relative;z-index:1;margin-top:20px;display:flex;gap:10px;}
.explore-search-big input{flex:1;padding:14px 20px 14px 48px;background:rgba(255,255,255,0.15);backdrop-filter:blur(12px);border:1.5px solid rgba(255,255,255,0.3);border-radius:14px;color:#fff;font-family:'DM Sans',sans-serif;font-size:0.95rem;outline:none;}
.explore-search-big input::placeholder{color:rgba(255,255,255,0.65);}
.explore-search-big .si{position:absolute;left:16px;top:50%;transform:translateY(-50%);color:rgba(255,255,255,0.75);font-size:1.1rem;}
.explore-search-btn{padding:14px 24px;background:rgba(255,255,255,0.2);border:1.5px solid rgba(255,255,255,0.4);border-radius:14px;color:#fff;font-family:'Syne',sans-serif;font-weight:700;cursor:pointer;font-size:0.9rem;backdrop-filter:blur(8px);}
.explore-cats{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:22px;}
.explore-cat-btn{padding:9px 18px;border-radius:100px;border:1.5px solid var(--border);background:var(--card);color:var(--text2);font-size:0.87rem;cursor:pointer;transition:all .2s;font-family:'DM Sans',sans-serif;font-weight:500;display:flex;align-items:center;gap:6px;}
.explore-cat-btn.active{background:var(--accent);border-color:var(--accent);color:#fff;}
.explore-cat-btn:hover:not(.active){border-color:var(--accent);color:var(--accent);}
.masonry{columns:3;gap:14px;}
.masonry-item{break-inside:avoid;margin-bottom:14px;background:var(--card);border:1px solid var(--border);border-radius:16px;overflow:hidden;cursor:pointer;transition:transform .2s;}
.masonry-item:hover{transform:scale(0.98);}
.masonry-media{width:100%;display:flex;align-items:center;justify-content:center;font-size:3rem;line-height:1;}
.masonry-body{padding:13px;}
.masonry-title{font-weight:700;font-size:0.9rem;margin-bottom:4px;}
.masonry-meta{font-size:0.77rem;color:var(--text3);}
.masonry-tags{display:flex;gap:4px;margin-top:7px;flex-wrap:wrap;}
.masonry-tag{font-size:0.72rem;padding:2px 8px;border-radius:100px;background:rgba(124,92,252,0.12);color:var(--accent);}

/* ============================================================
   PAGE 6 — PROFILE
============================================================ */
.profile-cover-img{height:210px;border-radius:20px;background:linear-gradient(135deg,var(--accent) 0%,var(--accent2) 50%,var(--accent3) 100%);position:relative;overflow:hidden;margin-bottom:-56px;}
.profile-cover-pattern{position:absolute;inset:0;background:repeating-linear-gradient(60deg,transparent,transparent 20px,rgba(255,255,255,0.04) 20px,rgba(255,255,255,0.04) 40px);}
.profile-info-bar{display:flex;align-items:flex-end;gap:18px;padding:0 20px;margin-bottom:22px;}
.profile-big-av{width:96px;height:96px;border-radius:50%;background:linear-gradient(135deg,var(--accent),var(--accent2));display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-size:2rem;font-weight:900;color:#fff;border:4px solid var(--bg);flex-shrink:0;position:relative;z-index:1;}
.profile-details{flex:1;padding-bottom:10px;}
.profile-name-row{font-family:'Syne',sans-serif;font-size:1.55rem;font-weight:900;display:flex;align-items:center;gap:8px;letter-spacing:-0.02em;}
.crown{font-size:1.1rem;}
.profile-handle{color:var(--text3);font-size:0.9rem;margin:3px 0 7px;}
.profile-bio-text{color:var(--text2);font-size:0.9rem;}
.profile-action-btns{display:flex;gap:9px;padding-bottom:10px;}
.pab{padding:10px 22px;border-radius:100px;font-family:'DM Sans',sans-serif;font-size:0.9rem;font-weight:700;cursor:pointer;transition:all .2s;}
.pab-primary{background:var(--accent);border:none;color:#fff;}
.pab-secondary{background:none;border:1.5px solid var(--border2);color:var(--text2);}
.pab:hover{opacity:0.85;}
.profile-stats-bar{display:flex;border-top:1px solid var(--border);border-bottom:1px solid var(--border);margin-bottom:22px;}
.psb{flex:1;text-align:center;padding:18px 8px;border-right:1px solid var(--border);}
.psb:last-child{border-right:none;}
.psb-num{font-family:'Syne',sans-serif;font-size:1.5rem;font-weight:900;color:var(--accent);}
.psb-lbl{font-size:0.76rem;color:var(--text3);margin-top:2px;}
.profile-tabs-bar{display:flex;border-bottom:1px solid var(--border);margin-bottom:22px;}
.ptab{padding:13px 22px;border:none;background:none;cursor:pointer;font-family:'DM Sans',sans-serif;font-size:0.9rem;font-weight:600;color:var(--text2);border-bottom:2px solid transparent;margin-bottom:-1px;transition:all .2s;}
.ptab.active{color:var(--accent);border-bottom-color:var(--accent);}
.media-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;}
.media-thumb{aspect-ratio:1;border-radius:13px;background:var(--card);display:flex;align-items:center;justify-content:center;font-size:2.4rem;cursor:pointer;border:1px solid var(--border);overflow:hidden;transition:transform .2s;position:relative;}
.media-thumb:hover{transform:scale(0.95);}
.media-thumb-overlay{position:absolute;inset:0;background:rgba(0,0,0,0);transition:background .2s;display:flex;align-items:center;justify-content:center;color:#fff;font-size:0.85rem;font-weight:700;opacity:0;}
.media-thumb:hover .media-thumb-overlay{background:rgba(0,0,0,0.45);opacity:1;}
.profile-about-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.about-card{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:18px;}
.about-card h4{font-family:'Syne',sans-serif;font-size:0.85rem;font-weight:800;color:var(--text3);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:12px;}
.about-item{display:flex;gap:10px;padding:8px 0;border-bottom:1px solid var(--border);font-size:0.88rem;color:var(--text2);}
.about-item:last-child{border-bottom:none;}
.about-item-icon{color:var(--accent);font-size:1rem;flex-shrink:0;}

/* ============================================================
   PAGE 7 — ADMIN
============================================================ */
.admin-head{display:flex;align-items:center;gap:14px;margin-bottom:26px;}
.admin-head h1{font-family:'Syne',sans-serif;font-size:1.8rem;font-weight:900;letter-spacing:-0.02em;}
.admin-pill{padding:6px 16px;border-radius:100px;background:linear-gradient(135deg,var(--accent2),var(--accent));color:#fff;font-size:0.8rem;font-weight:800;letter-spacing:0.04em;}
.admin-kpi-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:15px;margin-bottom:26px;}
.kpi-card{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:20px;position:relative;overflow:hidden;}
.kpi-card::before{content:'';position:absolute;top:-30px;right:-30px;width:90px;height:90px;border-radius:50%;opacity:0.12;}
.kpi-purple::before{background:var(--accent);}
.kpi-pink::before{background:var(--accent2);}
.kpi-teal::before{background:var(--accent3);}
.kpi-orange::before{background:#fd9f5a;}
.kpi-icon{font-size:1.7rem;margin-bottom:10px;}
.kpi-num{font-family:'Syne',sans-serif;font-size:1.9rem;font-weight:900;}
.kpi-lbl{font-size:0.82rem;color:var(--text3);margin-top:3px;}
.kpi-change{font-size:0.78rem;color:#3dd68c;margin-top:5px;display:flex;align-items:center;gap:4px;}
.admin-panels{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-bottom:18px;}
.admin-panel{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:20px;}
.ap-title{font-family:'Syne',sans-serif;font-size:0.88rem;font-weight:800;text-transform:uppercase;letter-spacing:0.08em;color:var(--text3);margin-bottom:16px;display:flex;align-items:center;gap:8px;}
.admin-tbl{width:100%;border-collapse:collapse;}
.admin-tbl th{text-align:left;font-size:0.76rem;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:0.06em;padding:0 0 10px;border-bottom:1px solid var(--border);}
.admin-tbl td{padding:12px 0;border-bottom:1px solid var(--border);font-size:0.87rem;color:var(--text2);vertical-align:middle;}
.admin-tbl tr:last-child td{border-bottom:none;}
.user-cell{display:flex;align-items:center;gap:8px;}
.user-cell-av{width:28px;height:28px;border-radius:50%;background:linear-gradient(135deg,var(--accent3),var(--accent));display:flex;align-items:center;justify-content:center;font-size:0.7rem;font-weight:800;color:#fff;}
.status-dot{width:8px;height:8px;border-radius:50%;display:inline-block;}
.s-active{background:#3dd68c;}
.s-pending{background:#fdcb6e;}
.s-banned{background:#ff4d6d;}
.sbadge{font-size:0.74rem;padding:3px 9px;border-radius:100px;font-weight:700;}
.sbadge.active{background:rgba(61,214,140,0.15);color:#3dd68c;}
.sbadge.pending{background:rgba(253,203,110,0.15);color:#fdcb6e;}
.sbadge.banned{background:rgba(255,77,109,0.15);color:#ff4d6d;}
.tbl-btn{padding:4px 11px;border-radius:8px;border:1px solid var(--border);background:none;color:var(--text2);font-size:0.76rem;cursor:pointer;transition:all .2s;margin-right:3px;font-family:'DM Sans',sans-serif;}
.tbl-btn:hover{background:var(--accent);border-color:var(--accent);color:#fff;}
.tbl-btn.danger:hover{background:#ff4d6d;border-color:#ff4d6d;}
.bar-chart{display:flex;flex-direction:column;gap:12px;}
.bar-row{display:flex;align-items:center;gap:10px;}
.bar-lbl{font-size:0.82rem;color:var(--text2);width:72px;flex-shrink:0;}
.bar-track{flex:1;height:8px;background:var(--bg2);border-radius:100px;overflow:hidden;}
.bar-fill{height:100%;border-radius:100px;background:linear-gradient(90deg,var(--accent),var(--accent2));transition:width 1.2s cubic-bezier(.4,0,.2,1);}
.bar-val{font-size:0.82rem;font-weight:700;color:var(--accent);width:36px;text-align:right;}
.report-list{display:flex;flex-direction:column;gap:0;}
.report-row{display:flex;align-items:center;gap:12px;padding:12px 0;border-bottom:1px solid var(--border);}
.report-row:last-child{border-bottom:none;}
.report-type-icon{width:36px;height:36px;border-radius:10px;background:rgba(255,77,109,0.12);display:flex;align-items:center;justify-content:center;font-size:1.2rem;flex-shrink:0;}
.report-info{flex:1;}
.report-title{font-size:0.87rem;font-weight:600;}
.report-meta{font-size:0.76rem;color:var(--text3);}
.admin-full-panel{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:20px;margin-bottom:18px;}

/* ============================================================
   NOTIFICATIONS PANEL
============================================================ */
.notif-panel{position:fixed;top:70px;right:20px;width:320px;background:var(--card);border:1px solid var(--border2);border-radius:20px;box-shadow:var(--shadow);z-index:250;display:none;max-height:480px;overflow-y:auto;}
.notif-panel.open{display:block;animation:fadeDown .2s ease;}
.notif-header{padding:18px 18px 12px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;}
.notif-title{font-family:'Syne',sans-serif;font-weight:800;font-size:1rem;}
.notif-clear{font-size:0.8rem;color:var(--accent);cursor:pointer;background:none;border:none;font-family:'DM Sans',sans-serif;}
.notif-item{display:flex;gap:11px;padding:13px 18px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .15s;}
.notif-item:hover{background:var(--bg2);}
.notif-item:last-child{border-bottom:none;}
.notif-av{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,var(--accent),var(--accent2));display:flex;align-items:center;justify-content:center;font-size:0.82rem;font-weight:800;color:#fff;flex-shrink:0;}
.notif-text{flex:1;font-size:0.86rem;color:var(--text2);line-height:1.5;}
.notif-text strong{color:var(--text);font-weight:700;}
.notif-time{font-size:0.74rem;color:var(--text3);margin-top:3px;}
.notif-dot{width:8px;height:8px;border-radius:50%;background:var(--accent);flex-shrink:0;margin-top:5px;}

/* ============================================================
   SHARE MODAL
============================================================ */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.65);backdrop-filter:blur(6px);z-index:500;display:none;align-items:center;justify-content:center;}
.modal-overlay.open{display:flex;animation:fadeIn .2s ease;}
@keyframes fadeIn{from{opacity:0;}to{opacity:1;}}
.modal-box{background:var(--card);border:1px solid var(--border2);border-radius:22px;padding:28px;width:420px;max-width:95vw;position:relative;animation:fadeUp .25s ease;}
.modal-close{position:absolute;top:16px;right:16px;width:32px;height:32px;border-radius:50%;background:var(--bg2);border:none;cursor:pointer;font-size:1.1rem;display:flex;align-items:center;justify-content:center;color:var(--text2);}
.modal-title{font-family:'Syne',sans-serif;font-size:1.2rem;font-weight:800;margin-bottom:18px;}
.share-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:18px;}
.share-opt{display:flex;flex-direction:column;align-items:center;gap:6px;cursor:pointer;padding:14px 8px;border-radius:14px;border:1px solid var(--border);background:var(--bg2);transition:all .2s;}
.share-opt:hover{border-color:var(--accent);background:rgba(124,92,252,0.1);}
.share-opt-icon{font-size:1.6rem;}
.share-opt-label{font-size:0.76rem;font-weight:600;color:var(--text2);}
.share-link-row{display:flex;gap:8px;}
.share-link-input{flex:1;padding:11px 14px;background:var(--bg2);border:1px solid var(--border);border-radius:11px;color:var(--text);font-size:0.85rem;outline:none;font-family:'DM Sans',sans-serif;}
.copy-btn{padding:11px 18px;background:var(--accent);border:none;border-radius:11px;color:#fff;font-size:0.85rem;font-weight:700;cursor:pointer;font-family:'DM Sans',sans-serif;}

/* ============================================================
   UTILITY
============================================================ */
.hidden{display:none!important;}
.flex{display:flex;}.flex-1{flex:1;}.items-center{align-items:center;}.gap-8{gap:8px;}.gap-12{gap:12px;}
input[type="file"]{display:none;}
</style>
</head>
<body>

<!-- ========== AUTH SCREEN ========== -->
<div id="auth-screen">
  <div class="auth-bg-orbs">
    <div class="orb orb1"></div>
    <div class="orb orb2"></div>
    <div class="orb orb3"></div>
  </div>
  <div class="auth-box">
    <div class="auth-logo">Orbix</div>
    <div class="auth-tagline">Your universe of content — posts, reels, articles & more.</div>
    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchAuthTab('login')">Sign In</button>
      <button class="auth-tab" onclick="switchAuthTab('register')">Register</button>
    </div>
    <!-- Login Form -->
    <div id="login-form">
      <label class="auth-label">Username</label>
      <input class="auth-input" id="login-username" type="text" placeholder="Enter your username" autocomplete="off">
      <label class="auth-label">Password</label>
      <input class="auth-input" id="login-password" type="password" placeholder="Enter your password">
      <div class="auth-error" id="login-error">❌ Invalid username or password.</div>
      <button class="auth-btn" onclick="doLogin()">✦ Sign In to Orbix</button>
      <div class="auth-divider">or</div>
      <button class="auth-guest-btn" onclick="guestLogin()">👁️ Continue as Guest</button>
      <div class="auth-footer">Admin account pre-configured for <span>Vedansh</span></div>
    </div>
    <!-- Register Form -->
    <div id="register-form" style="display:none;">
      <label class="auth-label">Full Name</label>
      <input class="auth-input" id="reg-name" type="text" placeholder="Your full name">
      <label class="auth-label">Username</label>
      <input class="auth-input" id="reg-username" type="text" placeholder="Choose a username">
      <label class="auth-label">Password</label>
      <input class="auth-input" id="reg-password" type="password" placeholder="Create a password">
      <label class="auth-label">Email</label>
      <input class="auth-input" id="reg-email" type="email" placeholder="your@email.com">
      <div class="auth-error" id="reg-error"></div>
      <div class="auth-success" id="reg-success"></div>
      <button class="auth-btn" onclick="doRegister()">🚀 Create Account</button>
      <div class="auth-divider">or</div>
      <button class="auth-guest-btn" onclick="guestLogin()">👁️ Continue as Guest</button>
    </div>
  </div>
</div>

<!-- ========== TOAST ========== -->
<div id="toast"></div>

<!-- ========== SHARE MODAL ========== -->
<div class="modal-overlay" id="share-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('share-modal')">✕</button>
    <div class="modal-title">📤 Share This Post</div>
    <div class="share-grid">
      <div class="share-opt" onclick="showToast('📲 Shared to WhatsApp!','success')"><div class="share-opt-icon">💬</div><div class="share-opt-label">WhatsApp</div></div>
      <div class="share-opt" onclick="showToast('🐦 Shared to Twitter!','success')"><div class="share-opt-icon">🐦</div><div class="share-opt-label">Twitter</div></div>
      <div class="share-opt" onclick="showToast('📘 Shared to Facebook!','success')"><div class="share-opt-icon">📘</div><div class="share-opt-label">Facebook</div></div>
      <div class="share-opt" onclick="showToast('📸 Shared to Instagram!','success')"><div class="share-opt-icon">📸</div><div class="share-opt-label">Instagram</div></div>
      <div class="share-opt" onclick="showToast('✉️ Opened in Mail!','success')"><div class="share-opt-icon">✉️</div><div class="share-opt-label">Email</div></div>
      <div class="share-opt" onclick="showToast('💼 Shared to LinkedIn!','success')"><div class="share-opt-icon">💼</div><div class="share-opt-label">LinkedIn</div></div>
      <div class="share-opt" onclick="showToast('📱 Shared via SMS!','success')"><div class="share-opt-icon">📱</div><div class="share-opt-label">SMS</div></div>
      <div class="share-opt" onclick="showToast('🔗 Copied!','success')"><div class="share-opt-icon">🔗</div><div class="share-opt-label">More</div></div>
    </div>
    <div style="font-size:0.82rem;color:var(--text3);margin-bottom:8px;font-weight:600;">Copy Link</div>
    <div class="share-link-row">
      <input class="share-link-input" id="share-link-val" value="https://orbix.app/post/abc123" readonly>
      <button class="copy-btn" onclick="copyLink()">Copy</button>
    </div>
  </div>
</div>

<!-- ========== MAIN APP ========== -->
<div id="app">

  <!-- Top Nav -->
  <nav class="top-nav">
    <div class="nav-logo" onclick="navTo('feed')">Orbix</div>
    <div class="nav-search-wrap">
      <span class="nav-search-icon">🔍</span>
      <input type="text" placeholder="Search Orbix..." oninput="handleSearch(this.value)">
    </div>
    <div class="nav-right">
      <button class="nav-btn" onclick="navTo('upload')" title="Create Post">✚</button>
      <button class="nav-btn" onclick="toggleNotif()" title="Notifications">
        🔔<span class="nav-badge" id="notif-count">3</span>
      </button>
      <button class="nav-btn" title="Messages" onclick="showToast('💬 Messages coming soon!','success')">✉️</button>
      <button class="nav-btn" onclick="toggleTheme()" id="theme-btn" title="Toggle Theme">🌙</button>
      <div class="nav-avatar" onclick="toggleDropdown()" id="nav-avatar-btn">V
        <div class="nav-dropdown" id="nav-dropdown">
          <div class="dd-item" onclick="navTo('profile');closeDropdown()">👤 My Profile</div>
          <div class="dd-item" onclick="navTo('upload');closeDropdown()">✚ Create Post</div>
          <div class="dd-item" onclick="showToast('⚙️ Settings coming soon!','success');closeDropdown()">⚙️ Settings</div>
          <div class="dd-item" onclick="showToast('🔖 Saved posts coming soon!','success');closeDropdown()">🔖 Saved Posts</div>
          <div class="dd-item" onclick="showToast('📊 Analytics coming soon!','success');closeDropdown()">📊 Analytics</div>
          <div id="admin-dd-item" class="dd-item hidden" onclick="navTo('admin');closeDropdown()">👑 Admin Panel<span class="dd-badge">Admin</span></div>
          <div class="dd-sep"></div>
          <div class="dd-item" onclick="doLogout()">🚪 Sign Out</div>
        </div>
      </div>
    </div>
  </nav>

  <!-- Notifications Panel -->
  <div class="notif-panel" id="notif-panel">
    <div class="notif-header">
      <div class="notif-title">Notifications</div>
      <button class="notif-clear" onclick="clearNotifs()">Mark all read</button>
    </div>
    <div class="notif-item"><div class="notif-av">A</div><div class="notif-info"><div class="notif-text"><strong>Aryan</strong> liked your post "Top Design Trends 2025"</div><div class="notif-time">2 min ago</div></div><div class="notif-dot"></div></div>
    <div class="notif-item"><div class="notif-av" style="background:linear-gradient(135deg,#fc5c9c,#ff8fb1)">S</div><div class="notif-info"><div class="notif-text"><strong>Sanya</strong> started following you</div><div class="notif-time">15 min ago</div></div><div class="notif-dot"></div></div>
    <div class="notif-item"><div class="notif-av" style="background:linear-gradient(135deg,#5cf0d8,#00b8a0)">R</div><div class="notif-info"><div class="notif-text"><strong>Rahul</strong> commented: "This is amazing content!"</div><div class="notif-time">1 hr ago</div></div><div class="notif-dot"></div></div>
    <div class="notif-item"><div class="notif-av" style="background:linear-gradient(135deg,#fdcb6e,#e17055)">P</div><div class="notif-info"><div class="notif-text"><strong>Priya</strong> shared your article to 3 groups</div><div class="notif-time">3 hrs ago</div></div></div>
    <div class="notif-item"><div class="notif-av" style="background:linear-gradient(135deg,#a29bfe,#6c5ce7)">K</div><div class="notif-info"><div class="notif-text"><strong>Karan</strong> mentioned you in a comment</div><div class="notif-time">Yesterday</div></div></div>
  </div>

  <!-- Side Nav -->
  <nav class="side-nav">
    <div class="snav-section">
      <div class="snav-label">Main</div>
      <button class="snav-item active" id="snav-feed" onclick="navTo('feed')"><span class="snav-icon">🏠</span> Home Feed</button>
      <button class="snav-item" id="snav-reels" onclick="navTo('reels')"><span class="snav-icon">🎬</span> Reels</button>
      <button class="snav-item" id="snav-articles" onclick="navTo('articles')"><span class="snav-icon">📝</span> Articles</button>
      <button class="snav-item" id="snav-explore" onclick="navTo('explore')"><span class="snav-icon">🔭</span> Explore</button>
      <button class="snav-item" id="snav-upload" onclick="navTo('upload')"><span class="snav-icon">✚</span> Upload <span class="snav-badge">New</span></button>
    </div>
    <div class="snav-divider"></div>
    <div class="snav-section">
      <div class="snav-label">You</div>
      <button class="snav-item" id="snav-profile" onclick="navTo('profile')"><span class="snav-icon">👤</span> Profile</button>
      <button class="snav-item" onclick="showToast('🔖 Saved coming soon!','success')"><span class="snav-icon">🔖</span> Saved</button>
      <button class="snav-item" onclick="showToast('👥 Friends coming soon!','success')"><span class="snav-icon">👥</span> Following</button>
      <button class="snav-item" onclick="showToast('📊 Analytics coming soon!','success')"><span class="snav-icon">📊</span> Analytics</button>
    </div>
    <div class="snav-divider"></div>
    <div class="snav-section">
      <div class="snav-label">Discover</div>
      <button class="snav-item" onclick="showToast('🎵 Music coming soon!','success')"><span class="snav-icon">🎵</span> Music</button>
      <button class="snav-item" onclick="showToast('🎮 Gaming coming soon!','success')"><span class="snav-icon">🎮</span> Gaming</button>
      <button class="snav-item" onclick="showToast('🌍 Travel coming soon!','success')"><span class="snav-icon">🌍</span> Travel</button>
    </div>
    <div class="snav-divider"></div>
    <div class="snav-section" id="admin-nav-section" style="display:none;">
      <div class="snav-label">Admin</div>
      <button class="snav-item admin-item" id="snav-admin" onclick="navTo('admin')"><span class="snav-icon">👑</span> Admin Panel</button>
      <button class="snav-item admin-item" onclick="showToast('📋 Content mod coming soon!','success')"><span class="snav-icon">🛡️</span> Moderation</button>
      <button class="snav-item admin-item" onclick="showToast('📈 Reports coming soon!','success')"><span class="snav-icon">📈</span> Reports</button>
    </div>
    <div class="snav-divider"></div>
    <div class="snav-user-status"><div class="online-dot"></div><span id="status-name">Online</span></div>
    <div style="padding:6px 13px;font-size:0.76rem;color:var(--text3);">Orbix v2.0 · <span style="color:var(--accent);">Switch Theme</span></div>
  </nav>

  <!-- Main Content -->
  <main class="main">

    <!-- ============================================================
         PAGE 1 — FEED
    ============================================================ -->
    <div class="page active" id="page-feed">
      <div class="feed-layout">
        <div class="feed-col">
          <!-- Stories -->
          <div class="stories-bar">
            <h3>Stories</h3>
            <div class="stories-row">
              <div class="story" onclick="showToast('➕ Add your story','success')">
                <div class="story-ring add"><div class="story-inner">➕</div></div>
                <div class="story-name">Add Story</div>
              </div>
              <div class="story" onclick="showToast('📸 Aryan\'s story','success')">
                <div class="story-ring"><div class="story-inner">🎭</div></div>
                <div class="story-name">Aryan</div>
              </div>
              <div class="story" onclick="showToast('📸 Sanya\'s story','success')">
                <div class="story-ring"><div class="story-inner">🌸</div></div>
                <div class="story-name">Sanya</div>
              </div>
              <div class="story" onclick="showToast('📸 Rahul\'s story','success')">
                <div class="story-ring"><div class="story-inner">🏔️</div></div>
                <div class="story-name">Rahul</div>
              </div>
              <div class="story" onclick="showToast('📸 Priya\'s story','success')">
                <div class="story-ring"><div class="story-inner">🎨</div></div>
                <div class="story-name">Priya</div>
              </div>
              <div class="story" onclick="showToast('📸 Dev\'s story','success')">
                <div class="story-ring"><div class="story-inner">💻</div></div>
                <div class="story-name">Dev</div>
              </div>
              <div class="story" onclick="showToast('📸 Meera\'s story','success')">
                <div class="story-ring"><div class="story-inner">🌺</div></div>
                <div class="story-name">Meera</div>
              </div>
            </div>
          </div>

          <!-- Post 1 -->
          <div class="post-card" id="post-1">
            <div class="post-head">
              <div class="post-avatar av-purple">A</div>
              <div class="post-meta">
                <div class="post-author-name">Aryan Kapoor <span class="verified">✦</span></div>
                <div class="post-time-tag">2 hours ago · 🌍 Public</div>
              </div>
              <button class="post-more" onclick="showToast('⚙️ Post options','success')">⋯</button>
            </div>
            <div class="post-body">
              <div class="post-title">Top UI Design Trends Shaping 2025 🎨</div>
              <div class="post-text">Glassmorphism is back — but smarter. Designers are pairing it with bento grids and bold typography to create interfaces that feel both futuristic and deeply human. Here's what's dominating the design scene this year...</div>
              <div class="post-tags-row">
                <span class="ptag">#Design</span><span class="ptag">#UI</span><span class="ptag">#2025</span><span class="ptag">#Trends</span>
              </div>
            </div>
            <div class="post-media"><div class="post-media-emoji">🎨</div></div>
            <div class="post-actions-bar">
              <button class="pact" id="like-1" onclick="toggleLike('1')"><span class="pi">🤍</span> <span id="like-count-1">247</span></button>
              <button class="pact" onclick="toggleComments('post-1-comments')"><span class="pi">💬</span> 38</button>
              <button class="pact" onclick="openModal('share-modal')"><span class="pi">📤</span> Share</button>
              <button class="pact" onclick="showToast('🔖 Saved!','success')"><span class="pi">🔖</span> Save</button>
              <button class="pact" onclick="showToast('📊 Insights coming soon!','success')"><span class="pi">📊</span> Stats</button>
            </div>
            <div class="comments-box hidden" id="post-1-comments">
              <div class="comments-inner">
                <div class="comments-ttl">Comments (38)</div>
                <div class="cmt"><div class="cmt-av av-teal">S</div><div class="cmt-bubble"><div class="cmt-name">Sanya</div><div class="cmt-text">This is so well written! Bento grids are everywhere now 🙌</div></div></div>
                <div class="cmt"><div class="cmt-av av-orange">R</div><div class="cmt-bubble"><div class="cmt-name">Rahul</div><div class="cmt-text">Glassmorphism was sleeping for a while but now it's back stronger than ever!</div></div></div>
                <div class="cmt"><div class="cmt-av" style="background:linear-gradient(135deg,#a29bfe,#6c5ce7)">P</div><div class="cmt-bubble"><div class="cmt-name">Priya</div><div class="cmt-text">Great insights Aryan. Would love a deep-dive article on this!</div></div></div>
                <div class="cmt-input-row">
                  <input class="cmt-input" placeholder="Write a comment..." id="cmt-input-1">
                  <button class="cmt-send" onclick="addComment('1')">Send</button>
                </div>
              </div>
            </div>
          </div>

          <!-- Post 2 -->
          <div class="post-card" id="post-2">
            <div class="post-head">
              <div class="post-avatar av-pink">S</div>
              <div class="post-meta">
                <div class="post-author-name">Sanya Mehta</div>
                <div class="post-time-tag">5 hours ago · 🌍 Public</div>
              </div>
              <button class="post-more" onclick="showToast('⚙️ Post options','success')">⋯</button>
            </div>
            <div class="post-body">
              <div class="post-title">Solo Trip to Coorg — A Digital Nomad's Paradise 🌿</div>
              <div class="post-text">Packed my laptop and headed to the hills. Coorg in monsoon is absolutely magical — misty mornings, coffee estates, and WiFi that actually works. Here's everything you need to know if you're planning a workcation...</div>
              <div class="post-tags-row">
                <span class="ptag">#Travel</span><span class="ptag">#Coorg</span><span class="ptag">#DigitalNomad</span><span class="ptag">#WorkFromHills</span>
              </div>
            </div>
            <div class="post-media"><div class="post-media-emoji">🌿</div></div>
            <div class="post-actions-bar">
              <button class="pact" id="like-2" onclick="toggleLike('2')"><span class="pi">🤍</span> <span id="like-count-2">512</span></button>
              <button class="pact" onclick="toggleComments('post-2-comments')"><span class="pi">💬</span> 74</button>
              <button class="pact" onclick="openModal('share-modal')"><span class="pi">📤</span> Share</button>
              <button class="pact" onclick="showToast('🔖 Saved!','success')"><span class="pi">🔖</span> Save</button>
              <button class="pact" onclick="showToast('📊 Insights coming soon!','success')"><span class="pi">📊</span> Stats</button>
            </div>
            <div class="comments-box hidden" id="post-2-comments">
              <div class="comments-inner">
                <div class="comments-ttl">Comments (74)</div>
                <div class="cmt"><div class="cmt-av av-blue">K</div><div class="cmt-bubble"><div class="cmt-name">Karan</div><div class="cmt-text">Adding Coorg to my bucket list right now! 🌧️</div></div></div>
                <div class="cmt"><div class="cmt-av av-green">M</div><div class="cmt-bubble"><div class="cmt-name">Meera</div><div class="cmt-text">I went last year and it's even more beautiful than photos show!</div></div></div>
                <div class="cmt-input-row">
                  <input class="cmt-input" placeholder="Write a comment..." id="cmt-input-2">
                  <button class="cmt-send" onclick="addComment('2')">Send</button>
                </div>
              </div>
            </div>
          </div>

          <!-- Post 3 -->
          <div class="post-card" id="post-3">
            <div class="post-head">
              <div class="post-avatar av-teal">R</div>
              <div class="post-meta">
                <div class="post-author-name">Rahul Dev <span class="verified">✦</span></div>
                <div class="post-time-tag">Yesterday · 🌍 Public</div>
              </div>
              <button class="post-more" onclick="showToast('⚙️ Post options','success')">⋯</button>
            </div>
            <div class="post-body">
              <div class="post-title">Why Every Developer Should Learn System Design in 2025 💡</div>
              <div class="post-text">Coding skills will only take you so far. The engineers who rise to senior levels fast are the ones who can think in systems — distributed databases, load balancers, microservices. Here's a roadmap to get started...</div>
              <div class="post-tags-row">
                <span class="ptag">#Tech</span><span class="ptag">#SystemDesign</span><span class="ptag">#Engineering</span>
              </div>
            </div>
            <div class="post-media"><div class="post-media-emoji">💡</div></div>
            <div class="post-actions-bar">
              <button class="pact" id="like-3" onclick="toggleLike('3')"><span class="pi">🤍</span> <span id="like-count-3">891</span></button>
              <button class="pact" onclick="toggleComments('post-3-comments')"><span class="pi">💬</span> 112</button>
              <button class="pact" onclick="openModal('share-modal')"><span class="pi">📤</span> Share</button>
              <button class="pact" onclick="showToast('🔖 Saved!','success')"><span class="pi">🔖</span> Save</button>
              <button class="pact" onclick="showToast('📊 Insights coming soon!','success')"><span class="pi">📊</span> Stats</button>
            </div>
            <div class="comments-box hidden" id="post-3-comments">
              <div class="comments-inner">
                <div class="comments-ttl">Comments (112)</div>
                <div class="cmt"><div class="cmt-av av-purple">V</div><div class="cmt-bubble"><div class="cmt-name">Vedansh</div><div class="cmt-text">Amazing post Rahul! System design interviews are brutal without this knowledge 🔥</div></div></div>
                <div class="cmt"><div class="cmt-av av-orange">D</div><div class="cmt-bubble"><div class="cmt-name">Dev</div><div class="cmt-text">Bookmarked. This is exactly the roadmap I needed!</div></div></div>
                <div class="cmt-input-row">
                  <input class="cmt-input" placeholder="Write a comment..." id="cmt-input-3">
                  <button class="cmt-send" onclick="addComment('3')">Send</button>
                </div>
              </div>
            </div>
          </div>

          <!-- Post 4 — Vedansh's Post -->
          <div class="post-card" id="post-4">
            <div class="post-head">
              <div class="post-avatar av-purple">V</div>
              <div class="post-meta">
                <div class="post-author-name">Vedansh 👑 <span class="verified">✦</span></div>
                <div class="post-time-tag">2 days ago · 🌍 Public</div>
              </div>
              <button class="post-more" onclick="showToast('⚙️ Post options','success')">⋯</button>
            </div>
            <div class="post-body">
              <div class="post-title">Welcome to Orbix — The Platform Built for Creators 🚀</div>
              <div class="post-text">We're live! Orbix is finally here — your all-in-one space for posts, reels, articles, and everything in between. Share your world, grow your audience, and connect with creators who think like you. Let's build something amazing together.</div>
              <div class="post-tags-row">
                <span class="ptag">#Orbix</span><span class="ptag">#Launch</span><span class="ptag">#Creators</span><span class="ptag">#Welcome</span>
              </div>
            </div>
            <div class="post-media"><div class="post-media-emoji">🚀</div></div>
            <div class="post-actions-bar">
              <button class="pact liked" id="like-4" onclick="toggleLike('4')"><span class="pi">❤️</span> <span id="like-count-4">2.4k</span></button>
              <button class="pact" onclick="toggleComments('post-4-comments')"><span class="pi">💬</span> 334</button>
              <button class="pact" onclick="openModal('share-modal')"><span class="pi">📤</span> Share</button>
              <button class="pact" onclick="showToast('🔖 Saved!','success')"><span class="pi">🔖</span> Save</button>
              <button class="pact" onclick="showToast('📌 Pinned to top!','success')"><span class="pi">📌</span> Pin</button>
            </div>
            <div class="comments-box hidden" id="post-4-comments">
              <div class="comments-inner">
                <div class="comments-ttl">Comments (334)</div>
                <div class="cmt"><div class="cmt-av av-pink">S</div><div class="cmt-bubble"><div class="cmt-name">Sanya</div><div class="cmt-text">This platform is incredible! Love the design 🔥</div></div></div>
                <div class="cmt"><div class="cmt-av av-teal">R</div><div class="cmt-bubble"><div class="cmt-name">Rahul</div><div class="cmt-text">Finally something worth switching to. Welcome to the future!</div></div></div>
                <div class="cmt-input-row">
                  <input class="cmt-input" placeholder="Write a comment..." id="cmt-input-4">
                  <button class="cmt-send" onclick="addComment('4')">Send</button>
                </div>
              </div>
            </div>
          </div>

        </div><!-- end feed-col -->

        <!-- Feed Sidebar -->
        <div class="feed-sidebar">
          <div class="sw">
            <div class="sw-title">🔥 Trending</div>
            <div class="trend-item" onclick="showToast('🔍 Searching #OrbixLaunch','success')">
              <div class="trend-num">1</div>
              <div class="trend-info"><div class="trend-tag">#OrbixLaunch</div><div class="trend-cnt">24.2K posts</div></div>
            </div>
            <div class="trend-item" onclick="showToast('🔍 Searching #UITrends2025','success')">
              <div class="trend-num">2</div>
              <div class="trend-info"><div class="trend-tag">#UITrends2025</div><div class="trend-cnt">18.5K posts</div></div>
            </div>
            <div class="trend-item" onclick="showToast('🔍 Searching #TechIndia','success')">
              <div class="trend-num">3</div>
              <div class="trend-info"><div class="trend-tag">#TechIndia</div><div class="trend-cnt">12.1K posts</div></div>
            </div>
            <div class="trend-item" onclick="showToast('🔍 Searching #DigitalNomad','success')">
              <div class="trend-num">4</div>
              <div class="trend-info"><div class="trend-tag">#DigitalNomad</div><div class="trend-cnt">9.8K posts</div></div>
            </div>
            <div class="trend-item" onclick="showToast('🔍 Searching #Reels2025','success')">
              <div class="trend-num">5</div>
              <div class="trend-info"><div class="trend-tag">#Reels2025</div><div class="trend-cnt">7.3K posts</div></div>
            </div>
          </div>
          <div class="sw">
            <div class="sw-title">👥 Suggested</div>
            <div class="sug-user">
              <div class="sug-av av-blue">K</div>
              <div class="sug-info"><div class="sug-name">Karan Sharma</div><div class="sug-handle">@karansharma · Dev</div></div>
              <button class="follow-btn" onclick="toggleFollow(this)">Follow</button>
            </div>
            <div class="sug-user">
              <div class="sug-av av-green">M</div>
              <div class="sug-info"><div class="sug-name">Meera Iyer</div><div class="sug-handle">@meeraiyer · Art</div></div>
              <button class="follow-btn" onclick="toggleFollow(this)">Follow</button>
            </div>
            <div class="sug-user">
              <div class="sug-av av-orange">D</div>
              <div class="sug-info"><div class="sug-name">Dev Patel</div><div class="sug-handle">@devpatel · Music</div></div>
              <button class="follow-btn" onclick="toggleFollow(this)">Follow</button>
            </div>
            <div class="sug-user">
              <div class="sug-av" style="background:linear-gradient(135deg,#a29bfe,#6c5ce7)">N</div>
              <div class="sug-info"><div class="sug-name">Nisha Roy</div><div class="sug-handle">@nisharoy · Travel</div></div>
              <button class="follow-btn" onclick="toggleFollow(this)">Follow</button>
            </div>
          </div>
          <div class="sw">
            <div class="sw-title">📡 Live Now</div>
            <div style="display:flex;flex-direction:column;gap:10px;">
              <div style="display:flex;align-items:center;gap:10px;cursor:pointer;" onclick="showToast('📡 Joining live stream...','success')">
                <div style="width:40px;height:40px;border-radius:10px;background:var(--bg2);display:flex;align-items:center;justify-content:center;font-size:1.3rem;">🎙️</div>
                <div style="flex:1;"><div style="font-size:0.87rem;font-weight:600;">Tech Talk with Rahul</div><div style="font-size:0.76rem;color:var(--text3);">1.2K watching</div></div>
                <div style="font-size:0.72rem;padding:3px 8px;border-radius:100px;background:#ff4d6d;color:#fff;font-weight:700;">LIVE</div>
              </div>
              <div style="display:flex;align-items:center;gap:10px;cursor:pointer;" onclick="showToast('📡 Joining live stream...','success')">
                <div style="width:40px;height:40px;border-radius:10px;background:var(--bg2);display:flex;align-items:center;justify-content:center;font-size:1.3rem;">🎨</div>
                <div style="flex:1;"><div style="font-size:0.87rem;font-weight:600;">Art Session by Meera</div><div style="font-size:0.76rem;color:var(--text3);">489 watching</div></div>
                <div style="font-size:0.72px;padding:3px 8px;border-radius:100px;background:#ff4d6d;color:#fff;font-weight:700;font-size:0.72rem;">LIVE</div>
              </div>
            </div>
          </div>
        </div><!-- end sidebar -->
      </div>
    </div>

    <!-- ============================================================
         PAGE 2 — REELS
    ============================================================ -->
    <div class="page" id="page-reels">
      <div class="page-header">
        <h1>🎬 Reels</h1>
        <p>Short, snappy videos — scroll to discover</p>
      </div>
      <div class="reels-page-layout">
        <div class="reels-main">
          <div class="reels-feed" id="reels-feed">

            <!-- Reel 1 -->
            <div class="reel" style="background:linear-gradient(160deg,#1a0040,#2d0060,#000820);">
              <div class="reel-bg-emoji">🎭</div>
              <div class="reel-gradient"></div>
              <div class="reel-info-area">
                <div class="reel-author-row">
                  <div class="reel-av">A</div>
                  <div class="reel-author-name">Aryan Kapoor</div>
                  <button class="reel-follow-pill" onclick="showToast('✅ Following Aryan!','success')">+ Follow</button>
                </div>
                <div class="reel-title">5 UI Animations That Will Blow Your Mind 🤯</div>
                <div class="reel-desc">These micro-interactions changed how I think about UX. Watch till the end — #5 is insane!</div>
                <div class="reel-hashtags">
                  <span class="reel-hash">#UI</span><span class="reel-hash">#Animation</span><span class="reel-hash">#Design</span><span class="reel-hash">#UX</span>
                </div>
                <div class="reel-music"><span class="music-icon">🎵</span> Neon Dreams — Synthwave Mix</div>
              </div>
              <div class="reel-side-actions">
                <div class="reel-act"><button class="reel-act-btn" id="rl-1" onclick="toggleReelLike('1')">🤍</button><div class="reel-act-cnt" id="rl-cnt-1">4.2K</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="toggleComments('reel-1-comments');showToast('💬 Comments','success')">💬</button><div class="reel-act-cnt">238</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="openModal('share-modal')">📤</button><div class="reel-act-cnt">Share</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('🔖 Saved reel!','success')">🔖</button><div class="reel-act-cnt">Save</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('⚙️ Options','success')">⋯</button><div class="reel-act-cnt">More</div></div>
              </div>
            </div>

            <!-- Reel 2 -->
            <div class="reel" style="background:linear-gradient(160deg,#003320,#001a10,#002030);">
              <div class="reel-bg-emoji">🌿</div>
              <div class="reel-gradient"></div>
              <div class="reel-info-area">
                <div class="reel-author-row">
                  <div class="reel-av" style="background:linear-gradient(135deg,#fc5c9c,#ff8fb1)">S</div>
                  <div class="reel-author-name">Sanya Mehta</div>
                  <button class="reel-follow-pill" onclick="showToast('✅ Following Sanya!','success')">+ Follow</button>
                </div>
                <div class="reel-title">Hidden Cafes in Bangalore You MUST Visit ☕</div>
                <div class="reel-desc">Found 7 hidden gems in Indiranagar and Koramangala. Aesthetic, affordable, and the coffee is 🔥</div>
                <div class="reel-hashtags">
                  <span class="reel-hash">#Bangalore</span><span class="reel-hash">#Cafe</span><span class="reel-hash">#Travel</span><span class="reel-hash">#Food</span>
                </div>
                <div class="reel-music"><span class="music-icon">🎵</span> Lo-fi Beats for Study</div>
              </div>
              <div class="reel-side-actions">
                <div class="reel-act"><button class="reel-act-btn" id="rl-2" onclick="toggleReelLike('2')">🤍</button><div class="reel-act-cnt" id="rl-cnt-2">7.8K</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('💬 Comments','success')">💬</button><div class="reel-act-cnt">512</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="openModal('share-modal')">📤</button><div class="reel-act-cnt">Share</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('🔖 Saved reel!','success')">🔖</button><div class="reel-act-cnt">Save</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('⚙️ Options','success')">⋯</button><div class="reel-act-cnt">More</div></div>
              </div>
            </div>

            <!-- Reel 3 -->
            <div class="reel" style="background:linear-gradient(160deg,#002040,#001030,#100030);">
              <div class="reel-bg-emoji">💻</div>
              <div class="reel-gradient"></div>
              <div class="reel-info-area">
                <div class="reel-author-row">
                  <div class="reel-av" style="background:linear-gradient(135deg,#5cf0d8,#00b8a0)">R</div>
                  <div class="reel-author-name">Rahul Dev</div>
                  <button class="reel-follow-pill" onclick="showToast('✅ Following Rahul!','success')">+ Follow</button>
                </div>
                <div class="reel-title">Code a Full App in 60 Seconds ⚡</div>
                <div class="reel-desc">Using AI + VS Code extensions to build a complete React app faster than ordering pizza. No cap.</div>
                <div class="reel-hashtags">
                  <span class="reel-hash">#Coding</span><span class="reel-hash">#React</span><span class="reel-hash">#AI</span><span class="reel-hash">#DevLife</span>
                </div>
                <div class="reel-music"><span class="music-icon">🎵</span> Cyberpunk 2077 OST</div>
              </div>
              <div class="reel-side-actions">
                <div class="reel-act"><button class="reel-act-btn" id="rl-3" onclick="toggleReelLike('3')">🤍</button><div class="reel-act-cnt" id="rl-cnt-3">12.1K</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('💬 Comments','success')">💬</button><div class="reel-act-cnt">891</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="openModal('share-modal')">📤</button><div class="reel-act-cnt">Share</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('🔖 Saved reel!','success')">🔖</button><div class="reel-act-cnt">Save</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('⚙️ Options','success')">⋯</button><div class="reel-act-cnt">More</div></div>
              </div>
            </div>

            <!-- Reel 4 -->
            <div class="reel" style="background:linear-gradient(160deg,#301000,#200800,#100010);">
              <div class="reel-bg-emoji">🎵</div>
              <div class="reel-gradient"></div>
              <div class="reel-info-area">
                <div class="reel-author-row">
                  <div class="reel-av" style="background:linear-gradient(135deg,#fdcb6e,#e17055)">D</div>
                  <div class="reel-author-name">Dev Patel</div>
                  <button class="reel-follow-pill" onclick="showToast('✅ Following Dev!','success')">+ Follow</button>
                </div>
                <div class="reel-title">Making a Beat From Scratch in 30 Mins 🎹</div>
                <div class="reel-desc">Started with just a kick and a pad. This is the entire production process — raw and unfiltered.</div>
                <div class="reel-hashtags">
                  <span class="reel-hash">#Music</span><span class="reel-hash">#Producer</span><span class="reel-hash">#BeatMaking</span>
                </div>
                <div class="reel-music"><span class="music-icon">🎵</span> Original Score by DevPatel</div>
              </div>
              <div class="reel-side-actions">
                <div class="reel-act"><button class="reel-act-btn" id="rl-4" onclick="toggleReelLike('4')">🤍</button><div class="reel-act-cnt" id="rl-cnt-4">9.3K</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('💬 Comments','success')">💬</button><div class="reel-act-cnt">634</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="openModal('share-modal')">📤</button><div class="reel-act-cnt">Share</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('🔖 Saved reel!','success')">🔖</button><div class="reel-act-cnt">Save</div></div>
                <div class="reel-act"><button class="reel-act-btn" onclick="showToast('⚙️ Options','success')">⋯</button><div class="reel-act-cnt">More</div></div>
              </div>
            </div>

          </div><!-- end reels-feed -->
        </div><!-- end reels-main -->

        <div class="reels-info-panel">
          <div class="reels-panel-card">
            <div class="reels-panel-title">🎯 Up Next</div>
            <div class="up-next-item" onclick="showToast('▶️ Playing next reel','success')">
              <div class="up-next-thumb">🌸</div>
              <div class="up-next-info"><div class="up-next-name">Spring Festival Vlog</div><div class="up-next-meta">Meera · 45K views</div></div>
            </div>
            <div class="up-next-item" onclick="showToast('▶️ Playing next reel','success')">
              <div class="up-next-thumb">🏋️</div>
              <div class="up-next-info"><div class="up-next-name">5AM Gym Routine</div><div class="up-next-meta">Karan · 22K views</div></div>
            </div>
            <div class="up-next-item" onclick="showToast('▶️ Playing next reel','success')">
              <div class="up-next-thumb">🍜</div>
              <div class="up-next-info"><div class="up-next-name">Midnight Ramen Recipe</div><div class="up-next-meta">Priya · 67K views</div></div>
            </div>
            <div class="up-next-item" onclick="showToast('▶️ Playing next reel','success')">
              <div class="up-next-thumb">🎨</div>
              <div class="up-next-info"><div class="up-next-name">Procreate Speed Art</div><div class="up-next-meta">Nisha · 38K views</div></div>
            </div>
          </div>
          <div class="reels-panel-card">
            <div class="reels-panel-title">📊 Today's Stats</div>
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;">
              <div style="background:var(--bg2);border-radius:12px;padding:12px;text-align:center;">
                <div style="font-family:'Syne',sans-serif;font-size:1.4rem;font-weight:900;color:var(--accent);">48K</div>
                <div style="font-size:0.74rem;color:var(--text3);">Reel Views</div>
              </div>
              <div style="background:var(--bg2);border-radius:12px;padding:12px;text-align:center;">
                <div style="font-family:'Syne',sans-serif;font-size:1.4rem;font-weight:900;color:var(--accent2);">2.3K</div>
                <div style="font-size:0.74rem;color:var(--text3);">New Likes</div>
              </div>
              <div style="background:var(--bg2);border-radius:12px;padding:12px;text-align:center;">
                <div style="font-family:'Syne',sans-serif;font-size:1.4rem;font-weight:900;color:var(--accent3);">187</div>
                <div style="font-size:0.74rem;color:var(--text3);">New Follows</div>
              </div>
              <div style="background:var(--bg2);border-radius:12px;padding:12px;text-align:center;">
                <div style="font-family:'Syne',sans-serif;font-size:1.4rem;font-weight:900;color:#fdcb6e;">94%</div>
                <div style="font-size:0.74rem;color:var(--text3);">Watch Rate</div>
              </div>
            </div>
          </div>
          <div class="reels-panel-card">
            <div class="reels-panel-title">🎬 Categories</div>
            <div style="display:flex;flex-wrap:wrap;gap:6px;">
              <button class="fpill active" onclick="filterReels(this,'all')">All</button>
              <button class="fpill" onclick="filterReels(this,'tech')">💻 Tech</button>
              <button class="fpill" onclick="filterReels(this,'travel')">🌍 Travel</button>
              <button class="fpill" onclick="filterReels(this,'food')">🍜 Food</button>
              <button class="fpill" onclick="filterReels(this,'music')">🎵 Music</button>
              <button class="fpill" onclick="filterReels(this,'art')">🎨 Art</button>
              <button class="fpill" onclick="filterReels(this,'fitness')">🏋️ Fitness</button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ============================================================
         PAGE 3 — ARTICLES
    ============================================================ -->
    <div class="page" id="page-articles">
      <div class="art-toolbar">
        <h1>📝 Articles</h1>
        <div class="filter-pills">
          <button class="fpill active" onclick="filterArticles(this,'all')">All</button>
          <button class="fpill" onclick="filterArticles(this,'tech')">💻 Tech</button>
          <button class="fpill" onclick="filterArticles(this,'travel')">🌍 Travel</button>
          <button class="fpill" onclick="filterArticles(this,'design')">🎨 Design</button>
          <button class="fpill" onclick="filterArticles(this,'lifestyle')">✨ Lifestyle</button>
          <button class="fpill" onclick="filterArticles(this,'finance')">💰 Finance</button>
          <button class="fpill" onclick="filterArticles(this,'health')">🏃 Health</button>
        </div>
        <button class="btn btn-primary btn-sm" onclick="navTo('upload')">✚ Write Article</button>
      </div>
      <div class="art-grid">
        <!-- Featured -->
        <div class="art-featured" onclick="showToast('📖 Opening article...','success')">
          <div class="art-featured-cover ac-purple">
            <div class="art-cover-overlay" style="background:linear-gradient(135deg,#2a1060,#401080);opacity:0.9;"></div>
            <div class="art-cover-inner">🤖</div>
          </div>
          <div class="art-featured-body">
            <div class="art-cat-pill">✦ Featured</div>
            <div class="art-title">The Complete 2025 Guide to Building AI-Powered Products Without Writing a Single Line of Code</div>
            <div class="art-excerpt">No-code AI tools have matured dramatically. From Zapier AI to Claude integrations, here's how founders are shipping in days, not months...</div>
            <div class="art-footer">
              <div class="art-author"><div class="art-av av-purple">V</div><div class="art-author-name">Vedansh</div></div>
              <div class="art-stats"><div class="art-stat">❤️ 1.2K</div><div class="art-stat">💬 89</div><div class="art-stat">👁️ 18K</div></div>
            </div>
          </div>
        </div>
        <!-- Cards -->
        <div class="art-card" onclick="showToast('📖 Opening article...','success')">
          <div class="art-cover ac-blue"><div class="art-cover-overlay"></div><div class="art-cover-inner">💡</div><div class="art-cat-pill">Tech</div></div>
          <div class="art-body"><div class="art-title">System Design for Beginners: A Visual Guide</div><div class="art-excerpt">Learn distributed systems through diagrams, not theory. Perfect for interview prep and real-world engineering.</div><div class="art-footer"><div class="art-author"><div class="art-av av-teal">R</div><div class="art-author-name">Rahul Dev</div></div><div class="art-stats"><div class="art-stat">❤️ 891</div><div class="art-stat">👁️ 12K</div></div></div></div>
        </div>
        <div class="art-card" onclick="showToast('📖 Opening article...','success')">
          <div class="art-cover ac-pink"><div class="art-cover-overlay"></div><div class="art-cover-inner">🌏</div><div class="art-cat-pill art-cat-pink">Travel</div></div>
          <div class="art-body"><div class="art-title">Southeast Asia on ₹500/Day: The Real Guide</div><div class="art-excerpt">Skip the tourist traps. Here's how to backpack Vietnam, Thailand, and Cambodia on a real budget without compromising experiences.</div><div class="art-footer"><div class="art-author"><div class="art-av av-pink">S</div><div class="art-author-name">Sanya Mehta</div></div><div class="art-stats"><div class="art-stat">❤️ 643</div><div class="art-stat">👁️ 9.8K</div></div></div></div>
        </div>
        <div class="art-card" onclick="showToast('📖 Opening article...','success')">
          <div class="art-cover ac-teal"><div class="art-cover-overlay"></div><div class="art-cover-inner">🎨</div><div class="art-cat-pill art-cat-teal">Design</div></div>
          <div class="art-body"><div class="art-title">Figma Variables Are Changing Everything — Here's Why</div><div class="art-excerpt">Figma Variables finally bring true design system power to the platform. Here's a practical guide to setting up tokens that scale.</div><div class="art-footer"><div class="art-author"><div class="art-av av-purple">A</div><div class="art-author-name">Aryan Kapoor</div></div><div class="art-stats"><div class="art-stat">❤️ 421</div><div class="art-stat">👁️ 6.2K</div></div></div></div>
        </div>
        <div class="art-card" onclick="showToast('📖 Opening article...','success')">
          <div class="art-cover ac-orange"><div class="art-cover-overlay"></div><div class="art-cover-inner">💰</div><div class="art-cat-pill">Finance</div></div>
          <div class="art-body"><div class="art-title">How I Built a ₹10L Emergency Fund in 18 Months on a Fresher Salary</div><div class="art-excerpt">Step-by-step financial planning that actually works for Indian millennials. No stock tips, just boring math that builds wealth.</div><div class="art-footer"><div class="art-author"><div class="art-av av-blue">K</div><div class="art-author-name">Karan Sharma</div></div><div class="art-stats"><div class="art-stat">❤️ 1.1K</div><div class="art-stat">👁️ 15K</div></div></div></div>
        </div>
        <div class="art-card" onclick="showToast('📖 Opening article...','success')">
          <div class="art-cover ac-purple"><div class="art-cover-overlay"></div><div class="art-cover-inner">🏃</div><div class="art-cat-pill">Health</div></div>
          <div class="art-body"><div class="art-title">The 20-Minute Morning Routine That Changed My Life</div><div class="art-excerpt">Journaling, sunlight, and intentional movement — here's the scientific breakdown of why this simple routine works so well.</div><div class="art-footer"><div class="art-author"><div class="art-av av-green">M</div><div class="art-author-name">Meera Iyer</div></div><div class="art-stats"><div class="art-stat">❤️ 788</div><div class="art-stat">👁️ 11K</div></div></div></div>
        </div>
      </div>
    </div>

    <!-- ============================================================
         PAGE 4 — UPLOAD
    ============================================================ -->
    <div class="page" id="page-upload">
      <div class="page-header">
        <h1>✚ Create & Upload</h1>
        <p>Share your posts, reels, photos, videos and articles with the Orbix community</p>
      </div>
      <div class="upload-layout">
        <div class="upload-form-card">
          <h2>New Post</h2>
          <p class="sub">Fill in the details and drag & drop or browse to upload your media</p>
          
          <div class="type-tabs">
            <button class="type-tab active" onclick="selectType(this,'post')"><div class="type-tab-icon">📝</div><div class="type-tab-label">Post</div></button>
            <button class="type-tab" onclick="selectType(this,'reel')"><div class="type-tab-icon">🎬</div><div class="type-tab-label">Reel</div></button>
            <button class="type-tab" onclick="selectType(this,'article')"><div class="type-tab-icon">📰</div><div class="type-tab-label">Article</div></button>
            <button class="type-tab" onclick="selectType(this,'photo')"><div class="type-tab-icon">📸</div><div class="type-tab-label">Photo</div></button>
            <button class="type-tab" onclick="selectType(this,'video')"><div class="type-tab-icon">📹</div><div class="type-tab-label">Video</div></button>
          </div>

          <div class="form-group">
            <label class="form-label">Title *</label>
            <input class="form-input" id="upload-title" placeholder="Give your post a compelling title..." maxlength="120" oninput="updateChar('upload-title','title-char',120)">
            <div class="char-count" id="title-char">0 / 120</div>
          </div>
          <div class="form-group">
            <label class="form-label">Description / Content *</label>
            <textarea class="form-textarea" id="upload-desc" placeholder="Tell your story, share your thoughts..." maxlength="2000" oninput="updateChar('upload-desc','desc-char',2000)"></textarea>
            <div class="char-count" id="desc-char">0 / 2000</div>
          </div>
          <div class="form-group">
            <label class="form-label">Category</label>
            <select class="form-select" id="upload-cat">
              <option value="">Select a category...</option>
              <option>🎨 Design & Art</option>
              <option>💻 Tech & Coding</option>
              <option>🌍 Travel</option>
              <option>🍜 Food & Recipes</option>
              <option>🎵 Music</option>
              <option>🏋️ Fitness & Health</option>
              <option>💰 Finance</option>
              <option>📸 Photography</option>
              <option>✨ Lifestyle</option>
              <option>🎬 Entertainment</option>
            </select>
          </div>
          <div class="form-group">
            <label class="form-label">Tags</label>
            <div class="tags-input-wrap">
              <input class="form-input" id="tag-input" placeholder="Add a tag and press Enter" onkeydown="addTag(event)">
              <button class="btn btn-primary btn-sm" onclick="addTagBtn()">Add</button>
            </div>
            <div class="tags-display" id="tags-display"></div>
          </div>
          <div class="form-group">
            <label class="form-label">Visibility</label>
            <select class="form-select" id="upload-vis">
              <option>🌍 Public — Everyone can see</option>
              <option>👥 Followers — Only followers</option>
              <option>🔒 Private — Only me</option>
            </select>
          </div>

          <!-- Drop Zone -->
          <div class="form-group">
            <label class="form-label">Media Upload (Drag & Drop)</label>
            <div class="drop-zone" id="drop-zone" ondragover="onDragOver(event)" ondragleave="onDragLeave(event)" ondrop="onDrop(event)" onclick="document.getElementById('file-input').click()">
              <div class="drop-icon">☁️</div>
              <div class="drop-main">Drag & drop your files here</div>
              <div class="drop-hint">or click to browse · Images, Videos, GIFs up to 500MB</div>
            </div>
            <input type="file" id="file-input" accept="image/*,video/*,.gif" onchange="onFileSelect(event)">
            <div class="file-preview-bar" id="file-preview">
              <div class="file-preview-icon" id="fp-icon">📄</div>
              <div class="file-preview-info">
                <div class="file-preview-name" id="fp-name">filename.jpg</div>
                <div class="file-preview-size" id="fp-size">2.4 MB</div>
              </div>
              <button class="file-rm" onclick="removeFile()">✕</button>
            </div>
          </div>

          <button class="submit-btn" onclick="submitPost()">🚀 Publish to Orbix</button>
        </div>

        <div class="upload-sidebar">
          <div class="sw">
            <div class="sw-title">📋 Guidelines</div>
            <div class="tip-item"><span class="tip-icon">✅</span> Be authentic and original in your content</div>
            <div class="tip-item"><span class="tip-icon">✅</span> Use high quality images (min 720px)</div>
            <div class="tip-item"><span class="tip-icon">✅</span> Add relevant tags to reach more people</div>
            <div class="tip-item"><span class="tip-icon">✅</span> Engaging titles get 3x more clicks</div>
            <div class="tip-item"><span class="tip-icon">🚫</span> No spam, hate speech or misinformation</div>
            <div class="tip-item"><span class="tip-icon">🚫</span> No copyright infringing material</div>
            <div class="tip-item"><span class="tip-icon">🚫</span> No explicit or adult content</div>
          </div>
          <div class="sw">
            <div class="sw-title">📊 Your Stats</div>
            <div class="upl-stats-grid">
              <div class="upl-stat-box"><div class="upl-stat-num" id="stat-posts">12</div><div class="upl-stat-lbl">Posts</div></div>
              <div class="upl-stat-box"><div class="upl-stat-num">3.2K</div><div class="upl-stat-lbl">Total Views</div></div>
              <div class="upl-stat-box"><div class="upl-stat-num">841</div><div class="upl-stat-lbl">Total Likes</div></div>
              <div class="upl-stat-box"><div class="upl-stat-num">94%</div><div class="upl-stat-lbl">Avg Quality</div></div>
            </div>
          </div>
          <div class="sw">
            <div class="sw-title">⚡ Quick Tips</div>
            <div style="font-size:0.85rem;color:var(--text2);line-height:1.7;">
              Posts with <strong style="color:var(--accent);">3–5 tags</strong> get 60% more reach.<br><br>
              The best time to post is <strong style="color:var(--accent2);">6–9 PM IST</strong> on weekdays.<br><br>
              Reels under <strong style="color:var(--accent3);">30 seconds</strong> have the highest completion rate.
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ============================================================
         PAGE 5 — EXPLORE
    ============================================================ -->
    <div class="page" id="page-explore">
      <div class="explore-hero">
        <div class="explore-hero-pattern"></div>
        <h2>Explore Orbix 🔭</h2>
        <p>Discover trending content, creators, and stories from around the world</p>
        <div class="explore-search-big">
          <span class="si">🔍</span>
          <input placeholder="Search posts, reels, articles, creators..." oninput="handleSearch(this.value)">
          <button class="explore-search-btn" onclick="showToast('🔍 Searching...','success')">Search</button>
        </div>
      </div>
      <div class="explore-cats">
        <button class="explore-cat-btn active" onclick="setExploreCat(this)">✦ For You</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">🔥 Trending</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">💻 Technology</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">🎨 Design</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">🌍 Travel</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">🍜 Food</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">🎵 Music</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">🏋️ Fitness</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">✨ Lifestyle</button>
        <button class="explore-cat-btn" onclick="setExploreCat(this)">📸 Photography</button>
      </div>
      <div class="masonry">
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:160px;background:linear-gradient(135deg,#1a0040,#2d0060);">🎭</div>
          <div class="masonry-body"><div class="masonry-title">The Art of Dark UI Design</div><div class="masonry-meta">Aryan · 4.2K likes</div><div class="masonry-tags"><span class="masonry-tag">#Design</span><span class="masonry-tag">#Dark</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:220px;background:linear-gradient(135deg,#003320,#002040);">🌿</div>
          <div class="masonry-body"><div class="masonry-title">Monsoon Hikes in Western Ghats</div><div class="masonry-meta">Sanya · 7.8K likes</div><div class="masonry-tags"><span class="masonry-tag">#Travel</span><span class="masonry-tag">#Nature</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:140px;background:linear-gradient(135deg,#002040,#001030);">💻</div>
          <div class="masonry-body"><div class="masonry-title">React 19 — What's New</div><div class="masonry-meta">Rahul · 12.1K likes</div><div class="masonry-tags"><span class="masonry-tag">#React</span><span class="masonry-tag">#Dev</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:190px;background:linear-gradient(135deg,#301000,#200800);">🎵</div>
          <div class="masonry-body"><div class="masonry-title">Lo-fi Playlist for Deep Work 🎧</div><div class="masonry-meta">Dev · 9.3K likes</div><div class="masonry-tags"><span class="masonry-tag">#Music</span><span class="masonry-tag">#Lofi</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:170px;background:linear-gradient(135deg,#200040,#300060);">🌸</div>
          <div class="masonry-body"><div class="masonry-title">Watercolor Digital Art Process</div><div class="masonry-meta">Meera · 6.7K likes</div><div class="masonry-tags"><span class="masonry-tag">#Art</span><span class="masonry-tag">#Digital</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:130px;background:linear-gradient(135deg,#002030,#003040);">🏋️</div>
          <div class="masonry-body"><div class="masonry-title">HIIT Workout for Busy Days</div><div class="masonry-meta">Karan · 3.2K likes</div><div class="masonry-tags"><span class="masonry-tag">#Fitness</span><span class="masonry-tag">#Health</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:200px;background:linear-gradient(135deg,#301520,#200010);">🍜</div>
          <div class="masonry-body"><div class="masonry-title">Authentic Thai Green Curry from Scratch</div><div class="masonry-meta">Priya · 5.4K likes</div><div class="masonry-tags"><span class="masonry-tag">#Food</span><span class="masonry-tag">#Recipe</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:155px;background:linear-gradient(135deg,#101040,#202070);">🚀</div>
          <div class="masonry-body"><div class="masonry-title">Orbix Launch — Behind the Scenes</div><div class="masonry-meta">Vedansh · 24K likes</div><div class="masonry-tags"><span class="masonry-tag">#Orbix</span><span class="masonry-tag">#BTS</span></div></div>
        </div>
        <div class="masonry-item" onclick="showToast('📖 Opening post...','success')">
          <div class="masonry-media" style="height:180px;background:linear-gradient(135deg,#003030,#002020);">📸</div>
          <div class="masonry-body"><div class="masonry-title">Golden Hour Photography Guide</div><div class="masonry-meta">Nisha · 8.9K likes</div><div class="masonry-tags"><span class="masonry-tag">#Photography</span><span class="masonry-tag">#Golden</span></div></div>
        </div>
      </div>
    </div>

    <!-- ============================================================
         PAGE 6 — PROFILE
    ============================================================ -->
    <div class="page" id="page-profile">
      <div class="profile-cover-img">
        <div class="profile-cover-pattern"></div>
      </div>
      <div class="profile-info-bar">
        <div class="profile-big-av" id="profile-avatar">V</div>
        <div class="profile-details">
          <div class="profile-name-row" id="profile-name-display">Vedansh <span class="crown">👑</span></div>
          <div class="profile-handle" id="profile-handle">@vedansh · Admin</div>
          <div class="profile-bio-text">Creator, builder, dreamer. Admin of Orbix 🚀 | Sharing my journey in tech, design & life.</div>
        </div>
        <div class="profile-action-btns">
          <button class="pab pab-primary" onclick="navTo('upload')">✚ New Post</button>
          <button class="pab pab-secondary" onclick="showToast('⚙️ Edit profile coming soon!','success')">⚙️ Edit Profile</button>
          <button class="pab pab-secondary" onclick="openModal('share-modal')">📤 Share</button>
        </div>
      </div>
      <div class="profile-stats-bar">
        <div class="psb"><div class="psb-num">12</div><div class="psb-lbl">Posts</div></div>
        <div class="psb"><div class="psb-num">3.4K</div><div class="psb-lbl">Followers</div></div>
        <div class="psb"><div class="psb-num">289</div><div class="psb-lbl">Following</div></div>
        <div class="psb"><div class="psb-num">48.2K</div><div class="psb-lbl">Total Views</div></div>
        <div class="psb"><div class="psb-num">2.4K</div><div class="psb-lbl">Likes Received</div></div>
      </div>
      <div class="profile-tabs-bar">
        <button class="ptab active" onclick="profileTab(this,'media')">📸 Media</button>
        <button class="ptab" onclick="profileTab(this,'posts')">📝 Posts</button>
        <button class="ptab" onclick="profileTab(this,'reels')">🎬 Reels</button>
        <button class="ptab" onclick="profileTab(this,'articles')">📰 Articles</button>
        <button class="ptab" onclick="profileTab(this,'saved')">🔖 Saved</button>
        <button class="ptab" onclick="profileTab(this,'about')">ℹ️ About</button>
      </div>
      <div id="profile-tab-media">
        <div class="media-grid">
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>🎭</span><div class="media-thumb-overlay">4.2K ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>🚀</span><div class="media-thumb-overlay">2.4K ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>💡</span><div class="media-thumb-overlay">891 ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>🌿</span><div class="media-thumb-overlay">643 ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>🎨</span><div class="media-thumb-overlay">421 ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>💻</span><div class="media-thumb-overlay">788 ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>📸</span><div class="media-thumb-overlay">334 ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>🎵</span><div class="media-thumb-overlay">512 ❤️</div></div>
          <div class="media-thumb" onclick="showToast('📸 Opening media','success')"><span>🌙</span><div class="media-thumb-overlay">267 ❤️</div></div>
        </div>
      </div>
      <div id="profile-tab-posts" class="hidden">
        <div style="display:flex;flex-direction:column;gap:16px;max-width:600px;">
          <div class="post-card"><div class="post-head"><div class="post-avatar av-purple">V</div><div class="post-meta"><div class="post-author-name">Vedansh 👑</div><div class="post-time-tag">2 days ago</div></div></div><div class="post-body"><div class="post-title">Welcome to Orbix 🚀</div><div class="post-text">We're live! Orbix is finally here...</div></div><div class="post-actions-bar"><button class="pact liked"><span class="pi">❤️</span> 2.4K</button><button class="pact"><span class="pi">💬</span> 334</button><button class="pact" onclick="openModal('share-modal')"><span class="pi">📤</span> Share</button><button class="pact"><span class="pi">🔖</span> Save</button></div></div>
        </div>
      </div>
      <div id="profile-tab-reels" class="hidden"><div style="padding:24px;text-align:center;color:var(--text3);">🎬 No reels yet. <button class="btn btn-primary btn-sm" onclick="navTo('upload')" style="margin-left:10px;">Create Reel</button></div></div>
      <div id="profile-tab-articles" class="hidden"><div style="padding:24px;text-align:center;color:var(--text3);">📝 No articles yet. <button class="btn btn-primary btn-sm" onclick="navTo('upload')" style="margin-left:10px;">Write Article</button></div></div>
      <div id="profile-tab-saved" class="hidden"><div style="padding:24px;text-align:center;color:var(--text3);">🔖 No saved posts yet. Go explore!</div></div>
      <div id="profile-tab-about" class="hidden">
        <div class="profile-about-grid">
          <div class="about-card"><h4>Info</h4>
            <div class="about-item"><span class="about-item-icon">👤</span> Vedansh — Admin & Founder</div>
            <div class="about-item"><span class="about-item-icon">📍</span> India 🇮🇳</div>
            <div class="about-item"><span class="about-item-icon">🔗</span> orbix.app/vedansh</div>
            <div class="about-item"><span class="about-item-icon">📅</span> Joined May 2025</div>
            <div class="about-item"><span class="about-item-icon">✉️</span> vedansh@orbix.app</div>
          </div>
          <div class="about-card"><h4>Interests</h4>
            <div class="about-item"><span class="about-item-icon">💻</span> Technology & AI</div>
            <div class="about-item"><span class="about-item-icon">🎨</span> UI/UX Design</div>
            <div class="about-item"><span class="about-item-icon">🚀</span> Startups & Building</div>
            <div class="about-item"><span class="about-item-icon">📸</span> Photography</div>
            <div class="about-item"><span class="about-item-icon">🌍</span> Travel</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ============================================================
         PAGE 7 — ADMIN (Vedansh only)
    ============================================================ -->
    <div class="page" id="page-admin">
      <div class="admin-head">
        <h1>Admin Panel</h1>
        <div class="admin-pill">👑 Vedansh</div>
      </div>
      <div class="admin-kpi-grid">
        <div class="kpi-card kpi-purple"><div class="kpi-icon">👥</div><div class="kpi-num">1,284</div><div class="kpi-lbl">Total Users</div><div class="kpi-change">↑ +124 this week</div></div>
        <div class="kpi-card kpi-pink"><div class="kpi-icon">📝</div><div class="kpi-num">8,492</div><div class="kpi-lbl">Total Posts</div><div class="kpi-change">↑ +892 this week</div></div>
        <div class="kpi-card kpi-teal"><div class="kpi-icon">👁️</div><div class="kpi-num">284K</div><div class="kpi-lbl">Total Views</div><div class="kpi-change">↑ +12% this week</div></div>
        <div class="kpi-card kpi-orange"><div class="kpi-icon">🚩</div><div class="kpi-num">7</div><div class="kpi-lbl">Pending Reports</div><div class="kpi-change" style="color:#fdcb6e;">⚠ Needs review</div></div>
      </div>
      <div class="admin-panels">
        <div class="admin-panel">
          <div class="ap-title">👥 User Management</div>
          <table class="admin-tbl">
            <tr><th>User</th><th>Status</th><th>Posts</th><th>Actions</th></tr>
            <tr><td><div class="user-cell"><div class="user-cell-av" style="background:linear-gradient(135deg,#fc5c9c,#ff8fb1)">S</div>Sanya Mehta</div></td><td><span class="sbadge active">Active</span></td><td>34</td><td><button class="tbl-btn">View</button><button class="tbl-btn danger">Ban</button></td></tr>
            <tr><td><div class="user-cell"><div class="user-cell-av" style="background:linear-gradient(135deg,#5cf0d8,#00b8a0)">R</div>Rahul Dev</div></td><td><span class="sbadge active">Active</span></td><td>67</td><td><button class="tbl-btn">View</button><button class="tbl-btn danger">Ban</button></td></tr>
            <tr><td><div class="user-cell"><div class="user-cell-av">A</div>Aryan Kapoor</div></td><td><span class="sbadge active">Active</span></td><td>28</td><td><button class="tbl-btn">View</button><button class="tbl-btn danger">Ban</button></td></tr>
            <tr><td><div class="user-cell"><div class="user-cell-av" style="background:linear-gradient(135deg,#fdcb6e,#e17055)">X</div>Unknown User</div></td><td><span class="sbadge pending">Pending</span></td><td>2</td><td><button class="tbl-btn">Approve</button><button class="tbl-btn danger">Reject</button></td></tr>
            <tr><td><div class="user-cell"><div class="user-cell-av" style="background:linear-gradient(135deg,#ff4d6d,#c0392b)">B</div>BadActor99</div></td><td><span class="sbadge banned">Banned</span></td><td>0</td><td><button class="tbl-btn">Unban</button><button class="tbl-btn danger">Delete</button></td></tr>
          </table>
        </div>
        <div class="admin-panel">
          <div class="ap-title">📊 Content by Category</div>
          <div class="bar-chart">
            <div class="bar-row"><div class="bar-lbl">Tech</div><div class="bar-track"><div class="bar-fill" style="width:88%"></div></div><div class="bar-val">88%</div></div>
            <div class="bar-row"><div class="bar-lbl">Travel</div><div class="bar-track"><div class="bar-fill" style="width:72%"></div></div><div class="bar-val">72%</div></div>
            <div class="bar-row"><div class="bar-lbl">Design</div><div class="bar-track"><div class="bar-fill" style="width:65%"></div></div><div class="bar-val">65%</div></div>
            <div class="bar-row"><div class="bar-lbl">Food</div><div class="bar-track"><div class="bar-fill" style="width:54%"></div></div><div class="bar-val">54%</div></div>
            <div class="bar-row"><div class="bar-lbl">Music</div><div class="bar-track"><div class="bar-fill" style="width:48%"></div></div><div class="bar-val">48%</div></div>
            <div class="bar-row"><div class="bar-lbl">Health</div><div class="bar-track"><div class="bar-fill" style="width:38%"></div></div><div class="bar-val">38%</div></div>
            <div class="bar-row"><div class="bar-lbl">Finance</div><div class="bar-track"><div class="bar-fill" style="width:29%"></div></div><div class="bar-val">29%</div></div>
          </div>
        </div>
      </div>
      <div class="admin-panels">
        <div class="admin-panel">
          <div class="ap-title">🚩 Reports Queue</div>
          <div class="report-list">
            <div class="report-row"><div class="report-type-icon">⚠️</div><div class="report-info"><div class="report-title">Spam post by @test123</div><div class="report-meta">Reported by 3 users · 2 hrs ago</div></div><button class="tbl-btn" onclick="showToast('✅ Post removed!','success')">Remove</button><button class="tbl-btn" onclick="showToast('✓ Dismissed report','success')">Dismiss</button></div>
            <div class="report-row"><div class="report-type-icon">🚫</div><div class="report-info"><div class="report-title">Misleading article title</div><div class="report-meta">Reported by 1 user · 5 hrs ago</div></div><button class="tbl-btn" onclick="showToast('✅ Post removed!','success')">Remove</button><button class="tbl-btn" onclick="showToast('✓ Dismissed','success')">Dismiss</button></div>
            <div class="report-row"><div class="report-type-icon">👁️</div><div class="report-info"><div class="report-title">Inappropriate comment</div><div class="report-meta">Reported by 2 users · Yesterday</div></div><button class="tbl-btn" onclick="showToast('✅ Comment removed!','success')">Remove</button><button class="tbl-btn" onclick="showToast('✓ Dismissed','success')">Dismiss</button></div>
          </div>
        </div>
        <div class="admin-panel">
          <div class="ap-title">📝 Recent Posts</div>
          <table class="admin-tbl">
            <tr><th>Post</th><th>Author</th><th>Likes</th><th>Action</th></tr>
            <tr><td style="max-width:140px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;">UI Design Trends 2025</td><td>Aryan</td><td>247</td><td><button class="tbl-btn" onclick="showToast('📌 Post pinned!','success')">Pin</button></td></tr>
            <tr><td>Coorg Travel Guide</td><td>Sanya</td><td>512</td><td><button class="tbl-btn" onclick="showToast('📌 Post pinned!','success')">Pin</button></td></tr>
            <tr><td>System Design Guide</td><td>Rahul</td><td>891</td><td><button class="tbl-btn" onclick="showToast('📌 Post pinned!','success')">Pin</button></td></tr>
            <tr><td>Welcome to Orbix</td><td>Vedansh</td><td>2.4K</td><td><button class="tbl-btn" onclick="showToast('✅ Already pinned!','success')">Pinned</button></td></tr>
          </table>
        </div>
      </div>
      <div class="admin-full-panel">
        <div class="ap-title">⚙️ Platform Settings</div>
        <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:12px;">
          <button class="btn btn-outline" onclick="showToast('✅ Maintenance mode toggled!','success')">🔧 Maintenance Mode</button>
          <button class="btn btn-outline" onclick="showToast('✅ Registrations updated!','success')">🔓 Toggle Registrations</button>
          <button class="btn btn-outline" onclick="showToast('📧 Email sent to all users!','success')">📧 Broadcast Email</button>
          <button class="btn btn-outline" onclick="showToast('📊 Report generated!','success')">📊 Export Reports</button>
          <button class="btn btn-outline" onclick="showToast('🗃️ Backup started!','success')">🗃️ Backup Data</button>
          <button class="btn btn-outline" onclick="showToast('🧹 Cache cleared!','success')">🧹 Clear Cache</button>
          <button class="btn btn-outline" onclick="showToast('🔍 SEO audit running...','success')">🔍 SEO Audit</button>
          <button class="btn btn-outline" onclick="showToast('🛡️ Security scan started!','success')">🛡️ Security Scan</button>
        </div>
      </div>
    </div>

  </main>
</div><!-- end #app -->

<script>
/* ========== STATE ========== */
const ADMIN = { username:'Vedansh', password:'7834962879', name:'Vedansh', isAdmin:true };
let currentUser = null;
let currentPage = 'feed';
let isDark = true;
let likedPosts = new Set(['4']);
let likedReels = new Set();
let following = new Set();
let uploadTags = [];
let selectedFile = null;
let postCount = 12;

/* ========== AUTH ========== */
function switchAuthTab(tab) {
  document.querySelectorAll('.auth-tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.auth-tab')[tab==='login'?0:1].classList.add('active');
  document.getElementById('login-form').style.display = tab==='login'?'block':'none';
  document.getElementById('register-form').style.display = tab==='register'?'block':'none';
}

function doLogin() {
  const u = document.getElementById('login-username').value.trim();
  const p = document.getElementById('login-password').value.trim();
  const err = document.getElementById('login-error');
  if(u===ADMIN.username && p===ADMIN.password) {
    currentUser = {...ADMIN};
    launchApp();
  } else if(u && p && p.length>=6) {
    // Registered user login simulation
    currentUser = {username:u, name:u, isAdmin:false};
    launchApp();
  } else {
    err.style.display='block';
    setTimeout(()=>err.style.display='none',3000);
  }
}

function doRegister() {
  const name = document.getElementById('reg-name').value.trim();
  const u = document.getElementById('reg-username').value.trim();
  const p = document.getElementById('reg-password').value.trim();
  const e = document.getElementById('reg-email').value.trim();
  const err = document.getElementById('reg-error');
  const suc = document.getElementById('reg-success');
  if(!name||!u||!p||!e){err.textContent='❌ Please fill in all fields.';err.style.display='block';return;}
  if(u===ADMIN.username){err.textContent='❌ Username already taken.';err.style.display='block';return;}
  if(p.length<6){err.textContent='❌ Password must be at least 6 characters.';err.style.display='block';return;}
  err.style.display='none';
  suc.textContent='✅ Account created! Signing you in...';
  suc.style.display='block';
  setTimeout(()=>{
    currentUser = {username:u, name:name, isAdmin:false};
    launchApp();
  },1200);
}

function guestLogin() {
  currentUser = {username:'Guest', name:'Guest User', isAdmin:false, isGuest:true};
  launchApp();
}

function launchApp() {
  document.getElementById('auth-screen').style.display='none';
  document.getElementById('app').style.display='block';
  // Set up UI based on user
  const initials = currentUser.name.charAt(0).toUpperCase();
  document.getElementById('nav-avatar-btn').textContent = initials;
  document.getElementById('profile-avatar').textContent = initials;
  document.getElementById('profile-name-display').innerHTML = currentUser.name + (currentUser.isAdmin?' <span class="crown">👑</span>':'') + (currentUser.isGuest?' <span style="font-size:0.75rem;padding:2px 8px;border-radius:100px;background:var(--border);color:var(--text2);">Guest</span>':'');
  document.getElementById('profile-handle').textContent = '@'+currentUser.username + (currentUser.isAdmin?' · Admin':'') + (currentUser.isGuest?' · Guest':'');
  document.getElementById('status-name').textContent = currentUser.name;
  if(currentUser.isAdmin){
    document.getElementById('admin-nav-section').style.display='block';
    document.getElementById('admin-dd-item').classList.remove('hidden');
  }
  navTo('feed');
  showToast('👋 Welcome to Orbix, '+currentUser.name+'!','success');
}

function doLogout() {
  currentUser = null;
  document.getElementById('app').style.display='none';
  document.getElementById('auth-screen').style.display='flex';
  document.getElementById('login-username').value='';
  document.getElementById('login-password').value='';
  closeDropdown();
  showToast('👋 Signed out successfully','success');
  switchAuthTab('login');
}

/* ========== NAVIGATION ========== */
function navTo(page) {
  if(page==='admin' && (!currentUser||!currentUser.isAdmin)){showToast('🔒 Admin access only!','error');return;}
  if(currentUser&&currentUser.isGuest && ['upload','admin'].includes(page)){
    showToast('🔒 Please sign in to '+page,'error');return;
  }
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.snav-item').forEach(i=>i.classList.remove('active'));
  const pg = document.getElementById('page-'+page);
  if(pg) pg.classList.add('active');
  const snav = document.getElementById('snav-'+page);
  if(snav) snav.classList.add('active');
  currentPage = page;
  closeDropdown();
  // Close panels
  document.getElementById('notif-panel').classList.remove('open');
  window.scrollTo({top:0,behavior:'smooth'});
}

/* ========== DROPDOWN / NOTIFS ========== */
function toggleDropdown() {
  const dd = document.getElementById('nav-dropdown');
  dd.classList.toggle('open');
  document.getElementById('notif-panel').classList.remove('open');
}
function closeDropdown() {
  document.getElementById('nav-dropdown').classList.remove('open');
}
function toggleNotif() {
  document.getElementById('notif-panel').classList.toggle('open');
  closeDropdown();
  document.getElementById('notif-count').style.display='none';
}
function clearNotifs() {
  document.querySelectorAll('.notif-dot').forEach(d=>d.remove());
  showToast('✅ All notifications marked as read','success');
}

document.addEventListener('click', function(e){
  if(!e.target.closest('.nav-avatar')&&!e.target.closest('.nav-dropdown')) closeDropdown();
  if(!e.target.closest('.nav-btn')&&!e.target.closest('.notif-panel')) {
    if(!e.target.closest('[onclick*="toggleNotif"]')) document.getElementById('notif-panel').classList.remove('open');
  }
});

/* ========== THEME ========== */
function toggleTheme() {
  isDark = !isDark;
  document.documentElement.setAttribute('data-theme', isDark?'dark':'light');
  document.getElementById('theme-btn').textContent = isDark?'🌙':'☀️';
  showToast(isDark?'🌙 Dark theme activated':'☀️ Light theme activated','success');
}

/* ========== LIKE / INTERACT ========== */
function toggleLike(id) {
  const btn = document.getElementById('like-'+id);
  const cnt = document.getElementById('like-count-'+id);
  if(!currentUser||currentUser.isGuest){showToast('🔒 Sign in to like posts!','error');return;}
  if(likedPosts.has(id)){
    likedPosts.delete(id);
    btn.classList.remove('liked');
    btn.querySelector('.pi').textContent='🤍';
    const c = parseInt(cnt.textContent.replace('k',''))||0;
    cnt.textContent = cnt.textContent.includes('k')?(parseFloat(cnt.textContent)-0.1).toFixed(1)+'k':(c-1);
    showToast('💔 Like removed','success');
  } else {
    likedPosts.add(id);
    btn.classList.add('liked');
    btn.querySelector('.pi').textContent='❤️';
    const c = parseInt(cnt.textContent.replace('k',''))||0;
    cnt.textContent = cnt.textContent.includes('k')?(parseFloat(cnt.textContent)+0.1).toFixed(1)+'k':(c+1);
    showToast('❤️ Liked!','success');
  }
}

function toggleReelLike(id) {
  if(!currentUser||currentUser.isGuest){showToast('🔒 Sign in to like!','error');return;}
  const btn = document.getElementById('rl-'+id);
  if(likedReels.has(id)){
    likedReels.delete(id);
    btn.textContent='🤍';
    btn.classList.remove('reel-liked');
  } else {
    likedReels.add(id);
    btn.textContent='❤️';
    btn.classList.add('reel-liked');
    showToast('❤️ Reel liked!','success');
  }
}

function toggleComments(id) {
  const el = document.getElementById(id);
  if(el) el.classList.toggle('hidden');
}

function addComment(postId) {
  if(!currentUser||currentUser.isGuest){showToast('🔒 Sign in to comment!','error');return;}
  const input = document.getElementById('cmt-input-'+postId);
  const val = input.value.trim();
  if(!val) return;
  const container = input.closest('.comments-inner');
  const newCmt = document.createElement('div');
  newCmt.className='cmt';
  newCmt.innerHTML=`<div class="cmt-av av-purple">${currentUser.name.charAt(0)}</div><div class="cmt-bubble"><div class="cmt-name">${currentUser.name}</div><div class="cmt-text">${val}</div></div>`;
  container.insertBefore(newCmt, input.closest('.cmt-input-row'));
  input.value='';
  showToast('💬 Comment posted!','success');
}

function toggleFollow(btn) {
  if(!currentUser||currentUser.isGuest){showToast('🔒 Sign in to follow!','error');return;}
  if(btn.classList.contains('following')){
    btn.classList.remove('following');
    btn.textContent='Follow';
    showToast('✖ Unfollowed','success');
  } else {
    btn.classList.add('following');
    btn.textContent='Following';
    showToast('✅ Following!','success');
  }
}

/* ========== UPLOAD ========== */
function selectType(el,type) {
  document.querySelectorAll('.type-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  showToast('📝 Mode: '+type,'success');
}

function updateChar(inputId, countId, max) {
  const val = document.getElementById(inputId).value.length;
  document.getElementById(countId).textContent = val+' / '+max;
}

function onDragOver(e){e.preventDefault();document.getElementById('drop-zone').classList.add('over');}
function onDragLeave(){document.getElementById('drop-zone').classList.remove('over');}
function onDrop(e){
  e.preventDefault();
  document.getElementById('drop-zone').classList.remove('over');
  const files=e.dataTransfer.files;
  if(files.length) handleFile(files[0]);
}
function onFileSelect(e){if(e.target.files.length) handleFile(e.target.files[0]);}

function handleFile(file) {
  selectedFile = file;
  const preview = document.getElementById('file-preview');
  preview.classList.add('show');
  document.getElementById('fp-name').textContent = file.name;
  document.getElementById('fp-size').textContent = (file.size/1024/1024).toFixed(2)+' MB';
  document.getElementById('fp-icon').textContent = file.type.startsWith('video')?'🎬':file.type.startsWith('image')?'🖼️':'📄';
  showToast('✅ File added: '+file.name,'success');
}

function removeFile(){
  selectedFile=null;
  document.getElementById('file-preview').classList.remove('show');
  document.getElementById('file-input').value='';
  showToast('🗑️ File removed','success');
}

function addTag(e){if(e.key==='Enter'){e.preventDefault();addTagBtn();}}
function addTagBtn(){
  const input=document.getElementById('tag-input');
  const val=input.value.trim().replace(/\s+/g,'').replace(/^#/,'');
  if(!val||uploadTags.includes(val)||uploadTags.length>=8) return;
  uploadTags.push(val);
  renderTags();
  input.value='';
}
function removeTag(tag){uploadTags=uploadTags.filter(t=>t!==tag);renderTags();}
function renderTags(){
  const d=document.getElementById('tags-display');
  d.innerHTML=uploadTags.map(t=>`<div class="tag-chip">#${t}<button class="tag-rm" onclick="removeTag('${t}')">✕</button></div>`).join('');
}

function submitPost(){
  if(!currentUser||currentUser.isGuest){showToast('🔒 Please sign in to post!','error');return;}
  const title=document.getElementById('upload-title').value.trim();
  const desc=document.getElementById('upload-desc').value.trim();
  if(!title||!desc){showToast('❌ Title and description are required!','error');return;}
  postCount++;
  document.getElementById('stat-posts').textContent=postCount;
  showToast('🚀 Post published successfully!','success');
  document.getElementById('upload-title').value='';
  document.getElementById('upload-desc').value='';
  document.getElementById('title-char').textContent='0 / 120';
  document.getElementById('desc-char').textContent='0 / 2000';
  uploadTags=[];renderTags();
  selectedFile=null;document.getElementById('file-preview').classList.remove('show');
  setTimeout(()=>navTo('feed'),1000);
}

/* ========== FILTERS ========== */
function filterArticles(el,cat){
  document.querySelectorAll('#page-articles .fpill').forEach(p=>p.classList.remove('active'));
  el.classList.add('active');
  showToast('🔍 Filtering: '+cat,'success');
}
function filterReels(el,cat){
  document.querySelectorAll('#page-reels .fpill').forEach(p=>p.classList.remove('active'));
  el.classList.add('active');
  showToast('🎬 Showing: '+cat+' reels','success');
}
function setExploreCat(el){
  document.querySelectorAll('.explore-cat-btn').forEach(b=>b.classList.remove('active'));
  el.classList.add('active');
  showToast('🔍 Browsing: '+el.textContent,'success');
}

/* ========== PROFILE TABS ========== */
function profileTab(el,tab){
  document.querySelectorAll('.ptab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  ['media','posts','reels','articles','saved','about'].forEach(t=>{
    const el=document.getElementById('profile-tab-'+t);
    if(el) el.classList.toggle('hidden',t!==tab);
  });
}

/* ========== MODAL ========== */
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}
document.querySelectorAll('.modal-overlay').forEach(m=>{
  m.addEventListener('click',function(e){if(e.target===this)closeModal(this.id);});
});
function copyLink(){
  const val=document.getElementById('share-link-val').value;
  navigator.clipboard.writeText(val).catch(()=>{});
  showToast('🔗 Link copied!','success');
}

/* ========== SEARCH ========== */
function handleSearch(val){
  if(val.length>2) showToast('🔍 Searching for "'+val+'"...','success');
}

/* ========== TOAST ========== */
function showToast(msg,type='success'){
  const container=document.getElementById('toast');
  const toast=document.createElement('div');
  toast.className='toast-item '+type;
  toast.innerHTML=msg;
  container.appendChild(toast);
  setTimeout(()=>{toast.style.opacity='0';toast.style.transform='translateX(40px)';toast.style.transition='all .3s';setTimeout(()=>toast.remove(),350);},2500);
}
</script>
</body>
</html>
