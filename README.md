<!DOCTYPE html>
<html lang="uz"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover,user-scalable=no">
<title>MiniCraft</title>
<style>
:root{--ui:rgba(0,0,0,.55);--fg:#fff;--ac:#5fa83a}
@media (prefers-color-scheme:dark){:root{--ui:rgba(0,0,0,.65)}}
html,body{margin:0;height:100%;overflow:hidden;background:#87ceeb;color:var(--fg);font:14px system-ui,sans-serif;touch-action:none;user-select:none;-webkit-user-select:none}
canvas{display:block;width:100%;height:100%}
.hud{position:fixed;pointer-events:none}
#cross{left:50%;top:50%;transform:translate(-50%,-50%);font-size:26px;text-shadow:0 0 3px #000}
#hp{left:50%;transform:translateX(-50%);bottom:calc(60px + env(safe-area-inset-bottom,0px));font-size:18px;text-shadow:0 0 3px #000;white-space:nowrap}
#hp i{font-style:normal;color:#e33}#hp i.e{color:#555}#hp i.h{opacity:.55}
#fd{left:50%;transform:translateX(-50%);bottom:calc(84px + env(safe-area-inset-bottom,0px));font-size:15px;text-shadow:0 0 3px #000;white-space:nowrap}#fd i{font-style:normal}#fd i.h{opacity:.6}#fd i.e{filter:grayscale(1);opacity:.35}
#bar{left:50%;transform:translateX(-50%);bottom:calc(8px + env(safe-area-inset-bottom,0px));display:flex;gap:2px;pointer-events:auto}
.s{width:36px;height:44px;background:var(--ui);border:2px solid #666;box-sizing:border-box;font-size:9px;display:flex;justify-content:center;align-items:center;border-radius:4px;position:relative;text-shadow:0 0 3px #000}
.s.on{border-color:#fff}.s b{font-size:11px;position:absolute;right:2px;bottom:0}
#tip{top:calc(10px + env(safe-area-inset-top,0px));left:50%;transform:translateX(-50%);background:var(--ui);padding:6px 12px;border-radius:6px;opacity:0;transition:opacity .3s;white-space:nowrap}
#fx{inset:0;background:#f00;opacity:0;transition:opacity .4s}
.ov{position:fixed;inset:0;background:rgba(0,0,0,.72);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;text-align:center;padding:20px;z-index:5}
.ov h1{margin:0;font-size:32px}.ov p{margin:0;max-width:420px;line-height:1.5}
.ov button{font:inherit;color:#fff;background:var(--ac);border:0;border-radius:8px;padding:12px 28px;font-size:18px}
.touch .dk,body:not(.touch) .mb,body:not(.touch) .tb,body:not(.touch) #jr{display:none}
.tb{position:fixed;width:50px;height:50px;border-radius:5px;background:var(--ui);border:2px solid #fff8;display:flex;align-items:center;justify-content:center;font-size:10px;text-align:center;line-height:1.1}
#bj{right:52px;bottom:calc(190px + env(safe-area-inset-bottom,0px))}
#bk{right:14px;bottom:calc(120px + env(safe-area-inset-bottom,0px))}
#bp{right:90px;bottom:calc(120px + env(safe-area-inset-bottom,0px))}
#jr{position:fixed;left:18px;bottom:calc(120px + env(safe-area-inset-bottom,0px));width:96px;height:96px;border-radius:6px;border:2px solid #fff8;background:rgba(0,0,0,.2);pointer-events:none}
#jk{position:absolute;left:30px;top:30px;width:36px;height:36px;border-radius:4px;background:#fffa}
#bi{position:fixed;z-index:3;right:12px;top:calc(12px + env(safe-area-inset-top,0px));background:var(--ui);color:#fff;border:2px solid #fff8;border-radius:10px;padding:8px 12px;font:inherit}
#tip{z-index:9}
#ig{display:grid;grid-template-columns:repeat(4,72px);gap:8px}
#ig .s{width:72px;height:72px;font-size:13px}#ig .s b{font-size:16px;right:5px;bottom:3px}

#os{background:rgba(0,0,0,.18);backdrop-filter:blur(5px);-webkit-backdrop-filter:blur(5px);justify-content:flex-start;padding-top:calc(7vh + env(safe-area-inset-top,0px))}
.lg{position:relative;display:inline-block}
.logo{margin:0;font:900 clamp(38px,13vw,84px)/1 "Courier New",monospace;letter-spacing:.05em;color:transparent;-webkit-text-stroke:2px #2b2824;background-clip:text;-webkit-background-clip:text;background-size:32px;image-rendering:pixelated;filter:drop-shadow(4px 5px 0 #1d1b19)}
.sub{margin:8px auto 0;display:table;padding:3px 18px;font:700 clamp(13px,3.8vw,20px) "Courier New",monospace;color:#eee;background:#6d6760;border:3px solid #2b2824;box-shadow:inset 0 0 0 2px #8a847d;letter-spacing:.18em}
.splash{position:absolute;right:-12px;bottom:-16px;white-space:nowrap;color:#ff0;text-shadow:2px 2px 0 #3f3f00;font:700 16px "Courier New",monospace;transform:rotate(-18deg);animation:pls .8s infinite alternate}
@keyframes pls{from{transform:rotate(-18deg) scale(1)}to{transform:rotate(-18deg) scale(1.12)}}
.mn{margin:auto 0 12vh;display:flex;flex-direction:column;align-items:center;gap:10px}
.row{display:flex;gap:10px;width:min(78vw,340px)}
#os .mbn{display:block;width:min(78vw,340px);padding:14px 0;border-radius:0;border:0;font:700 clamp(17px,5vw,24px) "Courier New",monospace;color:#fff;background:#9a8f88;box-shadow:inset -4px -4px 0 #6b625c,inset 4px 4px 0 #b9aea6,0 0 0 3px #2b2824;text-shadow:2px 2px 0 #3d3835}
#os .mbn:active{background:#7b716b}
#os .row .mbn{width:auto;flex:1;padding:12px 0;font-size:clamp(13px,3.8vw,18px)}
#hlp{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);width:min(88vw,420px);box-sizing:border-box;background:rgba(0,0,0,.85);padding:16px;border:3px solid #2b2824;text-align:left;z-index:2}
#hlp p{margin:0 0 8px;font-size:14px}
.cp,.vr{position:absolute;bottom:calc(8px + env(safe-area-inset-bottom,0px));font:700 14px "Courier New",monospace;color:#fff;text-shadow:2px 2px 0 #333}.cp{left:10px}.vr{right:10px}
body.m .hud,body.m .tb,body.m #bi,body.m #jr{visibility:hidden}
#pb{left:50%;top:calc(50% + 22px);transform:translateX(-50%);width:60px;height:6px;background:rgba(0,0,0,.5);border:1px solid #fff8;display:none}#pb i{display:block;height:100%;width:0;background:#fff}
#fade{inset:0;background:#000;opacity:0;transition:opacity .8s;z-index:8}
#bd{right:128px;bottom:calc(190px + env(safe-area-inset-bottom,0px));display:none}
body.fly #bd{display:flex}body:not(.touch) #bd{display:none!important}
#bar .s{font-size:8px}
#edb{position:fixed;left:50%;top:calc(10px + env(safe-area-inset-top,0px));transform:translateX(-50%);z-index:9;display:none;flex-direction:column;align-items:center;background:rgba(0,0,0,.82);padding:8px 12px;border-radius:8px;text-align:center;font-size:13px}
body.ed #edb{display:flex}#edb button{font:inherit;color:#fff;background:var(--ac);border:0;border-radius:6px;padding:8px 16px;margin:6px 4px 0}
body.ed .tb{display:flex!important}body.ed #bd{display:flex!important}body.ed #jr{display:block!important}
body.ed .tb,body.ed #jr,body.ed #bi,body.ed #bar{outline:2px dashed #ff0;pointer-events:auto}

#bk{right:10px;bottom:calc(110px + env(safe-area-inset-bottom,0px))}#bp{right:66px;bottom:calc(110px + env(safe-area-inset-bottom,0px))}
#bj{right:10px;bottom:calc(166px + env(safe-area-inset-bottom,0px))}#bd{right:66px;bottom:calc(166px + env(safe-area-inset-bottom,0px))}
#bq{right:10px;bottom:calc(222px + env(safe-area-inset-bottom,0px))}#bf{right:66px;bottom:calc(222px + env(safe-area-inset-bottom,0px))}
#bi{border-radius:4px}.ov button{border-radius:4px}
.pl{display:flex;flex-direction:column;gap:8px;max-height:46vh;overflow:auto;width:min(86vw,360px)}
.rc{font:inherit!important;font-size:14px!important;color:#fff;background:#6d6760!important;border:2px solid #2b2824!important;padding:10px!important;text-align:left}.rc:disabled{opacity:.4}
.wr{display:flex;gap:6px;align-items:center;background:var(--ui);padding:8px;border-radius:4px}.wr span{flex:1;text-align:left;font-size:14px}.wr button{padding:8px 10px!important;font-size:13px!important}
.ov input{font:inherit;padding:10px;border-radius:4px;border:2px solid #2b2824;width:min(80vw,300px);box-sizing:border-box}.ov label{font-size:12px;opacity:.8;margin-bottom:-8px}
.pb2{width:min(80vw,300px);height:10px;background:#0006;border:1px solid #fff8}.pb2 i{display:block;height:100%;width:0;background:#e08a20}
.row2{display:flex;gap:8px;flex-wrap:wrap;justify-content:center}.row2 button{padding:10px 14px!important;font-size:14px!important}
#ig{max-height:40vh;overflow:auto}
.ov textarea{width:min(86vw,320px);font:11px monospace;padding:8px;border-radius:4px;border:2px solid #2b2824;box-sizing:border-box}
#os,#mp{overflow:auto}
.scr{padding:0!important;gap:0!important;justify-content:flex-start!important;align-items:stretch!important;background:rgba(0,0,0,.2)!important;backdrop-filter:blur(5px);-webkit-backdrop-filter:blur(5px);font-family:"Courier New",monospace;overflow:auto;text-align:left!important}
.hdr{display:flex;align-items:center;justify-content:space-between;background:#706a6e;border-bottom:3px solid #2b2824;padding:8px 10px;padding-top:calc(8px + env(safe-area-inset-top,0px));font:700 clamp(16px,4.5vw,22px) "Courier New",monospace;text-shadow:2px 2px 0 #3d3835;flex:none}
.hdr .hb{padding:8px 14px!important;font:700 14px "Courier New",monospace!important;color:#fff;background:#9a8f88!important;border-radius:0!important;box-shadow:inset -3px -3px 0 #6b625c,inset 3px 3px 0 #b9aea6,0 0 0 2px #2b2824;text-shadow:2px 2px 0 #3d3835}
.pn2{margin:14px 12px;background:#9a8f88;border:3px solid #6b625c;box-shadow:0 0 0 3px #2b2824;padding:10px;flex:1;min-height:0;overflow:auto}
.wr2{margin-bottom:8px;background:#7d746e;box-shadow:inset 0 0 0 2px #2b2824}
.wt{display:flex;align-items:stretch}.wm{flex:1;position:relative;padding:10px 12px;cursor:pointer}.wm b{display:block;font-size:17px;text-shadow:2px 2px 0 #3d3835}.wm small{display:block;font-size:13px;opacity:.85}.wm i{position:absolute;right:10px;top:10px;font-style:normal;font-size:13px;opacity:.85}
.pe{width:56px;font-size:24px!important;padding:0!important;background:#9a8f88!important;border-radius:0!important;box-shadow:inset -3px -3px 0 #6b625c,inset 3px 3px 0 #b9aea6;color:#fff}
.wx{display:none;gap:6px;padding:8px;flex-wrap:wrap}.wr2.open .wx{display:flex}.wx input{flex:1;min-width:120px}.wx button{padding:8px 12px!important;font-size:13px!important}
.emp{text-align:center;opacity:.9;margin:20px}
.nwb{display:grid;grid-template-columns:1fr 1fr;gap:14px;align-content:start}@media (max-width:560px){.nwb{grid-template-columns:1fr}}
.nwl label,.nwr label{display:block;margin-bottom:6px;font-size:15px;text-shadow:2px 2px 0 #3d3835}.nwl input{width:100%;background:#363232;color:#fff;border-color:#2b2824;font-size:17px;margin-bottom:8px}.nwl p{font-size:14px;line-height:1.4;text-shadow:1px 1px 0 #3d3835}
.seg{display:flex;margin-bottom:12px}.seg button{flex:1;padding:14px 0!important;font:700 16px "Courier New",monospace!important;color:#fff;background:#9a8f88!important;border-radius:0!important;box-shadow:inset -3px -3px 0 #6b625c,inset 3px 3px 0 #b9aea6,0 0 0 2px #2b2824}.seg button.sel{background:#706a6e!important;box-shadow:inset 3px 3px 0 #5a5458,0 0 0 2px #2b2824}
.cbtn{width:100%;padding:16px 0!important;font:700 18px "Courier New",monospace!important;color:#fff;background:#9a8f88!important;border-radius:0!important;box-shadow:inset -4px -4px 0 #6b625c,inset 4px 4px 0 #b9aea6,0 0 0 3px #2b2824;text-shadow:2px 2px 0 #3d3835}
.ov .gbtn{position:absolute;right:10px;bottom:calc(38px + env(safe-area-inset-bottom,0px));width:52px;height:52px;border-radius:0;font-size:26px;background:#9a8f88;box-shadow:inset -3px -3px 0 #6b625c,inset 3px 3px 0 #b9aea6,0 0 0 2px #2b2824;padding:0}
html{overflow:hidden;background:#000}
body.rot{position:fixed;top:0;left:100%;width:100vh;height:100vw;transform-origin:0 0;transform:rotate(90deg)}
.szr{display:flex;align-items:center;gap:6px;font-size:12px;margin-top:6px}.szr input{width:130px}.szr b{min-width:38px}
body.ed .sel{outline:3px solid #3f3!important}
</style></head><body>
<canvas id="cv"></canvas>
<div class="hud" id="cross">+</div><div class="hud" id="hp"></div><div class="hud" id="fd"></div><div class="hud" id="pb"><i></i></div><div class="hud" id="fade"></div><div class="hud" id="tip"></div><div class="hud" id="fx"></div>
<div class="hud" id="bar"></div>
<div id="jr"><div id="jk"></div></div>
<button id="bi">🎒 Sumka (I)</button>
<div class="tb" id="bj">Sakra</div><div class="tb" id="bd">Pastga</div><div class="tb" id="bf">Fonar</div><div class="tb" id="bq">Tashla</div><div class="tb" id="bk">Urish / Buzish</div><div class="tb" id="bp">Qo'yish</div>
<div class="ov" id="os">
<div class="lg"><div class="logo" id="logo">MINICRAFT</div><div class="sub">VEB VERSIYA</div><div class="splash" id="spl"></div></div>
<div class="mn"><button class="mbn" id="cont" style="display:none">Davom etish</button><button class="mbn" id="go">O'ynash</button>
<div class="row"><button class="mbn" id="op">Sozlamalar</button><button class="mbn" id="hb">Boshqaruv</button></div></div>
<div id="hlp" style="display:none"><p class="dk">WASD yurish · Probel sakrash · Chap tugma urish/buzish (har bosish — bir marta) · O'ng tugma blok qo'yish · 1–9, 0, - narsa tanlash · E ovqat yeyish · Q tashlash · F fonar · I sumka</p><p class="mb">Chap pastdagi doira bilan yuring, ekranni sudrab buriling. Tugmalar: Sakra, Urish/Buzish, Qo'yish. Sumka tugmasi o'ng yuqorida.</p><p>Qo'y va sigirni qilich bilan uring — go'sht tushadi. Har 4 blok balandlikdan yiqilsangiz 1 jon ketadi. Go'sht yesangiz qorin va jon to'ladi. Blokni sindirish uchun tugmani bosib turing. Kechasi zombilar chiqadi, quyosh chiqsa yonib o'ladi. Yotoqqa "Qo'yish" ni bosing — kechasi uxlab tongni kutasiz. Creative: cheksiz bloklar, jon ketmaydi, Probelni (yoki Sakra tugmasini) ikki marta bosing — uchasiz. Kraft stoli va Pechkaga "Qo'yish" tugmasi bilan kiring: go'shtni pishirasiz. Dunyolar o'zi saqlanadi.</p><p style="opacity:.6">(yopish uchun bosing)</p></div>
<span class="cp">©MiniCraft</span><span class="vr" id="vr">v1.2</span></div>
<div id="edb"><span>Tugmani bosib tanlang va sudrab joylang</span><div class="szr">Kichik <input type="range" id="edsz" min="50" max="200" value="100"> Katta <b id="edszv">100%</b></div><div><button id="edall">Hammasi</button><button id="edok">Tayyor</button><button id="edrs">Tiklash</button></div></div>
<div class="ov" id="iv" style="display:none"><h1>Sumka</h1><p id="ih"></p><div id="ig"></div><div class="row2"><button id="ie">Ovqat yeyish</button><button id="cr2">Yasash</button></div><div class="row2"><button id="ed2">Tugmalarni sozlash</button><button id="ex">Menyuga chiqish</button></div><button id="ic">Yopish</button></div>
<div class="ov" id="cr" style="display:none"><h1 id="crt">Yasash</h1><div id="crl" class="pl"></div><button id="crx">Yopish</button></div>
<div class="ov" id="fu" style="display:none"><h1>Pechka</h1><p id="fup"></p><div class="pb2"><i id="fub"></i></div><div id="ful" class="pl"></div><button id="fux">Yopish</button></div>
<div class="ov scr" id="wl" style="display:none"><div class="hdr"><button class="hb" id="wlx">Orqaga</button><span>O'ynash</span><button class="hb" id="wnew">Yangi</button></div><div class="pn2"><div id="wll"></div></div></div>
<div class="ov scr" id="nw" style="display:none"><div class="hdr"><button class="hb" id="nwx">Orqaga</button><span>Dunyo yaratish</span><button class="hb" id="nwa">Murakkab</button></div>
<div class="pn2 nwb"><div class="nwl"><label>Nom</label><input id="wn" maxlength="20" value="Mening dunyom"><input id="wsd" placeholder="Urug' raqami (ixtiyoriy)" style="display:none"><p id="nwd"></p></div>
<div class="nwr"><label>O'yin rejimi</label><div class="seg"><button id="nms" class="sel">Survival</button><button id="nmc">Creative</button></div><button class="cbtn" id="nwc">Dunyo yaratish!</button></div></div></div>
<div class="ov" id="st" style="display:none"><h1>Sozlamalar</h1><label>Ismingiz</label><input id="sn" maxlength="16"><label>Dunyo nomi</label><input id="sw" maxlength="20"><div class="row2"><button id="sf"></button><button id="ss"></button></div><button id="sup">Yangilanishni tekshirish</button><button id="ed">Tugmalarni sozlash</button><button id="sx">Saqlash</button></div>
<div class="ov" id="up" style="display:none;z-index:7"><h1>Yangilanish bor!</h1><p id="upt"></p><div class="pb2"><i id="upb"></i></div><div class="row2"><button id="upg">Yangilash</button><button id="upl">Keyinroq</button></div></div>
<div class="ov" id="od" style="display:none"><h1 id="dm"></h1><button id="rs">Qayta tug'ilish</button></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
const $=id=>document.getElementById(id),T=matchMedia('(pointer:coarse)').matches||'ontouchstart' in window;
if(T)document.body.classList.add('touch');
const W=64,D=64,H=28,B=new Uint8Array(W*D*H),hm=[],ix=(x,y,z)=>(y*D+z)*W+x;
const get=(x,y,z)=>{if(x<0||z<0||x>=W||z>=D||y<0)return 3;if(y>=H)return 0;return B[ix(x,y,z)]};
let sd=7;const rnd=()=>(sd=sd*16807%2147483647)/2147483647;
const hash=(a,b)=>{const h=Math.sin(a*127.1+b*311.7)*43758.5453;return h-Math.floor(h)};
function vn(x,z){const xi=Math.floor(x),zi=Math.floor(z),u=x-xi,v=z-zi,s=t=>t*t*(3-2*t),a=hash(xi,zi),b=hash(xi+1,zi),c=hash(xi,zi+1),d=hash(xi+1,zi+1);return a+(b-a)*s(u)+(c-a)*s(v)+(a-b-c+d)*s(u)*s(v)}
let SO=0;function gen(seed){B.fill(0);sd=(seed*7919)%2147483646+1;SO=seed*.731;
for(let x=0;x<W;x++){hm[x]=[];for(let z=0;z<D;z++){const h=Math.floor(6+vn(x*.07+SO,z*.07+SO)*9+vn(x*.2+SO,z*.2+SO)*2);hm[x][z]=h;for(let y=0;y<=h;y++)B[ix(x,y,z)]=y==h?1:y>=h-3?2:3}}
for(let n=0;n<45;n++){const x=3+Math.floor(rnd()*(W-6)),z=3+Math.floor(rnd()*(D-6));if(Math.abs(x-32)<5&&Math.abs(z-32)<5)continue;const h=hm[x][z];if(B[ix(x,h+1,z)])continue;
for(let y=1;y<=4;y++)B[ix(x,h+y,z)]=4;
for(let a=-2;a<=2;a++)for(let b=-2;b<=2;b++)for(let c=3;c<=5;c++){if(c==5&&(Math.abs(a)>1||Math.abs(b)>1))continue;if(Math.abs(a)==2&&Math.abs(b)==2)continue;const i=ix(x+a,h+c,z+b);if(!B[i])B[i]=5}}
}gen(7);
const renderer=new THREE.WebGLRenderer({canvas:$('cv'),antialias:true}),scene=new THREE.Scene(),camera=new THREE.PerspectiveCamera(75,1,.05,220);
renderer.setPixelRatio(Math.min(devicePixelRatio,2));scene.background=new THREE.Color(0xcfe9ff);scene.fog=new THREE.Fog(0xcfe9ff,30,85);
const sg=new THREE.SphereGeometry(110,16,12),sc=[],pa=sg.attributes.position;for(let i=0;i<pa.count;i++){const t=Math.max(0,pa.getY(i)/110),a=new THREE.Color(0xcfe9ff).lerp(new THREE.Color(0x3b7fe0),Math.pow(t,.6));sc.push(a.r,a.g,a.b)}sg.setAttribute('color',new THREE.Float32BufferAttribute(sc,3));
const sky=new THREE.Mesh(sg,new THREE.MeshBasicMaterial({vertexColors:true,side:THREE.BackSide,fog:false,depthWrite:false}));sky.renderOrder=-1;scene.add(sky);
const sunM=new THREE.Mesh(new THREE.PlaneGeometry(22,22),new THREE.MeshBasicMaterial({color:0xfff6c0,fog:false,depthWrite:false}));sunM.position.set(60,75,-50);sunM.lookAt(0,0,0);sky.add(sunM);
const clouds=[];for(let i=0;i<16;i++){const m=new THREE.Mesh(new THREE.BoxGeometry(8+Math.random()*10,1.6,5+Math.random()*6),new THREE.MeshBasicMaterial({color:0xffffff,transparent:true,opacity:.85,fog:false}));m.position.set(-40+Math.random()*180,38+Math.random()*6,-30+Math.random()*130);scene.add(m);clouds.push(m)}
const moonM=new THREE.Mesh(new THREE.PlaneGeometry(14,14),new THREE.MeshBasicMaterial({color:0xe8ecff,fog:false,depthWrite:false}));sky.add(moonM);
const sg2=[];for(let i=0;i<260;i++){const u=Math.random()*6.283,v=.1+Math.random()*.9,r=Math.sqrt(1-v*v);sg2.push(Math.cos(u)*r*100,v*100,Math.sin(u)*r*100)}
const sgeo=new THREE.BufferGeometry();sgeo.setAttribute('position',new THREE.Float32BufferAttribute(sg2,3));
const stars=new THREE.Points(sgeo,new THREE.PointsMaterial({size:1.8,color:0xffffff,transparent:true,opacity:0,fog:false,depthWrite:false}));sky.add(stars);
const RN=500,rp=new Float32Array(RN*6),qx=[],qz=[],qy=[];for(let i=0;i<RN;i++){qx.push(Math.random()*24);qz.push(Math.random()*24);qy.push(Math.random()*16)}
const rgeo=new THREE.BufferGeometry();rgeo.setAttribute('position',new THREE.BufferAttribute(rp,3));
const rainM=new THREE.LineSegments(rgeo,new THREE.LineBasicMaterial({color:0xa0b4d8,transparent:true,opacity:0,fog:false}));rainM.frustumCulled=false;scene.add(rainM);
let rainT=70,rsrc,rgain;
function startRain(){const a=AC,n=a.sampleRate*2,b=a.createBuffer(1,n,a.sampleRate),d=b.getChannelData(0);for(let i=0;i<n;i++)d[i]=Math.random()*2-1;rsrc=a.createBufferSource();rsrc.buffer=b;rsrc.loop=true;const f=a.createBiquadFilter();f.type='lowpass';f.frequency.value=1800;rgain=a.createGain();rgain.gain.value=0;rsrc.connect(f);f.connect(rgain);rgain.connect(mg);rsrc.start()}
function env(dt){if(on&&!dead)tod=(tod+dt/300)%1;
rainT-=dt;if(rainT<=0){rainT=60+Math.random()*120;rainG=Math.random()<.4?1:0}rain+=(rainG-rain)*Math.min(1,dt*.3);
const a=tod*6.2832,sy=Math.sin(a)+.2;SY=sy;FD=Math.min(1,Math.max(0,(sy+.1)/.35));
const w=FD*(1-.4*rain),k=.28+.72*w,kk=.06+.94*w;
wmat.color.setRGB(k*(.78+.22*FD),k*(.85+.15*FD),k);pmat.color.copy(wmat.color);
sky.material.color.setRGB(kk*(.6+.4*FD),kk*(.7+.3*FD),kk);
scene.background.setRGB(.81*kk,.91*kk,kk);scene.fog.color.copy(scene.background);
amb.intensity=.28+.5*w;sun.intensity=.1+.4*w;ham.intensity=.45+.5*w;
sunM.position.set(Math.cos(a)*80,sy*95,-30);sunM.lookAt(sky.position);sunM.visible=sy>-.05;
moonM.position.set(-Math.cos(a)*80,-sy*95,-30);moonM.lookAt(sky.position);moonM.visible=-sy>-.05;
stars.material.opacity=Math.max(0,1-FD*1.8)*(1-rain);
for(const c of clouds)c.material.color.setRGB(kk,kk,kk);
rainM.material.opacity=.5*rain;
if(rain>.03){const px=P.x,pz=P.z,py=P.y;for(let i=0;i<RN;i++){qy[i]-=22*dt;if(qy[i]<0)qy[i]+=16;const x=px-12+(((qx[i]-px+12)%24)+24)%24,z=pz-12+(((qz[i]-pz+12)%24)+24)%24,y=py-4+qy[i],j=i*6;rp[j]=x;rp[j+1]=y;rp[j+2]=z;rp[j+3]=x-.05;rp[j+4]=y-.6;rp[j+5]=z}rgeo.attributes.position.needsUpdate=true}
if(AC){if(!rsrc)startRain();rgain.gain.value=.1*rain}
FL.uNt.value=.25+(1-FD)*3;const fon=(S[sel]&&S[sel].k=='fonar'&&fonOn)?1:0;FL.uTI.value+=(fon*(1-.85*FD)-FL.uTI.value)*Math.min(1,dt*8);FL.uTP.value.copy(camera.position);camera.getWorldDirection(FL.uTD.value);fl.intensity=FL.uTI.value*1.4;fl.position.copy(camera.position)}camera.rotation.order='YXZ';
const amb=new THREE.AmbientLight(0xffffff,.75);scene.add(amb);const sun=new THREE.DirectionalLight(0xffffff,.5);sun.position.set(3,8,5);scene.add(sun);
var handCam;let ROTV=false;const VW=()=>ROTV?innerHeight:innerWidth,VH=()=>ROTV?innerWidth:innerHeight;
function updRot(){ROTV=T&&innerHeight>innerWidth;document.body.classList.toggle('rot',ROTV)}
const TP=(x,y)=>ROTV?[y,innerWidth-x]:[x,y];
function crect(e){const r=e.getBoundingClientRect();return ROTV?{left:r.top,top:innerWidth-r.right,width:r.bottom-r.top,height:r.right-r.left}:r}
function rz(){updRot();renderer.setSize(VW(),VH(),false);camera.aspect=VW()/VH();camera.updateProjectionMatrix();if(handCam){handCam.aspect=camera.aspect;handCam.updateProjectionMatrix();hand.position.x=Math.min(.5,camera.aspect*.3)}}addEventListener('resize',rz);rz();
const CL={1:[0x5fa83a,0x7a5a36,0x6b4a2b],2:[0x7a5a36,0x7a5a36,0x6b4a2b],3:[0x888888,0x808080,0x707070],4:[0xa88555,0x6a4d2a,0xa88555],5:[0x2f7a2a,0x2f7a2a,0x2f7a2a],6:[0xb03030,0x8a6a38,0x8a6a38],7:[0xb08a50,0xb08a50,0xb08a50],8:[0xa07a40,0xb08a50,0xb08a50],9:[0x7e7e7e,0x7e7e7e,0x7e7e7e],10:[0xf0b848,0xf0b848,0xf0b848]};
const F=[[1,0,0,.8,[1,0,0,1,1,0,1,1,1,1,0,1]],[-1,0,0,.8,[0,0,1,0,1,1,0,1,0,0,0,0]],[0,1,0,1,[0,1,1,1,1,1,1,1,0,0,1,0]],[0,-1,0,.5,[0,0,0,1,0,0,1,0,1,0,0,1]],[0,0,1,.7,[1,0,1,1,1,1,0,1,1,0,0,1]],[0,0,-1,.7,[0,0,0,0,1,0,1,1,0,1,0,0]]];
const cvA=document.createElement('canvas');cvA.width=240;cvA.height=16;const ctxA=cvA.getContext('2d');
function tile(i,sp,fn){for(let y=0;y<16;y++)for(let x=0;x<16;x++){const c=fn(x,y),n=(hash(x+i*17,y*3+i)-.5)*sp;const e=(x==0||y==0||x==15||y==15)?.9:1;ctxA.fillStyle=`rgb(${(((c>>16)&255)+n)*e|0},${(((c>>8)&255)+n)*e|0},${((c&255)+n)*e|0})`;ctxA.fillRect(i*16+x,y,1,1)}}
tile(0,10,(x,y)=>{const h=hash(x*3.1,y*7.7);return h>.8?0x3a6b2a:h<.2?0x5a8f40:0x477a33});
tile(1,8,(x,y)=>{const f=2+Math.floor(hash(x,5)*3);if(y<f)return hash(x,y)>.6?0x3a6b2a:0x477a33;if(y==f)return hash(x,9)>.5?0x3a6b2a:0x5b3d22;return hash(x*5,y*9)>.9?0x4a4a4a:hash(x,y*3)>.55?0x7a5230:0x6b4527});
tile(2,8,(x,y)=>{const h=hash(x*5,y*9);return h>.93?0x4a4a4a:h>.6?0x7a5230:h<.2?0x8d6038:0x6b4527});
tile(3,8,(x,y)=>{const r=y>>2,o=(r%2)*2,c=(x+o)>>2;if((y&3)==3||((x+o)&3)==3)return 0x45494a;const h=hash(c+r*7,r*3);return h>.66?0x8a8e8f:h<.33?0x6a6e6f:0x7a7e7f});
tile(4,8,(x,y)=>{const g=hash(x,1);if(g>.78)return 0x3a2a18;if(g<.25)return 0x5b4426;return hash(x,y>>1)>.85?0x4a3520:0x6b4f2c});
tile(5,8,(x,y)=>{const d=Math.max(Math.abs(x-7.5),Math.abs(y-7.5));if(d>6)return 0x5b4426;return (d|0)%2?0x9a7b45:0xb8935a});
tile(6,10,(x,y)=>{if(hash(x*9,y*5)>.9)return 0x0f2a0f;const h=hash(x,y);return h>.66?0x3a7a30:h<.33?0x24581f:0x2d6a27});
tile(7,6,(x,y)=>(y<5&&x>2&&x<13)?0xf2f2f2:0xb03030);
tile(8,6,(x,y)=>y<5?0xb03030:0x8a6a38);
tile(9,8,(x,y)=>{const r=y>>2;return (y&3)==3?0x7a5a2c:((x+r*5)%8==0?0x8a6a3a:0xb08a50)});
tile(10,6,(x,y)=>(x==0||y==0||x==15||y==15||x==5||x==10||y==5||y==10)?0x5a3a1a:0xa07a40);
tile(11,6,(x,y)=>y<3?0x6a4a22:(x>3&&x<12&&y>5&&y<12)?((x+y)%3?0x8a8f94:0x4a4f54):0xb08a50);
tile(12,8,(x,y)=>(x>3&&x<12&&y>6&&y<14)?(y>10?(hash(x,y)>.5?0xe08a20:0xf2c030):0x1c1c1c):((x+y)%7==0?0x666666:0x808080));
tile(13,8,(x,y)=>hash(x*3,y*5)>.7?0x6a6a6a:0x7e7e7e);
tile(14,10,(x,y)=>hash(x*3,y*7)>.7?0xfff0b0:hash(x*5,y)>.6?0xd89020:0xf0b848);
const tex=new THREE.CanvasTexture(cvA);tex.magFilter=tex.minFilter=THREE.NearestFilter;
const TL={1:[0,2,1],2:[2,2,2],3:[3,3,3],4:[5,5,4],5:[6,6,6],6:[7,5,8],7:[9,9,9],8:[10,9,11],9:[13,13,12],10:[14,14,14]};
const wmat=new THREE.MeshBasicMaterial({map:tex,vertexColors:true,side:THREE.DoubleSide});let wmesh;
const pl=[];function genPl(){pl.length=0;for(let x=0;x<W;x++)for(let z=0;z<D;z++){const h=hm[x][z];if(B[ix(x,h+1,z)])continue;const r=hash(x*1.7,z*2.3);if(r>.8)pl.push([x,h+1,z,r>.97?2+(hash(x,z)>.5?1:0):r>.9?1:0])}}genPl();
const pcv=document.createElement('canvas');pcv.width=64;pcv.height=16;const pc=pcv.getContext('2d');
function px(t,x,y,c){pc.fillStyle=c;pc.fillRect(t*16+x,y,1,1)}
for(let x=0;x<16;x++){if(hash(x,2)>.3){const h=3+Math.floor(hash(x,1)*7);for(let y=16-h;y<16;y++)px(0,x,y,hash(x,y)>.5?'#3f7a2c':'#4f9238')}
if(hash(x,6)>.25){const h=6+Math.floor(hash(x,4)*8);for(let y=16-h;y<16;y++)px(1,x,y,hash(x,y)>.5?'#386e27':'#4a8a34')}}
for(let y=7;y<16;y++){px(2,7,y,'#3f7a2c');px(3,7,y,'#3f7a2c')}
for(let a=5;a<=9;a++)for(let b=3;b<=7;b++){px(2,a,b,(a==7&&b==5)?'#e08a00':'#f2d21b');px(3,a,b,(a==7&&b==5)?'#d0c000':'#f4f4f4')}
const ptex=new THREE.CanvasTexture(pcv);ptex.magFilter=ptex.minFilter=THREE.NearestFilter;
const pmat=new THREE.MeshBasicMaterial({map:ptex,alphaTest:.5,side:THREE.DoubleSide,vertexColors:true});let pmesh;
function buildPlants(){const p=[],c=[],u=[],ind=[];let n=0;for(const[x,y,z,t]of pl){if(get(x,y-1,z)!=1||get(x,y,z))continue;const u0=t/4,u1=(t+1)/4;
for(const q of[[.1,.1,.9,.9],[.9,.1,.1,.9]]){p.push(x+q[0],y,z+q[1],x+q[2],y,z+q[3],x+q[2],y+.9,z+q[3],x+q[0],y+.9,z+q[1]);u.push(u0,0,u1,0,u1,1,u0,1);for(let i=0;i<12;i++)c.push(.9);ind.push(n,n+1,n+2,n,n+2,n+3);n+=4}}
if(pmesh){scene.remove(pmesh);pmesh.geometry.dispose();pmesh=null}if(!n)return;
const g=new THREE.BufferGeometry();g.setAttribute('position',new THREE.Float32BufferAttribute(p,3));g.setAttribute('color',new THREE.Float32BufferAttribute(c,3));g.setAttribute('uv',new THREE.Float32BufferAttribute(u,2));g.setIndex(ind);pmesh=new THREE.Mesh(g,pmat);pmesh.frustumCulled=false;scene.add(pmesh)}
const FL={uNt:{value:.25},uTP:{value:new THREE.Vector3()},uTD:{value:new THREE.Vector3(0,0,-1)},uTI:{value:0}};
function patchL(m){m.onBeforeCompile=sh=>{sh.uniforms.uTP=FL.uTP;sh.uniforms.uTD=FL.uTD;sh.uniforms.uTI=FL.uTI;sh.uniforms.uNt=FL.uNt;
sh.vertexShader=sh.vertexShader.replace('#include <common>','#include <common>\nvarying vec3 vWP;attribute float lamp;varying float vLamp;').replace('#include <begin_vertex>','#include <begin_vertex>\nvWP=(modelMatrix*vec4(transformed,1.0)).xyz;vLamp=lamp;');
sh.fragmentShader=sh.fragmentShader.replace('#include <common>','#include <common>\nvarying vec3 vWP;varying float vLamp;uniform float uNt;uniform vec3 uTP;uniform vec3 uTD;uniform float uTI;').replace('#include <dithering_fragment>','gl_FragColor.rgb*=1.0+vLamp*uNt;vec3 dv=vWP-uTP;float dl=length(dv);float cn=smoothstep(.78,.93,dot(dv/max(dl,.001),uTD));float fo=clamp(1.0-dl/20.0,0.0,1.0);gl_FragColor.rgb*=1.0+uTI*(cn*fo*3.0+fo*fo*.8);\n#include <dithering_fragment>')}}
patchL(wmat);patchL(pmat);
const fl=new THREE.PointLight(0xffeeb0,0,20);scene.add(fl);let fonOn=true;
function togFon(){fonOn=!fonOn;tip(fonOn?'Fonar yoqildi':"Fonar o'chdi")}
const D6=[[1,0,0],[-1,0,0],[0,1,0],[0,-1,0],[0,0,1],[0,0,-1]];
const LC=new Uint8Array(W*D*H);
const LV=(x,y,z)=>(x<0||z<0||x>=W||z>=D||y<0||y>=H)?0:LC[ix(x,y,z)];
function calcLight(){LC.fill(0);const qx=[],qy=[],qz=[];
for(let i=0;i<B.length;i++)if(B[i]==10){LC[i]=13;qx.push(i%W);qy.push((i/(W*D))|0);qz.push(((i%(W*D))/W)|0)}
for(let h=0;h<qx.length;h++){const x=qx[h],y=qy[h],z=qz[h],l=LC[ix(x,y,z)]-1;if(l<=0)continue;
for(const d of D6){const a=x+d[0],b=y+d[1],c=z+d[2];if(a<0||b<0||c<0||a>=W||b>=H||c>=D)continue;const i=ix(a,b,c);if(B[i]==0&&LC[i]<l){LC[i]=l;qx.push(a);qy.push(b);qz.push(c)}}}}
function rebuild(){const p=[],c=[],uv=[],lm=[],ind=[];let n=0;calcLight();
for(let y=0;y<H;y++)for(let z=0;z<D;z++)for(let x=0;x<W;x++){const id=B[ix(x,y,z)];if(!id)continue;
for(let f=0;f<6;f++){const[dx,dy,dz,sh,q]=F[f];if(get(x+dx,y+dy,z+dz))continue;const tl=TL[id][dy>0?0:dy<0?1:2],u0=tl/15+.002,u1=(tl+1)/15-.002;const k=sh*(.9+.2*hash(x*3+y*7+f,z*5+y)),lv=id==10?1.4:LV(x+dx,y+dy,z+dz)/12;
for(let i=0;i<4;i++){p.push(x+q[i*3],y+q[i*3+1],z+q[i*3+2]);c.push(k,k,k);lm.push(lv);uv.push(i<2?u0:u1,i==0||i==3?0:1)}ind.push(n,n+1,n+2,n,n+2,n+3);n+=4}}
const g=new THREE.BufferGeometry();g.setAttribute('position',new THREE.Float32BufferAttribute(p,3));g.setAttribute('color',new THREE.Float32BufferAttribute(c,3));g.setAttribute('uv',new THREE.Float32BufferAttribute(uv,2));g.setAttribute('lamp',new THREE.Float32BufferAttribute(lm,1));g.setIndex(ind);
if(wmesh){scene.remove(wmesh);wmesh.geometry.dispose()}wmesh=new THREE.Mesh(g,wmat);wmesh.frustumCulled=false;scene.add(wmesh);buildPlants()}
rebuild();
const AX=['x','z','y'];
function col(x,y,z,hw,h){for(let i=Math.floor(x-hw);i<=Math.floor(x+hw);i++)for(let k=Math.floor(z-hw);k<=Math.floor(z+hw);k++)for(let j=Math.floor(y);j<=Math.floor(y+h-.001);j++)if(get(i,j,k))return true;return false}
function move(o,dx,dy,dz,hw,h){const d={x:dx,z:dz,y:dy},n=Math.ceil(Math.max(Math.abs(dx),Math.abs(dy),Math.abs(dz))/.15)||1,r={x:0,y:0,z:0};
for(let s=0;s<n;s++)for(const a of AX){const v=d[a]/n;if(!v)continue;o[a]+=v;if(col(o.x,o.y,o.z,hw,h)){if(a=='y'&&v<0)o.y=Math.floor(o.y)+1;else o[a]-=v;r[a]=v<0?-1:1}}return r}
// o'yinchi
const handScene=new THREE.Scene();handCam=new THREE.PerspectiveCamera(60,camera.aspect,.01,10);const ham=new THREE.AmbientLight(0xffffff,.9);handScene.add(ham);const hl2=new THREE.DirectionalLight(0xffffff,.5);hl2.position.set(1,2,1);handScene.add(hl2);
const hand=new THREE.Group();hand.position.set(Math.min(.5,camera.aspect*.3),-.45,-.85);hand.rotation.set(-.15,.35,0);handScene.add(hand);
const arm=new THREE.Mesh(new THREE.BoxGeometry(.3,.3,1),new THREE.MeshLambertMaterial({color:0xa86f4f}));arm.position.set(0,-.05,.45);arm.scale.set(.7,.7,1);hand.add(arm);
let held=null,heldSel=-1,swing=0;
function tm(tl){const c=document.createElement('canvas');c.width=c.height=16;c.getContext('2d').drawImage(cvA,tl*16,0,16,16,0,0,16,16);const t=new THREE.CanvasTexture(c);t.magFilter=t.minFilter=THREE.NearestFilter;return new THREE.MeshLambertMaterial({map:t})}
function setHeld(){if(held)hand.remove(held);const s=S[sel];held=new THREE.Group();
const bx=(w,h,d,x,y,z,co)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),new THREE.MeshLambertMaterial({color:co}));m.position.set(x,y,z);held.add(m)};
if(s.k=='b'){const t=TL[s.id],a=tm(t[0]),b=tm(t[1]),c=tm(t[2]),m=new THREE.Mesh(new THREE.BoxGeometry(.55,.55,.55),[c,c,a,b,c,c]);m.position.set(0,.3,-.2);m.rotation.y=.6;held.add(m)}
else if(s.k=='sword'){bx(.1,.9,.06,0,.5,-.2,0xcfd8dc);bx(.4,.08,.1,0,.05,-.2,0x8b6b3d);bx(.08,.28,.08,0,-.12,-.2,0x6b4a2a)}
else if(s.k=='pick'){bx(.08,.9,.08,0,.2,-.2,0x7a5a2e);bx(.8,.1,.1,0,.65,-.2,0x9ea7ad)}
else if(s.k=='axe'){bx(.08,.9,.08,0,.2,-.2,0x7a5a2e);bx(.35,.3,.08,.18,.7,-.2,0x9ea7ad)}
else if(s.k=='shov'){bx(.08,.9,.08,0,.2,-.2,0x7a5a2e);bx(.28,.34,.06,0,.72,-.2,0x9ea7ad)}
else if(s.k=='fonar'){bx(.14,.5,.14,0,.3,-.2,0x555a60);bx(.2,.16,.2,0,.62,-.2,0xffe27a)}
else if(s.k=='f'){const m=new THREE.Mesh(new THREE.BoxGeometry(.5,.5,.06),new THREE.MeshLambertMaterial({map:ictex(s.id),transparent:true,alphaTest:.5}));m.position.set(0,.35,-.2);m.rotation.set(-.3,.5,0);held.add(m)}
held.scale.setScalar(.45);hand.add(held);heldSel=sel}
let started=false,creative=false,tod=.2,rain=0,rainG=0,FD=1,SY=1,dn=false,lastJ=0,zt=3;
const P={x:32.5,y:0,z:32.5,vy:0,hp:20,food:20,ft:0,ground:0,fs:0,rg:0};let yaw=0,pitch=0,on=false,dead=false,sel=0;
const inv={1:0,2:0,3:0,4:0,5:0,6:1,7:0,8:0,9:0,10:0,beef:0,mutton:0,cbeef:0,cmutton:0},keys={};let jx=0,jy=0,jh=false;
function spawn(){P.x=P.z=32.5;P.y=hm[32][32]+1;P.vy=0;P.fs=P.y;P.hp=20;P.food=20}spawn();
const S=[{n:"Qo'l",k:'hand'},{n:'Qilich',k:'sword'},{n:'Kirka',k:'pick'},{n:'Bel',k:'shov'},{n:'Bolta',k:'axe'},{n:'Fonar',k:'fonar'},
{n:"O't",k:'b',id:1},{n:'Tuproq',k:'b',id:2},{n:'Tosh',k:'b',id:3},{n:"Yog'och",k:'b',id:4},{n:'Barg',k:'b',id:5},{n:'Taxta',k:'b',id:7},{n:'Kraft',k:'b',id:8},{n:'Pechka',k:'b',id:9},{n:'Yotoq',k:'b',id:6},{n:'Chiroq',k:'b',id:10},
{n:"Mol go'shti",k:'f',id:'beef'},{n:"Qo'y go'shti",k:'f',id:'mutton'},{n:'Bifshteks',k:'f',id:'cbeef'},{n:'Kabob',k:'f',id:'cmutton'}];
const KI=(k,id)=>S.findIndex(s=>s.k==k&&(id===undefined||s.id===id));
let HB=[],hs=0;
function defHB(c){const t=[KI('sword'),KI('pick'),KI('shov'),KI('axe'),KI('fonar')];HB=c?t.concat([KI('b',1),KI('b',2),KI('b',3),KI('b',7)]):t.concat([KI('b',6),-1,-1,-1]);hs=0}
function newInv(c){Object.assign(inv,{1:0,2:0,3:0,4:0,5:0,6:c?0:1,7:0,8:0,9:0,10:0,beef:0,mutton:0,cbeef:0,cmutton:0});defHB(c)}
defHB(false);
for(let i=0;i<9;i++){const d=document.createElement('div');d.className='s';d.innerHTML='<span></span><b></b>';d.addEventListener('pointerdown',e=>{e.preventDefault();pickSlot(i)});$('bar').appendChild(d)}
const ICON={};for(const id in TL){const c=document.createElement('canvas');c.width=c.height=16;c.getContext('2d').drawImage(cvA,TL[id][2]*16,0,16,16,0,0,16,16);ICON[id]=c.toDataURL()}$('logo').style.backgroundImage=`url(${ICON[3]})`;
function mkc(f){const c=document.createElement('canvas');c.width=c.height=16;const q=c.getContext('2d');for(let y=0;y<16;y++)for(let x=0;x<16;x++){const v=f(x,y);if(v){q.fillStyle=v;q.fillRect(x,y,1,1)}}return c}
const IT={
beef:mkc((x,y)=>{const d=((x-7.5)/6.8)**2+((y-8)/4.8)**2;if(d>1)return 0;if(d>.74)return '#efe3dc';return hash(x*3,y)>.78?'#e8909a':hash(x,y*5)>.7?'#a82836':'#c23b4a'}),
mutton:mkc((x,y)=>{if(x>=11&&x<=14&&y>=7&&y<=9)return '#f4efe6';if(x==14&&(y==6||y==10))return '#f4efe6';const d=((x-6.5)/5.6)**2+((y-8)/5)**2;if(d>1)return 0;if(d>.72)return '#f6e4e0';return hash(x,y*3)>.75?'#f0b0b0':'#e0828c'}),
cbeef:mkc((x,y)=>{const d=((x-7.5)/6.8)**2+((y-8)/4.8)**2;if(d>1)return 0;if(d>.74)return '#5a2c14';return (x+y)%5==0?'#3f1d0c':hash(x,y*2)>.75?'#a0613a':'#7a3b1e'}),
cmutton:mkc((x,y)=>{if(x>=11&&x<=14&&y>=7&&y<=9)return '#f4efe6';if(x==14&&(y==6||y==10))return '#f4efe6';const d=((x-6.5)/5.6)**2+((y-8)/5)**2;if(d>1)return 0;if(d>.72)return '#6a3a1a';return (x*2+y)%6==0?'#4a2810':hash(x,y*3)>.75?'#c8884e':'#a8683a'})};
const IC={};for(const k in IT)IC[k]=IT[k].toDataURL();
const ictc={};function ictex(id){if(!ictc[id]){const t=new THREE.CanvasTexture(IT[id]);t.magFilter=t.minFilter=THREE.NearestFilter;ictc[id]=t}return ictc[id]}
const iconOf=s=>s.k=='b'?ICON[s.id]:s.k=='f'?IC[s.id]:null;
function fillSlot(e,s,n,o){const ic=iconOf(s);e.style.background=ic?`url(${ic}) center/100% 100%`:'';e.style.imageRendering='pixelated';e.firstChild.textContent=ic?'':s.n;e.lastChild.textContent=n;e.classList.toggle('on',o)}
function pickSlot(i){hs=i;sel=HB[i]>=0?HB[i]:0;ui()}
function renderGrid(){const g=$('ig');g.innerHTML='';$('ih').textContent='Katak '+(hs+1)+' tanlangan — narsani bosing';S.forEach((s,k)=>{if(k==0)return;const c=s.k=='b'||s.k=='f';if(c&&!creative&&!(inv[s.id]>0))return;const d=document.createElement('div');d.className='s';d.innerHTML='<span></span><b></b>';fillSlot(d,s,c?(creative?'∞':inv[s.id]):'',HB[hs]==k);d.addEventListener('pointerdown',e=>{e.preventDefault();for(let i=0;i<9;i++)if(HB[i]==k)HB[i]=-1;HB[hs]=k;sel=k;ui()});g.appendChild(d)})}
function ui(){
if(!creative){for(let i=0;i<9;i++){const k=HB[i];if(k>0){const s=S[k];if((s.k=='b'||s.k=='f')&&!(inv[s.id]>0))HB[i]=-1}}
for(let k=1;k<S.length;k++){const s=S[k];if((s.k=='b'||s.k=='f')&&inv[s.id]>0&&!HB.includes(k)){const j=HB.indexOf(-1);if(j>=0)HB[j]=k}}}
sel=HB[hs]>=0?HB[hs]:0;if(heldSel!=sel)setHeld();
let h='';for(let i=0;i<10;i++)h+=`<i class="${P.hp>=2*i+2?'':P.hp>=2*i+1?'h':'e'}">♥</i>`;$('hp').innerHTML=h;let f='';for(let i=0;i<10;i++)f+=`<i class="${P.food>=2*i+2?'':P.food>=2*i+1?'h':'e'}">🍗</i>`;$('fd').innerHTML=f;
const bs=$('bar').children;for(let i=0;i<9;i++){const k=HB[i],s=S[k>0?k:0],c=s.k=='b'||s.k=='f';fillSlot(bs[i],s,c?(creative?'∞':inv[s.id]):'',i==hs);if(k<=0)bs[i].firstChild.textContent=''}
if($('iv').style.display=='flex')renderGrid()}
ui();
let tt;function tip(m){const t=$('tip');t.textContent=m;t.style.opacity=1;clearTimeout(tt);tt=setTimeout(()=>t.style.opacity=0,1600)}
function hurt(n,why){if(dead||creative)return;P.hp-=n;SF.hurt();$('fx').style.opacity=.5;setTimeout(()=>$('fx').style.opacity=0,120);
if(P.hp<=0){P.hp=0;dead=true;$('dm').textContent=why||"Siz o'ldingiz";$('od').style.display='flex';document.exitPointerLock&&document.exitPointerLock()}ui()}
// mobslar
const mobs=[],drops=[];
const mt={};function mm(hex){if(!mt[hex]){const c=document.createElement('canvas');c.width=c.height=8;const q=c.getContext('2d');for(let i=0;i<8;i++)for(let j=0;j<8;j++){const n=(hash(i+hex%97,j*3+hex%31)-.5)*30;q.fillStyle=`rgb(${((hex>>16)&255)+n|0},${((hex>>8)&255)+n|0},${(hex&255)+n|0})`;q.fillRect(i,j,1,1)}const t=new THREE.CanvasTexture(c);t.magFilter=t.minFilter=THREE.NearestFilter;mt[hex]=new THREE.MeshLambertMaterial({map:t})}return mt[hex].clone()}
function model(t){const g=new THREE.Group(),legs=[],cow=t=='cow';
const bx=(p,w,h,d,x,y,z,co)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),mm(co));m.position.set(x,y,z);p.add(m)};
if(cow){bx(g,.95,.78,1.3,0,.95,0,0x4a3322);bx(g,.97,.42,.45,0,1.05,.3,0xe8e4de);bx(g,.45,.8,.45,-.2,.95,-.2,0xe8e4de);
bx(g,.6,.55,.5,0,1.35,-.85,0x4a3322);bx(g,.4,.25,.12,0,1.22,-1.16,0xd7aaa0);
for(const s of[1,-1]){bx(g,.1,.1,.02,.2*s,1.45,-1.11,0xffffff);bx(g,.05,.05,.02,.2*s,1.45,-1.12,0x111111);bx(g,.1,.18,.1,.34*s,1.68,-.85,0xe9e4c8)}}
else{bx(g,1,.85,1.25,0,1.0,0,0xeeeeea);bx(g,.5,.5,.45,0,1.25,-.8,0xc8a894);bx(g,.54,.2,.5,0,1.57,-.78,0xeeeeea);
for(const s of[1,-1]){bx(g,.12,.08,.2,.3*s,1.35,-.75,0xc8a894);bx(g,.1,.1,.02,.15*s,1.32,-1.03,0xffffff);bx(g,.05,.05,.02,.15*s,1.32,-1.04,0x111111)}}
const lh=cow?.6:.55,lc=cow?0x3a2818:0xc4a08e;
[[.27,.42],[-.27,.42],[.27,-.42],[-.27,-.42]].forEach(([x,z])=>{const l=new THREE.Group();l.position.set(x,lh,z);bx(l,.24,lh,.24,0,-lh/2,0,lc);g.add(l);legs.push(l)});return{g,legs}}
function zmodel(){const g=new THREE.Group(),legs=[];const bx=(p,w,h,d,x,y,z,co)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),mm(co));m.position.set(x,y,z);p.add(m)};
bx(g,.5,.5,.5,0,1.7,0,0x5b8a4a);bx(g,.5,.75,.25,0,1.075,0,0x2e5a9a);bx(g,.1,.1,.02,.12,1.78,-.26,0x111111);bx(g,.1,.1,.02,-.12,1.78,-.26,0x111111);
[.14,-.14].forEach(x=>{const l=new THREE.Group();l.position.set(x,.7,0);bx(l,.24,.7,.24,0,-.35,0,0x2a2a6a);g.add(l);legs.push(l)});
for(const s of[1,-1]){const a=new THREE.Group();a.position.set(.37*s,1.4,0);a.rotation.x=1.5;bx(a,.22,.7,.22,0,-.3,0,0x5b8a4a);g.add(a)}return{g,legs}}
function topY(x,z){for(let y=H-1;y>=0;y--)if(B[ix(x,y,z)])return y;return 0}
function spawnZ(){for(let k=0;k<20;k++){const a=Math.random()*6.28,r=14+Math.random()*12,x=Math.floor(P.x+Math.cos(a)*r),z=Math.floor(P.z+Math.sin(a)*r);if(x<2||z<2||x>=W-2||z>=D-2)continue;const y=topY(x,z)+1;if(get(x,y,z)||get(x,y+1,z)||get(x,y-1,z)==5||LV(x,y,z)>3)continue;
const m=zmodel();scene.add(m.g);mobs.push({t:'zombie',o:m.g,legs:m.legs,x:x+.5,y,z:z+.5,vy:0,hp:20,ang:0,tm:0,go:0,hurt:0,flee:0,kx:0,kz:0,gr:0,cd:1,hw:.3,hh:1.8});return}}
function spawnMob(t){for(let k=0;k<30;k++){const x=2+Math.floor(Math.random()*(W-4)),z=2+Math.floor(Math.random()*(D-4)),y=hm[x][z]+1;if(get(x,y,z)||Math.hypot(x-P.x,z-P.z)<6)continue;
const m=model(t);scene.add(m.g);mobs.push({t,o:m.g,legs:m.legs,x:x+.5,y,z:z+.5,vy:0,hp:t=='cow'?10:8,ang:Math.random()*6.28,tm:0,go:0,hurt:0,flee:0,kx:0,kz:0,gr:0});return}}
for(let i=0;i<7;i++){spawnMob('cow');spawnMob('sheep')}
function dmat(it){return typeof it=='string'?new THREE.MeshLambertMaterial({map:ictex(it),transparent:true,alphaTest:.5,emissive:0x222222}):tm(TL[it][2])}
function drop(x,y,z,it,vx,vz,dl){const m=new THREE.Mesh(new THREE.BoxGeometry(.28,.28,.28),dmat(it));scene.add(m);drops.push({o:m,x,y,z,vy:3,it,vx:vx||0,vz:vz||0,dl:dl||0})}
function dropItem(){if(!on||dead)return;const s=S[sel];if(s.k!='b'&&s.k!='f')return tip("Buni tashlab bo'lmaydi");if(!creative&&!(inv[s.id]>0))return;if(!creative)inv[s.id]--;camera.getWorldDirection(dir);drop(P.x+dir.x*.7,P.y+1.4,P.z+dir.z*.7,s.id,dir.x*6,dir.z*6,1.2);drops[drops.length-1].vy=2+dir.y*5;SF.put(1);ui()}
function hurtMob(m,d){m.hp-=d;m.hurt=.4;SF.hit();SF.mob(m.t,m.hp<=0);const z=m.t=='zombie',a=Math.atan2(m.x-P.x,m.z-P.z);if(!z){m.flee=3;m.ang=a+Math.PI}m.kx=Math.sin(a)*(z?4:7);m.kz=Math.cos(a)*(z?4:7);m.vy=5;m.gr=0;
if(m.hp<=0){scene.remove(m.o);mobs.splice(mobs.indexOf(m),1);if(!z)for(let i=0,n=1+Math.floor(Math.random()*2.99);i<n;i++)drop(m.x+(Math.random()-.5)*.5,m.y+.5,m.z+(Math.random()-.5)*.5,m.t=='cow'?'beef':'mutton')}}
// nishonga olish
const dir=new THREE.Vector3(),eye=new THREE.Vector3();
function aim(){camera.getWorldDirection(dir);eye.copy(camera.position);const r={};let pv=null;
for(let t=0;t<=5;t+=.05){const x=Math.floor(eye.x+dir.x*t),y=Math.floor(eye.y+dir.y*t),z=Math.floor(eye.z+dir.z*t);if(get(x,y,z)){r.b=[x,y,z];r.p=pv;r.t=t;break}pv=[x,y,z]}
let bt=r.t===undefined?9:r.t;for(const m of mobs){const vx=m.x-eye.x,vy=m.y+.65-eye.y,vz=m.z-eye.z,t=vx*dir.x+vy*dir.y+vz*dir.z;if(t<0||t>3.5||t>bt)continue;
const ex=eye.x+dir.x*t-m.x,ey=eye.y+dir.y*t-m.y-.65,ez=eye.z+dir.z*t-m.z;if(ex*ex+ey*ey+ez*ez<.4){bt=t;r.m=m}}return r}
let holding=false,bprog=0,bkey='',bsnd=0;
function btime(id,k){const b={1:.9,2:.8,3:2.2,4:1.4,5:.25,6:.6,7:1.2,8:1.2,9:2.2,10:.6}[id]||1,m=(k=='axe'&&(id==4||id==7||id==8))?4:(k=='pick'&&(id==3||id==9))?4:(k=='shov'&&id<3)?3:((k=='sword'||k=='axe')&&id==5)?3:1;return b/m}
function doBreak(x,y,z){const id=get(x,y,z),s=S[sel];if(y==0)return tip('Bu blok sinmaydi');B[ix(x,y,z)]=0;mpSend({t:'b',x,y,z,v:0});SF.brk(id);
if(!creative){if(id==3){if(s.k=='pick')inv[3]++}else if(id!=5)inv[id]+=(s.k=='shov'&&id<3)?2:1}rebuild();ui()}
function act(){if(!on||dead)return;swing=1;const r=aim(),s=S[sel];
if(r.m){hurtMob(r.m,s.k=='sword'?7:s.k=='axe'?5:s.k=='pick'?3:s.k=='shov'?2:1);return}
if(!r.b)return;if(creative){doBreak(r.b[0],r.b[1],r.b[2]);return}holding=true;bprog=0;bkey=''}
function rel(){holding=false;bprog=0;$('pb').style.display='none'}
function togFly(){P.fly=!P.fly;P.vy=0;document.body.classList.toggle('fly',!!P.fly);tip(P.fly?'Uchish yoqildi':"Uchish o'chdi")}
function sleep(){if(FD>.5)return tip('Faqat kechasi uxlash mumkin');if(mobs.some(m=>m.t=='zombie'&&Math.hypot(m.x-P.x,m.z-P.z)<12))return tip('Yaqin atrofda zombi bor!');
on=false;rel();$('fade').style.opacity=1;setTimeout(()=>{tod=.1;rain=0;rainG=0;rainT=120;$('fade').style.opacity=0;on=true;tip('Xayrli tong!')},1400)}
const FOOD={beef:[2,2],mutton:[2,2],cbeef:[6,6],cmutton:[5,5]};
function eat(k){if(dead)return;if(typeof k!='string')k=S[sel].k=='f'?S[sel].id:['cbeef','cmutton','beef','mutton'].find(q=>inv[q]>0);
if(!k||(!creative&&!(inv[k]>0)))return tip("Ovqat yo'q");if(P.hp>=20&&P.food>=20)return tip("Qorin to'q, jon to'liq");SF.eat();if(!creative)inv[k]--;P.food=Math.min(20,P.food+FOOD[k][0]);P.hp=Math.min(20,P.hp+FOOD[k][1]);ui()}
function place(){if(!on||dead)return;swing=.6;const s=S[sel],r=aim();
if(r.b){const t=get(r.b[0],r.b[1],r.b[2]);if(t==6)return sleep();if(t==8)return openCraft(true);if(t==9)return openFurnace()}
if(s.k=='f')return eat(s.id);if(s.k!='b')return;if(!r.b||!r.p||(!creative&&!(inv[s.id]>0)))return;const[x,y,z]=r.p;
if(x<0||z<0||x>=W||z>=D||y<0||y>=H)return;if(x+1>P.x-.3&&x<P.x+.3&&z+1>P.z-.3&&z<P.z+.3&&y+1>P.y&&y<P.y+1.8)return;
B[ix(x,y,z)]=s.id;mpSend({t:'b',x,y,z,v:s.id});SF.put(s.id);if(!creative)inv[s.id]--;rebuild();ui()}
const hl=new THREE.LineSegments(new THREE.EdgesGeometry(new THREE.BoxGeometry(1.004,1.004,1.004)),new THREE.LineBasicMaterial({color:0x000000}));hl.visible=false;scene.add(hl);
// yangilash
let last=performance.now(),spT=0;
function upd(dt,now){
let mx=(keys.KeyD?1:0)-(keys.KeyA?1:0)+jx,mz=(keys.KeyW?1:0)-(keys.KeyS?1:0)-jy;const l=Math.hypot(mx,mz);if(l>1){mx/=l;mz/=l}
const c=Math.cos(yaw),s=Math.sin(yaw),sp=4.3;
if(creative&&P.fly){P.vy=(keys.Space||jh)?6:(keys.ShiftLeft||dn)?-6:0}else{P.vy=Math.max(P.vy-25*dt,-40);if((keys.Space||jh)&&P.ground)P.vy=8.2}
const r=move(P,(c*mx-s*mz)*sp*dt,P.vy*dt,(-s*mx-c*mz)*sp*dt,.3,1.8);
if(r.y<0){if(P.fly){P.fly=0;document.body.classList.remove("fly")}const d=Math.floor(P.fs-P.y+.05);P.vy=0;P.ground=1;P.fs=P.y;if(d>=4)hurt(2*Math.floor(d/4),"Baland joydan yiqilib o'ldingiz")}
else{if(r.y>0)P.vy=0;P.ground=0;P.fs=Math.max(P.fs,P.y)}
if(P.ground&&(mx||mz)){P.sd=(P.sd||0)+dt;if(P.sd>.42){P.sd=0;SF.step(get(Math.floor(P.x),Math.floor(P.y)-1,Math.floor(P.z)))}}
P.ft+=dt;if(P.ft>25){P.ft=0;if(P.food>0){P.food--;ui()}}
P.rg+=dt;if(P.rg>6){P.rg=0;if(P.food>=6&&P.hp<20){P.hp++;ui()}else if(P.food<=0&&P.hp>2)hurt(1,"Ochlikdan o'ldingiz")}
camera.position.set(P.x,P.y+1.62,P.z);camera.rotation.set(pitch,yaw,0);sky.position.copy(camera.position);for(const cl of clouds){cl.position.x+=dt*1.5;if(cl.position.x>140)cl.position.x-=180}
for(const m of mobs){if(m.flee<=0){m.tm-=dt;if(m.tm<=0){m.tm=2+Math.random()*4;m.ang=Math.random()*6.28;m.go=Math.random()<.6?1:0}}
m.hurt-=dt;m.flee-=dt;if(Math.random()<dt*.03&&Math.hypot(m.x-P.x,m.z-P.z)<14)SF.mob(m.t,0,.5);let v=m.flee>0?3:m.go?1:0;
if(m.t=='zombie'){const dx=P.x-m.x,dz=P.z-m.z,dd=Math.hypot(dx,dz);m.cd-=dt;if(dd<24&&!dead){m.ang=Math.atan2(-dx,-dz);v=dd>.9?2.4:0;if(dd<1.3&&Math.abs(P.y-m.y)<1.6&&m.cd<=0){m.cd=1;hurt(2,"Zombi sizni o'ldirdi")}}else v=m.go?.8:0;
if(FD>.55){m.hp-=5*dt;m.burn=1;if(m.hp<=0&&!m.rm){m.rm=1;SF.mob('zombie',1)}}else m.burn=0}
m.vy=Math.max(m.vy-25*dt,-40);const q=move(m,(-Math.sin(m.ang)*v+m.kx)*dt,m.vy*dt,(-Math.cos(m.ang)*v+m.kz)*dt,m.hw||.4,m.hh||1.2);
m.kx*=Math.pow(.003,dt);m.kz*=Math.pow(.003,dt);if(q.y){m.gr=q.y<0;m.vy=0}else m.gr=0;if((q.x||q.z)&&m.gr)m.vy=7.5;
m.o.position.set(m.x,m.y,m.z);m.o.rotation.y=m.ang;const w=v?Math.sin(now*.012)*.6:0;m.legs.forEach((g,i)=>g.rotation.x=i%2?-w:w);
const e=m.hurt>0?0x990000:m.burn?(Math.random()<.5?0xff6600:0xaa2200):0;m.o.traverse(o=>{if(o.material)o.material.emissive.setHex(e)})}
for(let i=drops.length-1;i>=0;i--){const d=drops[i];d.dl-=dt;d.vy-=25*dt;const q=move(d,d.vx*dt,d.vy*dt,d.vz*dt,.12,.28);if(q.y){d.vy=0;d.vx*=.8;d.vz*=.8}if(q.x)d.vx=0;if(q.z)d.vz=0;d.o.position.set(d.x,d.y+.2+Math.sin(now*.004+i)*.05,d.z);d.o.rotation.y+=dt*2;
if(d.dl<=0&&Math.hypot(d.x-P.x,d.z-P.z)<1.5&&Math.abs(d.y-P.y-.8)<1.8){scene.remove(d.o);drops.splice(i,1);if(!creative)inv[d.it]=(inv[d.it]||0)+1;SF.pop();ui();tip('+1 '+S.find(q=>q.id===d.it).n)}}
spT+=dt;if(spT>15){spT=0;if(mobs.filter(q=>q.t!='zombie').length<12)spawnMob(Math.random()<.5?'cow':'sheep')}
const a=aim();if(a.b&&!a.m){hl.visible=true;hl.position.set(a.b[0]+.5,a.b[1]+.5,a.b[2]+.5)}else hl.visible=false;
if(holding){if(a.b&&!a.m){const k=a.b.join();if(k!=bkey){bkey=k;bprog=0}const id=get(a.b[0],a.b[1],a.b[2]);bprog+=dt/btime(id,S[sel].k);bsnd-=dt;if(bsnd<=0){bsnd=.22;SF.tick(id)}$('pb').style.display='block';$('pb').firstChild.style.width=Math.min(100,bprog*100)+'%';if(bprog>=1){doBreak(a.b[0],a.b[1],a.b[2]);bprog=0;bkey=''}}else{bprog=0;bkey='';$('pb').style.display='none'}}
if(!creative&&FD<.3){zt-=dt;if(zt<=0){zt=3+Math.random()*4;if(mobs.filter(q=>q.t=='zombie').length<6)spawnZ()}}
for(let i=mobs.length-1;i>=0;i--)if(mobs[i].rm){scene.remove(mobs[i].o);mobs.splice(i,1)}
if(creative&&(P.food<20||P.hp<20)){P.food=20;P.hp=20;ui()}}
function loop(now){requestAnimationFrame(loop);const dt=Math.min((now-last)/1e3,.05);last=now;env(dt);mpTick(dt,now);const mn=!on&&!dead&&$('iv').style.display!='flex'&&$('os').style.display!='none';document.body.classList.toggle('m',mn);if(on&&!dead)upd(dt,now);else if(mn){const a=now*.00008;camera.position.set(32+Math.cos(a)*34,26,32+Math.sin(a)*34);camera.lookAt(32,9,32);sky.position.copy(camera.position)}swing=Math.max(0,swing-dt*4);if(held)held.rotation.x=-.25-Math.sin(swing*Math.PI)*1.1;renderer.autoClear=false;renderer.clear();renderer.render(scene,camera);if(!mn){renderer.clearDepth();renderer.render(handScene,handCam)}}
requestAnimationFrame(loop);
// boshqaruv
function lock(){if(!T)$('cv').requestPointerLock();else{try{const e=document.documentElement;if(e.requestFullscreen)e.requestFullscreen().then(()=>{try{screen.orientation.lock('landscape').catch(()=>{})}catch(x){}}).catch(()=>{})}catch(x){}}}
let AC,mg;function au(){if(!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)();mg=AC.createGain();mg.gain.value=ST.snd?.5:0;mg.connect(AC.destination)}catch(e){}}if(AC&&AC.state=='suspended')AC.resume()}
addEventListener('pointerdown',au);addEventListener('keydown',au);
function tone(f0,f1,d,v,w,lp){const a=AC;if(!a)return;const o=a.createOscillator(),g=a.createGain(),t=a.currentTime;o.type=w||'sine';o.frequency.setValueAtTime(f0,t);o.frequency.exponentialRampToValueAtTime(Math.max(20,f1),t+d);g.gain.setValueAtTime(v,t);g.gain.exponentialRampToValueAtTime(.001,t+d);let n=o;if(lp){const f=a.createBiquadFilter();f.type='lowpass';f.frequency.value=lp;o.connect(f);n=f}n.connect(g);g.connect(mg);o.start(t);o.stop(t+d)}
function nz(d,f,q,v,type){const a=AC;if(!a)return;const n=Math.floor(a.sampleRate*d),b=a.createBuffer(1,n,a.sampleRate),x=b.getChannelData(0);for(let i=0;i<n;i++)x[i]=Math.random()*2-1;const s=a.createBufferSource(),fl=a.createBiquadFilter(),g=a.createGain(),t=a.currentTime;s.buffer=b;fl.type=type||'bandpass';fl.frequency.value=f;fl.Q.value=q;g.gain.setValueAtTime(v,t);g.gain.exponentialRampToValueAtTime(.001,t+d);s.connect(fl);fl.connect(g);g.connect(mg);s.start(t)}
const SF={
brk(id){if(id==3){nz(.18,1800,1,.9);tone(180,90,.12,.4,'square',500)}else if(id==4){nz(.15,900,2,.6);tone(220,120,.12,.5,'triangle')}else if(id==5)nz(.2,3000,.7,.35,'highpass');else{nz(.16,500,.8,.8,'lowpass');tone(110,60,.12,.5)}},
put(id){tone(id==3?200:130,70,.09,.5,'triangle');nz(.07,id==3?1500:600,1,.35)},
hurt(){tone(320,110,.28,.5,'sawtooth',900);nz(.12,700,1,.4)},
hit(){nz(.08,1100,1,.5);tone(150,80,.08,.35,'square',600)},
mob(t,die,v){v=v||1;if(t=='zombie'){tone(die?90:120,die?40:80,.5,.4*v,'sawtooth',300);return}if(t=='cow'){tone(die?170:190,die?60:140,die?.7:.5,.35*v,'sawtooth',450)}else{tone(die?380:420,die?150:350,die?.6:.45,.3*v,'sawtooth',800);tone(die?388:428,die?155:356,die?.6:.45,.2*v,'sawtooth',800)}},
eat(){[0,110,220].forEach(d=>setTimeout(()=>nz(.06,1200,1.5,.5),d))},
pop(){tone(500,1000,.1,.3)},
tick(id){nz(.05,id==3?1500:500,1,.25,id==3?'bandpass':'lowpass')},
step(id){id==3?nz(.05,1200,1,.12):nz(.06,400,1,.14,'lowpass')}};
const EL=['bj','bd','bk','bp','jr','bi','bar','bf','bq'];let LAY={},ed=false,dr=null,edFrom='os';
try{LAY=JSON.parse(localStorage.getItem('mclay')||'{}')}catch(e){}
let SZ={},selEl=null;try{SZ=JSON.parse(localStorage.getItem('mcsz')||'{}')}catch(e){}
function applySz(){for(const id of EL){const e=$(id);if(SZ[id]){e.style.transformOrigin='0 0';e.style.scale=SZ[id]}}}
function selectEl(id){selEl=id;EL.forEach(i=>$(i).classList.toggle('sel',i==id));$('edsz').value=Math.round((SZ[id]||1)*100);$('edszv').textContent=$('edsz').value+'%'}
function selAll(){selEl=null;EL.forEach(i=>$(i).classList.remove('sel'));$('edsz').value=100;$('edszv').textContent='100%'}
function applyLay(){for(const id of EL){const p=LAY[id],e=$(id);if(!p)continue;const sc=SZ[id]||1,w=(e.offsetWidth||60)*sc,h=(e.offsetHeight||60)*sc;e.style.left=Math.max(0,Math.min(VW()-w,p[0]*VW()))+'px';e.style.top=Math.max(0,Math.min(VH()-h,p[1]*VH()))+'px';e.style.right=e.style.bottom='auto';e.style.transform='none'}}
applySz();applyLay();addEventListener('resize',applyLay);
EL.forEach(id=>{const e=$(id);e.addEventListener('pointerdown',ev=>{if(!ed)return;ev.preventDefault();selectEl(id);const r=crect(e),q=TP(ev.clientX,ev.clientY);dr={e,id,dx:q[0]-r.left,dy:q[1]-r.top};try{e.setPointerCapture(ev.pointerId)}catch(x){}})});
document.addEventListener('pointermove',ev=>{if(!dr)return;const e=dr.e,q=TP(ev.clientX,ev.clientY),x=Math.max(0,Math.min(VW()-e.offsetWidth*(SZ[dr.id]||1),q[0]-dr.dx)),y=Math.max(0,Math.min(VH()-e.offsetHeight*(SZ[dr.id]||1),q[1]-dr.dy));e.style.left=x+'px';e.style.top=y+'px';e.style.right=e.style.bottom='auto';e.style.transform='none';LAY[dr.id]=[x/VW(),y/VH()]});
const dre=()=>{if(dr){dr=null;try{localStorage.setItem('mclay',JSON.stringify(LAY))}catch(e){}}};document.addEventListener('pointerup',dre);document.addEventListener('pointercancel',dre);
function edOn(from){selAll();ed=true;edFrom=from;on=false;rel();document.body.classList.add('ed');$(from).style.display='none';document.exitPointerLock&&document.exitPointerLock()}
function edOff(){ed=false;document.body.classList.remove('ed');$(edFrom).style.display='flex'}
$('ed').onclick=()=>{$('st').style.display='none';edOn('os')};$('ed2').onclick=()=>edOn('iv');$('edok').onclick=edOff;
$('edrs').onclick=()=>{LAY={};SZ={};try{localStorage.removeItem('mclay');localStorage.removeItem('mcsz')}catch(e){}for(const id of EL){const e=$(id);e.style.left=e.style.top=e.style.right=e.style.bottom=e.style.transform=e.style.scale=e.style.transformOrigin=''}selAll()};
$('edsz').oninput=()=>{const v=$('edsz').value/100;if(selEl)SZ[selEl]=v;else EL.forEach(id=>SZ[id]=v);$('edszv').textContent=$('edsz').value+'%';applySz();try{localStorage.setItem('mcsz',JSON.stringify(SZ))}catch(e){}};
$('edall').onclick=selAll;
const SP=["Sigirni ur!","Go'sht yeysan!","4 blokdan sakrama!","Kirka olib kel!","Qo'yni qidir!"];$('spl').textContent=SP[Math.floor(Math.random()*SP.length)];
$('hb').onclick=()=>$('hlp').style.display='block';$('hlp').onclick=()=>$('hlp').style.display='none';

const LS={get(k){try{return localStorage.getItem(k)}catch(e){return null}},set(k,v){try{localStorage.setItem(k,v);return true}catch(e){return false}},del(k){try{localStorage.removeItem(k)}catch(e){}}};
let WL=[];try{WL=JSON.parse(LS.get('mcw_list')||'[]')}catch(e){}
let curW=null;const saveList=()=>LS.set('mcw_list',JSON.stringify(WL));
function clearEnts(){for(const m of mobs)scene.remove(m.o);mobs.length=0;for(const d of drops)scene.remove(d.o);drops.length=0}
function calcHm(){for(let x=0;x<W;x++){hm[x]=hm[x]||[];for(let z=0;z<D;z++){let y=H-1;while(y>0){const v=B[ix(x,y,z)];if(v>=1&&v<=3)break;y--}hm[x][z]=y}}}
function rle(){const o=[];let v=B[0],c=0;for(let i=0;i<B.length;i++){if(B[i]==v)c++;else{o.push(v,c);v=B[i];c=1}}o.push(v,c);return o}
function unrle(a){let p=0;for(let i=0;i<a.length;i+=2){B.fill(a[i],p,p+a[i+1]);p+=a[i+1]}}
function saveWorld(){if(!curW)return;const w=WL.find(q=>q.id==curW);if(!w)return;w.t=Date.now();LS.set('mcw_'+curW,JSON.stringify({b:rle(),p:[P.x,P.y,P.z,yaw,pitch,P.hp,P.food],inv,hb:HB,hs,tod}));saveList()}
function enterWorld(id){const w=WL.find(q=>q.id==id);if(!w)return;let d=null;try{d=JSON.parse(LS.get('mcw_'+id)||'null')}catch(e){}
clearEnts();creative=!!w.creative;P.fly=0;document.body.classList.remove('fly');
if(d){unrle(d.b);calcHm();genPl();newInv(creative);Object.assign(inv,d.inv);HB=d.hb;hs=d.hs;tod=d.tod;[P.x,P.y,P.z,yaw,pitch,P.hp,P.food]=d.p;P.vy=0;P.fs=P.y}
else{gen(w.seed);genPl();newInv(creative);spawn();tod=.2}
rebuild();curW=id;lanHostStart(w);if(hasLan())window.Android.lanScan(0);for(let i=0;i<7;i++){spawnMob('cow');spawnMob('sheep')}
rain=0;rainG=0;dead=false;on=true;$('od').style.display='none';$('os').style.display='none';$('wl').style.display='none';$('nw').style.display='none';lock();au();ui();saveWorld()}
function exitWorld(){saveWorld();mpClose();on=false;rel();$('iv').style.display='none';$('os').style.display='flex';$('cont').style.display=curW?'block':'none'}
$('cont').onclick=()=>{on=true;$('os').style.display='none';lock();au()};$('ex').onclick=exitWorld;
const fmtSz=n=>n>1048576?(n/1048576).toFixed(1)+' MB':Math.max(1,Math.round(n/1024))+' KB';
const fmtD=t=>{const d=new Date(t);return d.toDateString()==new Date().toDateString()?'Bugun':d.toLocaleDateString()};
function renderWorlds(){const l=$('wll');l.innerHTML='';
if(hasLan()&&LANL.length){const h=document.createElement('p');h.className='emp';h.textContent="Do'stlar (shu Wi-Fi)";l.appendChild(h);LANL.forEach(x=>{const r=document.createElement('div');r.className='wr2';const m=document.createElement('div');m.className='wm';m.innerHTML='<b></b><small></small><i></i>';m.children[0].textContent=x.n;m.children[1].textContent=(x.h||"Do'st")+' · LAN';m.children[2].textContent="Qo'shilish";m.onclick=()=>{tip('Ulanmoqda...');window.Android.lanJoin(x.ip,x.p)};r.appendChild(m);l.appendChild(r)})}
if(!WL.length)l.innerHTML="<p class='emp'>Hali dunyo yo'q. Yuqoridagi «Yangi» tugmasini bosing.</p>";
WL.slice().sort((a,b)=>b.t-a.t).forEach(w=>{const r=document.createElement('div');r.className='wr2';
const m=document.createElement('div');m.className='wm';m.innerHTML='<b></b><small></small><i></i>';m.children[0].textContent=w.name;m.children[1].textContent=(w.creative?'Creative':'Survival')+'   '+fmtD(w.t);m.children[2].textContent=fmtSz((LS.get('mcw_'+w.id)||'').length);m.onclick=()=>enterWorld(w.id);
const pe=document.createElement('button');pe.className='pe';pe.textContent='✎';pe.onclick=()=>r.classList.toggle('open');
const tp=document.createElement('div');tp.className='wt';tp.append(m,pe);
const ex=document.createElement('div');ex.className='wx';const inp=document.createElement('input');inp.value=w.name;inp.maxLength=20;
const sv=document.createElement('button');sv.textContent='Saqlash';sv.onclick=()=>{const v=inp.value.trim();if(v){w.name=v;saveList();renderWorlds()}};
const d=document.createElement('button');d.textContent="O'chirish";let arm=0;d.onclick=()=>{if(!arm){arm=1;d.textContent='Aniqmi?';setTimeout(()=>{arm=0;d.textContent="O'chirish"},2500);return}WL=WL.filter(q=>q.id!=w.id);LS.del('mcw_'+w.id);saveList();if(curW==w.id)curW=null;renderWorlds()};
ex.append(inp,sv,d);r.append(tp,ex);l.appendChild(r)})}
$('go').onclick=()=>{renderWorlds();$('wl').style.display='flex';if(hasLan())window.Android.lanScan(1)};$('wlx').onclick=()=>{$('wl').style.display='none';if(hasLan())window.Android.lanScan(0)};
let nmode=0;
function setNM(c){nmode=c;$('nms').classList.toggle('sel',!c);$('nmc').classList.toggle('sel',!!c);$('nwd').textContent=c?"Cheksiz resurslar. Jon ketmaydi. Uchish mumkin.":"Resurslarni yig'ing, ovqat yeng, kechasi zombilardan saqlaning."}
function mkW(){const nm=($('wn').value||'').trim()||('Dunyo '+(WL.length+1));const sd=parseInt($('wsd').value)||(1+Math.floor(Math.random()*99999));const w={id:Date.now().toString(36),name:nm,creative:!!nmode,seed:Math.abs(sd)%1000000,t:Date.now()};WL.push(w);saveList();$('nw').style.display='none';enterWorld(w.id)}
$('wnew').onclick=()=>{$('wn').value='Mening dunyom';$('wsd').value='';setNM(0);$('nw').style.display='flex'};$('nwx').onclick=()=>$('nw').style.display='none';$('nwa').onclick=()=>{const e=$('wsd');e.style.display=e.style.display=='none'?'':'none'};$('nms').onclick=()=>setNM(0);$('nmc').onclick=()=>setNM(1);$('nwc').onclick=mkW;setNM(0);
setInterval(()=>{if(curW&&on&&!dead)saveWorld()},15000);addEventListener('pagehide',saveWorld);document.addEventListener('visibilitychange',()=>{if(document.hidden)saveWorld()});
let ST={name:'',fog:1,snd:1};try{ST=Object.assign(ST,JSON.parse(LS.get('mcset')||'{}'))}catch(e){}
const FOGS=[[18,45],[30,85],[50,130]],FN=['Yaqin',"O'rta",'Uzoq'];
function applyST(){const q=FOGS[ST.fog];scene.fog.near=q[0];scene.fog.far=q[1];$('sf').textContent="Ko'rinish: "+FN[ST.fog];$('ss').textContent='Ovoz: '+(ST.snd?'yoqilgan':"o'chiq");if(mg)mg.gain.value=ST.snd?.5:0}applyST();
$('op').onclick=()=>{$('sn').value=ST.name;const w=WL.find(q=>q.id==curW);$('sw').value=w?w.name:'';$('sw').disabled=!w;$('st').style.display='flex'};
$('sf').onclick=()=>{ST.fog=(ST.fog+1)%3;applyST()};$('ss').onclick=()=>{ST.snd=ST.snd?0:1;applyST()};
$('sx').onclick=()=>{ST.name=$('sn').value.trim();const w=WL.find(q=>q.id==curW),v=$('sw').value.trim();if(w&&v){w.name=v;saveList()}LS.set('mcset',JSON.stringify(ST));$('st').style.display='none'};
const mp={lan:false,host:false,parts:[],hd:null,rm:null,name:'',tx:0,ty:0,tz:0,tr:0,dirty:0,dt:0,tm:0,n:0};
const hasLan=()=>!!(window.Android&&window.Android.lanHost);
const mpSend=o=>{if(mp.lan&&hasLan())window.Android.lanSend(JSON.stringify(o))};
function pmodel(name){const g=new THREE.Group(),bx=(w,h,d,x,y,z,co)=>{const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),mm(co));m.position.set(x,y,z);g.add(m)};
bx(.5,.5,.5,0,1.7,0,0xc89a76);bx(.5,.75,.25,0,1.075,0,0x2a8a4a);bx(.24,.7,.24,.14,.35,0,0x2a3a7a);bx(.24,.7,.24,-.14,.35,0,0x2a3a7a);bx(.22,.7,.22,.37,1.05,0,0xc89a76);bx(.22,.7,.22,-.37,1.05,0,0xc89a76);bx(.1,.1,.02,.12,1.75,-.26,0x111111);bx(.1,.1,.02,-.12,1.75,-.26,0x111111);
const c=document.createElement('canvas');c.width=256;c.height=48;const q=c.getContext('2d');q.font='bold 28px sans-serif';q.textAlign='center';q.fillStyle='rgba(0,0,0,.5)';q.fillRect(0,0,256,48);q.fillStyle='#fff';q.fillText(name,128,34);
const sp=new THREE.Sprite(new THREE.SpriteMaterial({map:new THREE.CanvasTexture(c),fog:false,depthTest:false}));sp.scale.set(1.6,.3,1);sp.position.y=2.3;g.add(sp);return g}
function mpDrop(){if(mp.rm){scene.remove(mp.rm);mp.rm=null}}
function mpLeft(){const was=mp.lan;mp.lan=false;mpDrop();if(was)tip("Do'st chiqib ketdi")}
function mpClose(){if(hasLan())window.Android.lanStop();mp.lan=false;mpDrop()}
function lanHostStart(w){if(hasLan())window.Android.lanHost(JSON.stringify({n:w.name,h:ST.name||"O'yinchi"}))}
function sendWorld(){const s=JSON.stringify(rle()),n=Math.ceil(s.length/12000);mpSend({t:'wh',n,tod,creative,x:P.x,y:P.y,z:P.z});for(let i=0;i<n;i++)mpSend({t:'wc',d:s.slice(i*12000,(i+1)*12000)})}
function joinWorld(){const hd=mp.hd;unrle(JSON.parse(mp.parts.join('')));calcHm();genPl();clearEnts();creative=!!hd.creative;P.fly=0;newInv(creative);tod=hd.tod;curW=null;P.x=hd.x+1.5;P.y=hd.y;P.z=hd.z;P.vy=0;P.fs=P.y;P.hp=20;P.food=20;rebuild();
for(let i=0;i<5;i++){spawnMob('cow');spawnMob('sheep')}dead=false;on=true;['os','wl','iv'].forEach(i=>$(i).style.display='none');if(hasLan())window.Android.lanScan(0);lock();au();ui();tip("Do'st dunyosiga qo'shildingiz")}
function mpRecv(m){
if(m.t=='n'){mp.name=m.name;mpDrop();mp.rm=pmodel(mp.name||"Do'st");scene.add(mp.rm)}
else if(m.t=='p'){mp.tx=m.x;mp.ty=m.y;mp.tz=m.z;mp.tr=m.r;if(!mp.rm){mp.rm=pmodel(mp.name||"Do'st");scene.add(mp.rm);mp.rm.position.set(m.x,m.y,m.z)}}
else if(m.t=='b'){if(m.y>=0&&m.y<H&&m.x>=0&&m.x<W&&m.z>=0&&m.z<D){B[ix(m.x,m.y,m.z)]=m.v;mp.dirty=1}}
else if(m.t=='t'){tod=m.tod}
else if(m.t=='wh'){mp.hd=m;mp.parts=[]}
else if(m.t=='wc'){mp.parts.push(m.d);if(mp.hd&&mp.parts.length==mp.hd.n)joinWorld()}}
window.onLanOpen=role=>{mp.lan=true;mp.host=role=='host';mpSend({t:'n',name:ST.name||(mp.host?'Host':'Mehmon')});if(mp.host){sendWorld();tip("Do'st qo'shildi!")}else tip("Ulandi, dunyo yuklanmoqda...")};
window.onLanMsg=x=>{try{mpRecv(JSON.parse(x))}catch(e){}};
window.onLanClose=()=>mpLeft();window.onLanErr=()=>tip("Ulanib bo'lmadi");
let LANL=[];window.onLan=a=>{if(JSON.stringify(a)==JSON.stringify(LANL))return;LANL=a;if($('wl').style.display=='flex')renderWorlds()};
function mpTick(dt,now){if(mp.rm){const k=Math.min(1,dt*12),p=mp.rm.position;p.x+=(mp.tx-p.x)*k;p.y+=(mp.ty-p.y)*k;p.z+=(mp.tz-p.z)*k;mp.rm.rotation.y=mp.tr}
if(mp.dirty){mp.dt-=dt;if(mp.dt<=0){rebuild();mp.dirty=0;mp.dt=.1}}
if(mp.lan){mp.tm+=dt;if(mp.tm>.1&&on&&!dead){mp.tm=0;mpSend({t:'p',x:P.x,y:P.y,z:P.z,r:yaw});mp.n++;if(mp.host&&mp.n%50==0)mpSend({t:'t',tod})}}}
const APPVER='__VER__',APPREPO='__REPO__';let upURL='',upWas=false;
const isApp=()=>!!window.Android&&/^\d+$/.test(APPVER);

async function chkUpd(manual){if(!isApp()){if(manual)tip('Yangilash faqat ilovada ishlaydi');return}
try{const r=await fetch('https://api.github.com/repos/'+APPREPO+'/releases/latest'),j=await r.json(),v=parseInt(String(j.tag_name||'').replace(/\D/g,'')),a=(j.assets||[]).find(x=>/\.apk$/i.test(x.name));
if(a&&v>+APPVER){upURL=a.browser_download_url;$('upt').textContent='Yangi yangilanish bor (№'+v+', sizda №'+APPVER+'). Yangilaymizmi?';upWas=on;on=false;rel();$('upb').style.width='0';$('up').style.display='flex'}
else if(manual)tip("Yangilanish yo'q — eng so'nggi versiya")}catch(e){if(manual)tip("Tekshirib bo'lmadi (internet bormi?)")}}
window.onUpd=p=>{$('upb').style.width=p+'%';$('upt').textContent='Yuklanmoqda... '+p+'%'};
window.onUpdErr=m=>{$('upt').textContent=m=='perm'?"O'rnatishga ruxsat bering, keyin «Yangilash» ni yana bosing":'Xatolik: '+m};
$('upg').onclick=()=>{$('upt').textContent='Yuklanmoqda...';window.Android.install(upURL)};
$('upl').onclick=()=>{$('up').style.display='none';on=upWas};
$('sup').onclick=()=>{$('st').style.display='none';chkUpd(true)};
setTimeout(chkUpd,3000);setInterval(chkUpd,1800000);
const REC=[{n:'Taxta ×4',r:[4,7],c:{4:1},h:1},{n:'Kraft stoli',r:[1,8],c:{7:4},h:1},{n:'Chiroq',r:[1,10],c:{7:2,3:2},h:1},{n:'Pechka',r:[1,9],c:{3:8}},{n:'Yotoq',r:[1,6],c:{7:6}}];
let crFull=false;const nmOf=k=>S.find(s=>s.id==k).n;
function pnl(id,o){$(id).style.display=o?'flex':'none';if(o){on=false;rel();document.exitPointerLock&&document.exitPointerLock()}else{on=true;lock()}}
const can=c=>creative||Object.keys(c).every(k=>inv[k]>=c[k]);
function renderCraft(){const l=$('crl');l.innerHTML='';REC.forEach(q=>{if(!crFull&&!q.h)return;const b=document.createElement('button');b.className='rc';b.textContent=q.n+' ← '+Object.keys(q.c).map(k=>q.c[k]+' '+nmOf(k)).join(' + ');b.disabled=!can(q.c);
b.onclick=()=>{if(!can(q.c))return;if(!creative)for(const k in q.c)inv[k]-=q.c[k];inv[q.r[1]]+=q.r[0];SF.put(7);ui();renderCraft();tip('Yasaldi: '+q.n)};l.appendChild(b)})}
function openCraft(f){crFull=f;$('crt').textContent=f?'Kraft stoli':'Yasash';renderCraft();pnl('cr',1)}
$('crx').onclick=()=>pnl('cr',0);$('cr2').onclick=()=>{$('iv').style.display='none';openCraft(false)};
let fuel=0,cook=null;const fuelOk=()=>creative||fuel>0||inv[7]>0||inv[4]>0;
function startCook(raw,out){if(cook)return;if(!creative&&!(inv[raw]>0))return;if(!fuelOk())return tip("Yoqilg'i kerak: yog'och yoki taxta");
if(!creative){if(fuel<=0){if(inv[7]>0){inv[7]--;fuel=1}else{inv[4]--;fuel=2}}fuel--;inv[raw]--}cook={out,t:0};SF.put(3);ui();renderF()}
function renderF(){const l=$('ful');l.innerHTML='';[['beef','cbeef',"Mol go'shtini pishirish"],['mutton','cmutton',"Qo'y go'shtini pishirish"]].forEach(([a,o,n])=>{const b=document.createElement('button');b.className='rc';b.textContent=n+' ('+(creative?'∞':inv[a])+')';b.disabled=!!cook||(!creative&&!(inv[a]>0))||!fuelOk();b.onclick=()=>startCook(a,o);l.appendChild(b)});
$('fup').textContent=cook?'Pishyapti...':"Yoqilg'i: yog'och yoki taxta ("+(creative?'∞':fuel+inv[4]*2+inv[7])+")"}
function openFurnace(){renderF();pnl('fu',1)}$('fux').onclick=()=>pnl('fu',0);
setInterval(()=>{if(!cook)return;cook.t+=.1;$('fub').style.width=Math.min(100,cook.t/3*100)+'%';if(cook.t>=3){inv[cook.out]=(inv[cook.out]||0)+1;cook=null;$('fub').style.width='0';SF.pop();ui();renderF();tip('Pishdi!')}},100);
$('rs').onclick=()=>{spawn();dead=false;on=true;$('od').style.display='none';ui();lock()};
function togInv(){if(dead)return;if($('iv').style.display=='flex'){$('iv').style.display='none';on=true;lock()}else if(on){on=false;$('iv').style.display='flex';document.exitPointerLock&&document.exitPointerLock();ui()}}
$('bi').onclick=togInv;$('ic').onclick=togInv;$('ie').onclick=eat;
document.addEventListener('pointerlockchange',()=>{if(!T&&on&&!dead&&document.pointerLockElement!=$('cv')){on=false;$('cont').style.display='block';$('os').style.display='flex'}});
document.addEventListener('mousemove',e=>{if(document.pointerLockElement==$('cv')){yaw-=e.movementX*.0025;pitch=Math.max(-1.55,Math.min(1.55,pitch-e.movementY*.0025))}});
document.addEventListener('mousedown',e=>{if(document.pointerLockElement!=$('cv'))return;if(e.button==0)act();else if(e.button==2)place()});
addEventListener('contextmenu',e=>e.preventDefault());document.addEventListener('mouseup',e=>{if(e.button==0)rel()});
addEventListener('keydown',e=>{keys[e.code]=true;if(e.code=='Space'){e.preventDefault();if(!e.repeat){const t=performance.now();if(creative&&t-lastJ<300)togFly();lastJ=t}}if(e.code=='KeyE')eat();if(e.code=='KeyI')togInv();const n=+e.code.replace('Digit','');if(n>=1&&n<=9)pickSlot(n-1);if(e.code=='KeyQ')dropItem();if(e.code=='KeyF')togFon();});
addEventListener('keyup',e=>keys[e.code]=false);
const btn=(id,dn,up)=>{const e=$(id);e.addEventListener('pointerdown',ev=>{ev.preventDefault();if(document.body.classList.contains('ed'))return;dn()});if(up){e.addEventListener('pointerup',up);e.addEventListener('pointercancel',up);e.addEventListener('pointerleave',up)}};
btn('bj',()=>{jh=true;const t=performance.now();if(creative&&t-lastJ<300)togFly();lastJ=t},()=>jh=false);btn('bd',()=>dn=true,()=>dn=false);btn('bk',act,rel);btn('bp',place);btn('bf',togFon);btn('bq',dropItem);
let js=null,lk=null;const cv=$('cv');
cv.addEventListener('touchstart',e=>{e.preventDefault();for(const t of e.changedTouches){const rc=$('jr').getBoundingClientRect(),cx=rc.left+rc.width/2,cy=rc.top+rc.height/2;if(!js&&Math.hypot(t.clientX-cx,t.clientY-cy)<85){js={id:t.identifier,x:cx,y:cy}}else if(!lk)lk={id:t.identifier,x:t.clientX,y:t.clientY}}},{passive:false});
cv.addEventListener('touchmove',e=>{e.preventDefault();for(const t of e.changedTouches){if(js&&t.identifier==js.id){let ddx=t.clientX-js.x,ddy=t.clientY-js.y;if(ROTV){const tt=ddx;ddx=ddy;ddy=-tt}let a=ddx/48,b=ddy/48;const l=Math.hypot(a,b);if(l>1){a/=l;b/=l}jx=Math.abs(a)>.15?a:0;jy=Math.abs(b)>.15?b:0;$('jk').style.transform=`translate(${a*30}px,${b*30}px)`}
else if(lk&&t.identifier==lk.id){let lx=t.clientX-lk.x,ly=t.clientY-lk.y;if(ROTV){const tt=lx;lx=ly;ly=-tt}yaw-=lx*.006;pitch=Math.max(-1.55,Math.min(1.55,pitch-ly*.006));lk.x=t.clientX;lk.y=t.clientY}}},{passive:false});
const te=e=>{for(const t of e.changedTouches){if(js&&t.identifier==js.id){js=null;jx=jy=0;$('jk').style.transform=''}if(lk&&t.identifier==lk.id)lk=null}};
cv.addEventListener('touchend',te);cv.addEventListener('touchcancel',te);
</script></body></html>
# Minecraft
