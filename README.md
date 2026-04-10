<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1">
<title>✦ RAUPATU ✦</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
html,body{height:100%;background:#0e2d0e;}
body{font-family:Georgia,serif;color:#fef3c7;user-select:none;display:flex;flex-direction:column;min-height:100%;overflow-x:hidden;}

/* Felt texture */
body::before{content:'';position:fixed;inset:0;pointer-events:none;z-index:0;
  background:radial-gradient(ellipse at 50% 40%,#1c4f1c,#0e2d0e 60%,#061406);
  background-image:radial-gradient(ellipse at 50% 40%,#1c4f1c,#0e2d0e 60%,#061406),
    repeating-linear-gradient(0deg,rgba(255,255,255,.006) 0,rgba(255,255,255,.006) 1px,transparent 1px,transparent 10px),
    repeating-linear-gradient(90deg,rgba(255,255,255,.006) 0,rgba(255,255,255,.006) 1px,transparent 1px,transparent 10px);}

/* Kōwhaiwhai strips */
#ts,#bs{position:fixed;left:0;right:0;height:5px;z-index:999;opacity:.6;}
#ts{top:0;background:repeating-linear-gradient(90deg,#8B0000 0,#8B0000 20px,#C9A84C 20px,#C9A84C 40px);}
#bs{bottom:0;background:repeating-linear-gradient(90deg,#C9A84C 0,#C9A84C 20px,#8B0000 20px,#8B0000 40px);}

/* Layout */
#app{position:relative;z-index:1;flex:1;display:flex;flex-direction:column;padding:8px 10px 70px;}
#menu{position:relative;z-index:1;display:flex;flex-direction:column;min-height:100vh;}

/* ── CARDS ── */
.card{width:72px;height:104px;border-radius:10px;border:3px solid #78350f;
  background:linear-gradient(160deg,#fffdf0 55%,#f5e8c0);
  display:flex;flex-direction:column;justify-content:space-between;
  padding:5px;position:relative;flex-shrink:0;cursor:pointer;
  transition:transform .15s,box-shadow .15s,border-color .15s;}
.card.tiny{width:38px;height:56px;padding:3px;border-radius:7px;border-width:2px;}
.cr{font-weight:900;line-height:1.1;font-size:15px;color:#111;}
.card.tiny .cr{font-size:9px;}
.cs{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:30px;opacity:.13;pointer-events:none;}
.card.tiny .cs{font-size:18px;}
.crb{font-weight:900;line-height:1.1;font-size:15px;color:#111;transform:rotate(180deg);align-self:flex-end;}
.card.tiny .crb{font-size:9px;}
.card.red .cr,.card.red .crb{color:#dc2626;}
.card.back{background:linear-gradient(135deg,#1a3a5c,#0c1e38);}
.card.back::before{content:'';position:absolute;inset:3px;border-radius:7px;border:2px solid rgba(147,197,253,.2);}
.koru{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:24px;opacity:.18;}
.card.steal-g{border-color:#10b981!important;box-shadow:0 0 16px 5px rgba(16,185,129,.85);}
.card.place-g{border-color:#3b82f6!important;box-shadow:0 0 14px 4px rgba(59,130,246,.75);}
.card.lifted{border-color:#f59e0b!important;
  box-shadow:0 0 22px 8px rgba(245,158,11,.85),0 12px 24px rgba(0,0,0,.5);
  transform:translateY(-18px) rotate(-3deg) scale(1.05);}

/* ── PILE ── */
.pslot{position:relative;}
.pempty{width:38px;height:56px;border-radius:7px;border:2px dashed rgba(255,255,255,.25);
  display:flex;align-items:center;justify-content:center;color:rgba(255,255,255,.3);font-size:20px;}
.gring{position:absolute;inset:-3px;border-radius:10px;pointer-events:none;animation:gp 1s ease-in-out infinite;}
.blov{position:absolute;inset:0;border-radius:7px;background:rgba(220,38,38,.35);
  display:flex;align-items:center;justify-content:center;font-size:14px;pointer-events:none;}
@keyframes gp{0%,100%{opacity:1}50%{opacity:.25}}

/* ── PLAYER BOX ── */
.pbox{border-radius:12px;padding:7px 9px;display:flex;flex-direction:column;align-items:center;gap:4px;
  min-width:88px;position:relative;border:2px solid #78350f;
  transition:box-shadow .2s,border-color .2s;}
.pbox.cp{cursor:pointer;}
.tbadge{position:absolute;top:-9px;left:50%;transform:translateX(-50%);
  background:#d97706;border-radius:7px;padding:1px 8px;font-size:8px;font-weight:900;
  color:#fff;white-space:nowrap;border:2px solid #fbbf24;}
.pnm{font-size:10px;font-weight:700;}
.phc{font-size:15px;font-weight:900;color:#93c5fd;}
.ppc{font-size:8px;color:#fcd34d;}

/* ── DECK ── */
.dstk{position:relative;width:82px;height:114px;}
.dsh{position:absolute;width:72px;height:104px;border-radius:10px;border:3px solid #78350f;}
.ds2{top:8px;left:8px;background:#1a3a5c;z-index:0;}
.ds1{top:4px;left:4px;background:#1c3d62;z-index:1;}
.dtop{position:absolute;top:0;left:0;z-index:2;}
.dem{width:72px;height:104px;border-radius:10px;border:2px dashed #a16207;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  color:#a16207;font-size:10px;gap:3px;opacity:.7;}

/* ── HAND SECTION ── */
#handarea{
  position:fixed;bottom:5px;left:0;right:0;z-index:50;
  display:flex;flex-direction:column;align-items:center;gap:0;
}
#hlbl{
  font-size:9px;font-weight:700;letter-spacing:.14em;
  background:rgba(0,0,0,.8);padding:3px 14px;border-radius:8px 8px 0 0;
  border:2px solid #78350f;border-bottom:none;color:#fef3c7;
}
#hcards{
  display:flex;gap:12px;justify-content:center;
  padding:10px 18px 12px;
  background:rgba(0,0,0,.65);
  border-radius:0 0 12px 12px;
  border:2px solid #78350f;border-top:none;
  box-shadow:0 4px 20px rgba(0,0,0,.5);
}
.hcard-wrap{transition:transform .15s ease;cursor:pointer;}
.hcard-wrap:hover{transform:translateY(-6px);}

/* ── MISC ── */
.glog{height:44px;overflow-y:auto;border-radius:8px;border:1px solid rgba(139,53,15,.6);
  background:rgba(0,0,0,.65);padding:3px 8px;font-family:monospace;font-size:9.5px;}
.glog div{color:#fef3c7;line-height:1.55;}
.sb{display:flex;gap:5px;margin-bottom:5px;}
.sc{flex:1;border-radius:8px;padding:4px 5px;background:rgba(0,0,0,.5);text-align:center;border:1px solid transparent;}
.hbar{text-align:center;min-height:22px;margin-bottom:4px;}
.hpill{display:inline-block;font-size:10px;background:rgba(0,0,0,.7);padding:3px 14px;border-radius:10px;border:1px solid #78350f;}
#tiptop{border-radius:10px;padding:8px 12px;margin-bottom:6px;display:flex;gap:10px;align-items:flex-start;}

/* ── BUTTONS ── */
.btn{padding:9px 20px;border-radius:12px;font-weight:900;font-size:14px;border:none;
  cursor:pointer;font-family:Georgia,serif;transition:transform .1s;}
.btn:active{transform:scale(.97);}
.btn:disabled{opacity:.4;cursor:not-allowed;}
.bg{background:linear-gradient(135deg,#92400e,#d97706);color:#fff;border:3px solid #fbbf24;box-shadow:0 0 12px rgba(251,191,36,.3);}
.bgn{background:linear-gradient(135deg,#065f46,#047857);color:#fff;border:3px solid #059669;}
.brd{background:linear-gradient(135deg,#9f1239,#be123c);color:#fff;border:3px solid #be123c;}
.bpu{background:linear-gradient(135deg,#4c1d95,#7c3aed);color:#fff;border:3px solid #7c3aed;}
.bgr{background:rgba(0,0,0,.5);color:#9ca3af;border:2px solid #6b7280;font-size:12px;}
.bor{background:linear-gradient(135deg,#c2410c,#ea580c);color:#fff;border:3px solid #f97316;}
.inp{width:100%;padding:10px 14px;border-radius:10px;font-size:14px;
  background:rgba(0,0,0,.6);color:#fef3c7;font-family:Georgia,serif;
  outline:none;box-sizing:border-box;border:2px solid #78350f;}
.inp:focus{border-color:#C9A84C;}

/* ── MODALS ── */
.mbg{position:fixed;inset:0;z-index:200;background:rgba(0,0,0,.9);
  display:flex;align-items:center;justify-content:center;padding:16px;}
.mbox{border-radius:20px;border:3px solid #C9A84C;
  background:linear-gradient(160deg,#0c1a0c,#111a08);
  padding:24px 22px;max-width:440px;width:100%;max-height:86vh;overflow-y:auto;}

/* ── STAKE ── */
.sgrid{display:flex;gap:6px;flex-wrap:wrap;}
.sbtn{flex:1 1 calc(25% - 6px);min-width:52px;padding:9px 3px;border-radius:10px;
  font-weight:900;font-size:12px;cursor:pointer;font-family:Georgia,serif;
  border:2px solid rgba(255,255,255,.12);background:rgba(0,0,0,.5);color:#9ca3af;
  display:flex;flex-direction:column;align-items:center;gap:1px;transition:all .15s;}
.sbtn.on{border-color:#fbbf24;background:linear-gradient(135deg,#92400e,#d97706);color:#fff;box-shadow:0 0 10px rgba(251,191,36,.35);}

/* ── MENU CARDS ── */
.mcards{display:flex;gap:14px;flex-wrap:wrap;justify-content:center;}
.mcard{flex:1;min-width:110px;max-width:140px;padding:20px 14px;border-radius:18px;
  cursor:pointer;border:2px solid rgba(255,255,255,.1);background:rgba(0,0,0,.5);
  transition:all .2s;text-align:center;display:flex;flex-direction:column;align-items:center;gap:9px;}
.mcard:hover{transform:translateY(-5px) scale(1.02);}

/* ── SEAT SLOTS ── */
.sslot{display:flex;align-items:center;gap:9px;padding:7px 12px;border-radius:10px;
  border:2px solid rgba(255,255,255,.1);background:rgba(0,0,0,.35);margin-bottom:6px;}
.wpanel{border-radius:14px;border:2px solid #be123c;background:rgba(60,0,16,.7);padding:14px 16px;}

/* ── ANIMS ── */
@keyframes tp{0%,100%{text-shadow:0 0 28px rgba(201,168,76,.8),4px 4px 0 #4a0000}50%{text-shadow:0 0 48px rgba(201,168,76,1),0 0 80px rgba(201,168,76,.4),4px 4px 0 #4a0000}}
@keyframes fl{0%,100%{transform:translateY(0) rotate(var(--r))}50%{transform:translateY(-8px) rotate(var(--r))}}
</style>
</head>
<body>
<div id="ts"></div><div id="bs"></div>
<div id="app" style="display:none"></div>
<div id="menu"></div>
<div id="handarea" style="display:none">
  <div id="hlbl"></div>
  <div id="hcards"></div>
</div>

<script>
'use strict';

// ── Storage fallback ──────────────────────────────────────────
if(!window.storage){window.storage={
  async get(k){const v=localStorage.getItem('rp_'+k);return v?{value:v}:null;},
  async set(k,v){localStorage.setItem('rp_'+k,v);return{key:k,value:v};}
};}

// ── Constants ─────────────────────────────────────────────────
const RANKS=['A','K','Q','J','10','9','8','7','6','5','4','3','2'];
const SUITS=['♠','♥','♦','♣'];
const RED=new Set(['♥','♦']);
const RV=r=>({A:14,K:13,Q:12,J:11}[r]??+r);
const STAKES=[1,2,5,10,20,50,100];
const SEAT=[
  {ring:'#059669',bg:'rgba(0,40,20,.85)',lbl:'#6ee7b7'},
  {ring:'#be123c',bg:'rgba(60,0,16,.85)',lbl:'#fda4af'},
  {ring:'#7c3aed',bg:'rgba(36,0,60,.85)',lbl:'#c4b5fd'},
  {ring:'#0891b2',bg:'rgba(0,36,56,.85)',lbl:'#67e8f9'},
];

// ── Game helpers ──────────────────────────────────────────────
const topOf=p=>p.length?p[p.length-1]:null;
const cloneP=ps=>ps.map(p=>({...p,hand:[...p.hand],pile:[...p.pile]}));
const $=id=>document.getElementById(id);

function makeDeck(){return RANKS.flatMap(r=>SUITS.map(s=>({r,s,id:r+s})));}
function shuffle(a){const b=[...a];for(let i=b.length-1;i>0;i--){const j=0|Math.random()*(i+1);[b[i],b[j]]=[b[j],b[i]];}return b;}

function freshGame(names){
  const deck=shuffle(makeDeck());
  return{
    deck,
    players:names.map((name,id)=>({id,name,hand:deck.splice(0,3),pile:[]})),
    turn:0,sel:null,mode:null,steals:0,frozen:[],phase:'play',winner:null,
    log:['🎮 Tīmata! Raupatu begins.','📖 Steal from opponents · Place on YOUR pile only · Draw to 3 after turn']
  };
}

function drawToThree(players,deck,pid){
  const d=[...deck],ps=cloneP(players);
  while(ps[pid].hand.length<3&&d.length)ps[pid].hand.push(d.shift());
  return{players:ps,deck:d};
}

function endTurn(G,pid){
  const next=(pid+1)%G.players.length;
  const{players,deck}=drawToThree(G.players,G.deck,pid);
  return{...G,players,deck,turn:next,sel:null,mode:null,steals:0,frozen:[]};
}

function checkOver(G){
  if(G.deck.length>0||G.players.some(p=>p.hand.length>0))return G;
  const best=Math.max(...G.players.map(p=>p.pile.length));
  const tops=G.players.filter(p=>p.pile.length===best);
  const w=tops.length>1?'Tie':tops[0].name;
  return{...G,phase:'over',winner:w,
    log:[...G.log,tops.length>1?`🤝 He ōrite! Tie — ${tops.map(t=>t.name).join(' & ')} (${best} cards)`:`🏆 ${w} wins with ${best} cards!`]};
}

// ── ACTION RULES ──────────────────────────────────────────────
// STEAL: opponent pile top matches card rank → pile + card → own pile; mode locks to steal
//        Auto-ends if hand emptied; can chain multiple steals
// PLACE: own pile only; always ends turn (even after stealing)
// END TURN: available after stealing, skips placing

function doAction(G,myPid,targetId){
  if(G.sel===null||G.sel>=G.players[myPid].hand.length)return G;
  const card=G.players[myPid].hand[G.sel];
  const tgt=G.players[targetId];
  const top=topOf(tgt.pile);
  const isOpp=targetId!==myPid;
  const isOwn=targetId===myPid;
  const matches=top&&top.r===card.r;
  const frozen=G.frozen.includes(targetId);

  if(isOpp&&matches&&G.mode!=='place'&&!frozen){
    // STEAL
    const ps=cloneP(G.players);
    ps[myPid].hand.splice(G.sel,1);
    const stolen=[...ps[targetId].pile];
    ps[myPid].pile=[...ps[myPid].pile,...stolen,card];
    ps[targetId].pile=[];
    const G2={...G,players:ps,sel:null,mode:'steal',steals:G.steals+1,
      frozen:[...G.frozen,targetId],
      log:[...G.log,`🔥 ${G.players[myPid].name} stole ${stolen.length} from ${tgt.name} with ${card.r}! (pile: ${ps[myPid].pile.length})`]};
    if(ps[myPid].hand.length===0)
      return checkOver(endTurn({...G2,log:[...G2.log,'§ Hand empty — auto end turn']},myPid));
    return G2;
  }

  if(isOwn){
    // PLACE on own pile — always ends turn
    const ps=cloneP(G.players);
    ps[myPid].hand.splice(G.sel,1);
    ps[myPid].pile.push(card);
    return checkOver(endTurn({...G,players:ps,
      log:[...G.log,`📤 ${G.players[myPid].name} placed ${card.r}${card.s} → pile ${ps[myPid].pile.length}`]},myPid));
  }

  if(isOpp&&frozen)return{...G,sel:null,log:[...G.log,`🚫 ${tgt.name}'s pile is frozen this turn`]};
  if(isOpp&&!matches)return{...G,sel:null,log:[...G.log,`§ No rank match — ${card.r} ≠ ${top?top.r:'empty pile'}`]};
  return{...G,sel:null};
}

// ── SFX ──────────────────────────────────────────────────────
const SFX=(()=>{
  let ctx=null;
  const ac=()=>{if(!ctx)try{ctx=new(window.AudioContext||window.webkitAudioContext)();}catch{}return ctx;};
  const tone=(f,t,d,v=.14,dl=0)=>{const c=ac();if(!c)return;const o=c.createOscillator(),g=c.createGain();o.connect(g);g.connect(c.destination);o.type=t;o.frequency.setValueAtTime(f,c.currentTime+dl);g.gain.setValueAtTime(0,c.currentTime+dl);g.gain.linearRampToValueAtTime(v,c.currentTime+dl+.01);g.gain.exponentialRampToValueAtTime(.001,c.currentTime+dl+d);o.start(c.currentTime+dl);o.stop(c.currentTime+dl+d+.06);};
  const nz=(d,v=.06,dl=0)=>{const c=ac();if(!c)return;const b=c.createBuffer(1,c.sampleRate*d,c.sampleRate);const da=b.getChannelData(0);for(let i=0;i<da.length;i++)da[i]=Math.random()*2-1;const s=c.createBufferSource(),g=c.createGain();s.buffer=b;s.connect(g);g.connect(c.destination);g.gain.setValueAtTime(v,c.currentTime+dl);g.gain.exponentialRampToValueAtTime(.001,c.currentTime+dl+d);s.start(c.currentTime+dl);s.stop(c.currentTime+dl+d+.06);};
  return{
    pick(){nz(.04,.08);tone(520,'sine',.07,.06);},
    place(){nz(.06,.1);tone(180,'triangle',.12,.1);},
    steal(){nz(.08,.14);tone(330,'sawtooth',.14,.11);tone(500,'sine',.22,.09,.1);tone(660,'sine',.28,.08,.18);},
    draw(){nz(.03,.05);tone(700,'sine',.05,.04);},
    desel(){tone(400,'triangle',.05,.05);},
    win(){[523,659,784,1047].forEach((f,i)=>tone(f,'sine',.4,.16,i*.11));},
    lose(){[440,370,311,261].forEach((f,i)=>tone(f,'sine',.35,.12,i*.1));},
    aiSteal(){tone(200,'sawtooth',.2,.07);nz(.06,.05,.05);},
  };
})();

// ── App state ─────────────────────────────────────────────────
const A={G:null,session:null,isTut:false,tutStep:'select',pollId:null,aiT:[],wallet:null,ethPrice:null,stake:1};
const clearTimers=()=>{if(A.pollId){clearInterval(A.pollId);A.pollId=null;}A.aiT.forEach(clearTimeout);A.aiT=[];};

// ── Card HTML ─────────────────────────────────────────────────
function cardH(card,cls=''){
  if(!card||card==='BACK')return`<div class="card back${cls?' '+cls:''}"><div class="koru">🌀</div></div>`;
  const r=RED.has(card.s)?' red':'';
  return`<div class="card${r}${cls?' '+cls:''}">
    <div class="cr">${card.r}<br>${card.s}</div>
    <div class="cs">${card.s}</div>
    <div class="crb">${card.r}<br>${card.s}</div>
  </div>`;
}

function pileH(pile,tiny,sg,pg){
  const top=topOf(pile);
  if(!top)return`<div class="pempty">+</div>`;
  const cx=(sg?'steal-g':pg?'place-g':'');
  const W=tiny?42:54,H=tiny?60:76;
  const sh=pile.length>2
    ?`<div class="dsh ds2" style="width:${W-10}px;height:${H-10}px;top:5px;left:5px;border:2px solid #78350f;"></div>
      <div class="dsh ds1" style="width:${W-10}px;height:${H-10}px;top:2px;left:2px;border:2px solid #78350f;"></div>`
    :pile.length>1?`<div class="dsh ds1" style="width:${W-10}px;height:${H-10}px;top:2px;left:2px;border:2px solid #78350f;"></div>`:'';
  return`<div style="position:relative;width:${W}px;height:${H}px;">
    ${sh}<div style="position:absolute;top:0;left:0;z-index:2;">${cardH(top,(tiny?' tiny ':' ')+cx)}</div>
  </div>`;
}

function deckH(n){
  if(!n)return`<div class="dem"><div>DECK</div><div>EMPTY</div></div>`;
  return`<div class="dstk">${n>2?'<div class="dsh ds2"></div>':''}${n>1?'<div class="dsh ds1"></div>':''}<div class="dtop">${cardH('BACK')}</div></div>`;
}

// ── Player box HTML ───────────────────────────────────────────
function pboxH(player,{isActive,selCard,mode,frozen,myPid}){
  const C=SEAT[player.id%4];
  const top=topOf(player.pile);
  const isFrz=frozen.includes(player.id);
  const isOpp=player.id!==myPid;
  const isOwn=player.id===myPid;
  const matches=selCard&&top&&top.r===selCard.r;
  const canSteal=selCard&&isOpp&&matches&&mode!=='place'&&!isFrz;
  const canPlace=selCard&&isOwn;
  const blocked=selCard&&isFrz&&isOpp;
  const click=canSteal||canPlace;

  let bsh='none',bc=`${C.ring}66`;
  if(canSteal){bsh=`0 0 18px 6px rgba(16,185,129,.8),0 0 0 2px #10b981`;bc='#10b981';}
  else if(canPlace){bsh=`0 0 14px 5px rgba(59,130,246,.7),0 0 0 2px #3b82f6`;bc='#3b82f6';}
  else if(blocked){bsh=`0 0 12px 4px rgba(220,38,38,.6)`;bc='#dc2626';}
  else if(isActive){bsh=`0 0 10px 3px rgba(251,191,36,.3)`;}

  const gr=canSteal||canPlace?`<div class="gring" style="box-shadow:${canSteal?'0 0 16px 7px rgba(16,185,129,.85)':'0 0 13px 5px rgba(59,130,246,.75)'}"></div>`:'';
  const blov=blocked?`<div class="blov">🚫</div>`:'';

  return`<div class="pbox${click?' cp':''}" data-pid="${player.id}"
    style="background:${C.bg};border-color:${bc};box-shadow:${bsh};">
    ${isActive?`<div class="tbadge">⚡ TURN</div>`:''}
    <div class="pnm" style="color:${C.lbl};">${player.name}${isOwn?' ★':''}</div>
    <div class="phc">🂠×${player.hand.length}</div>
    <div class="ppc">${player.pile.length} cards</div>
    <div class="pslot">${pileH(player.pile,true,canSteal,canPlace)}${gr}${blov}</div>
  </div>`;
}

// ── Render game ───────────────────────────────────────────────
function renderGame(){
  const G=A.G;
  const myPid=A.session?.myPid??0;
  const me=G.players[myPid];
  const others=G.players.filter(p=>p.id!==myPid);
  const myTurn=G.turn===myPid&&G.phase==='play';
  const selCard=G.sel!==null&&G.sel<me.hand.length?me.hand[G.sel]:null;

  $('menu').style.display='none';
  $('app').style.display='flex';
  $('handarea').style.display='flex';

  // Hint
  let hint='';
  if(myTurn){
    if(selCard){
      const tgts=others.filter(a=>{const t=topOf(a.pile);return t&&t.r===selCard.r&&G.mode!=='place'&&!G.frozen.includes(a.id);});
      if(G.mode==='steal')hint=tgts.length?`🔥 Steal from ${tgts.map(a=>a.name).join('/')} again · or tap YOUR pile to place`:`No more steals · tap YOUR pile or End Turn`;
      else hint=tgts.length?`Kua ōrite! STEAL ${tgts.map(a=>a.name).join('/')} 🔥 · or tap YOUR pile to place`:`Tap YOUR pile to place card`;
    }else if(G.mode==='steal'){
      hint=`${G.steals} steal${G.steals>1?'s':''} done · select card to steal/place · or End Turn`;
    }else hint='STEAL from opponents · or PLACE 1 card on YOUR pile';
  }else if(G.phase==='play'){hint=`⏳ ${G.players[G.turn]?.name}'s turn…`;}

  const showET=myTurn&&G.mode==='steal'&&G.sel===null;

  $('app').innerHTML=`
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;flex-wrap:wrap;gap:6px;">
    <div>
      <div style="font-size:20px;font-weight:900;letter-spacing:.15em;color:#C9A84C;animation:tp 3s ease-in-out infinite;">✦ RAUPATU ✦</div>
      <div style="font-size:8px;color:#fbbf24;letter-spacing:.14em;">${A.isTut?'TUTORIAL · VS AI':(A.session?.premium?'💰 PREMIUM · ':'')+`ROOM ${A.session?.code||''}`}</div>
    </div>
    <div style="display:flex;gap:7px;align-items:center;">
      <div style="font-size:10px;color:#fcd34d;background:rgba(0,0,0,.6);padding:3px 10px;border-radius:8px;border:1px solid #78350f;">🃏 ${G.deck.length}</div>
      <div style="font-size:11px;font-weight:700;padding:3px 12px;border-radius:10px;
        background:${myTurn?'#065f46':'#7f1d1d'};color:${myTurn?'#fff':'#fca5a5'};">
        ${myTurn?'⚡ YOUR TURN':G.players[G.turn]?.name+'…'}</div>
      <button class="btn bgr" onclick="${A.isTut?'startMenu()':'leaveGame()'}" style="font-size:10px;padding:3px 10px;border-radius:7px;">${A.isTut?'Skip':'Leave'}</button>
    </div>
  </div>
  ${A.isTut?buildTip():''}
  <div style="display:flex;justify-content:center;gap:12px;margin-bottom:8px;">
    ${others.map(p=>pboxH(p,{isActive:G.turn===p.id,selCard:myTurn?selCard:null,mode:G.mode,frozen:G.frozen,myPid})).join('')}
  </div>
  <div style="display:flex;justify-content:center;align-items:center;gap:24px;margin-bottom:8px;">
    ${pboxH(me,{isActive:myTurn,selCard:myTurn?selCard:null,mode:G.mode,frozen:G.frozen,myPid})}
    <div style="display:flex;flex-direction:column;align-items:center;gap:4px;">
      <div style="font-size:9px;color:#fbbf24;font-weight:700;letter-spacing:.1em;">DRAW PILE</div>
      ${deckH(G.deck.length)}
      <div style="font-size:9px;color:#fcd34d;">${G.deck.length} cards</div>
    </div>
  </div>
  <div class="hbar">${hint?`<span class="hpill">${hint}</span>`:''}</div>
  ${showET?`<div style="text-align:center;margin-bottom:6px;">
    <button class="btn bg" onclick="endTurnNow()" style="font-size:12px;padding:7px 22px;">↩️ End Turn &amp; Draw to 3</button>
  </div>`:''}
  <div class="sb">${G.players.map(p=>`<div class="sc" style="border-color:${SEAT[p.id%4].ring}44;">
    <div style="font-size:8px;color:#d1d5db;font-weight:700;">${p.name}${p.id===myPid?' ★':''}</div>
    <div style="font-size:13px;color:#93c5fd;font-weight:900;">🂠×${p.hand.length}</div>
    <div style="font-size:7px;color:#fcd34d;">${p.pile.length} cards</div>
  </div>`).join('')}</div>
  <div class="glog" id="glog">${G.log.map(l=>`<div>${l}</div>`).join('')}</div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:4px;margin-top:5px;">
    ${[['🔥','Steal — match rank, take whole pile'],['📤','Place on YOUR pile only (ends turn)'],['🂠×','Hand count shown live per player'],['🏆','Most cards in pile when deck runs out']].map(([i,t])=>`<div style="border-radius:6px;border:1px solid #78350f;padding:3px 7px;background:rgba(0,0,0,.4);font-size:8.5px;color:#fbbf24;opacity:.75;">${i} ${t}</div>`).join('')}
  </div>`;

  const log=$('glog');if(log)log.scrollTop=log.scrollHeight;
  document.querySelectorAll('[data-pid]').forEach(el=>el.addEventListener('click',()=>onPile(+el.dataset.pid)));

  // Hand
  const C=SEAT[myPid%4];
  let hlbl=`YOUR HAND (${me.hand.length})`;
  if(G.mode==='steal')hlbl+=` · ${G.steals} steal${G.steals>1?'s':''} done`;
  else if(myTurn)hlbl+=' · steal or place on your pile';
  else hlbl+=' · waiting…';
  $('hlbl').textContent=hlbl;
  $('hlbl').style.color=C.lbl;
  $('hlbl').style.borderColor=C.ring;

  $('hcards').style.borderColor=C.ring;
  $('hcards').innerHTML=me.hand.length===0
    ? `<div style="color:rgba(255,255,255,.3);font-size:11px;padding:4px 8px;">Hand empty</div>`
    : me.hand.map((card,i)=>{
        const isSel=G.sel===i;
        const canSt=!isSel&&myTurn&&G.sel===null&&G.mode!=='place'&&
          others.some(a=>{const t=topOf(a.pile);return t&&t.r===card.r&&!G.frozen.includes(a.id);});
        return`<div class="hcard-wrap" onclick="onHand(${i})">${cardH(card,(isSel?'lifted ':'')+( canSt?'steal-g':''))}</div>`;
      }).join('');

  if(G.phase==='over')setTimeout(showOver,120);
  if(!A.isTut&&A.session&&G.turn!==myPid&&G.phase==='play'){
    clearTimers();
    A.pollId=setInterval(async()=>{
      const room=await loadRoom(A.session.code);if(!room?.game)return;
      const R=room.game;if(R.turn!==A.G.turn||R.phase!==A.G.phase||R.log.length!==A.G.log.length){A.G=R;renderGame();}
    },2000);
  }
}

// ── Tutorial tip ──────────────────────────────────────────────
function buildTip(){
  const tips={
    select:{t:'Select a card from your hand ↓',b:'Tap any card below to pick it up.',c:'#C9A84C'},
    steal:{t:'🔥 Raupatuhia! You can steal!',b:'Green glow = rank match! Click that player\'s box.',c:'#10b981'},
    place:{t:'📤 Place on your own pile',b:'Click YOUR box (blue glow) to place the card.',c:'#3b82f6'},
    endturn:{t:'↩️ Done stealing? End your turn',b:'Hit End Turn to draw back to 3 cards.',c:'#f59e0b'},
    ai_watch:{t:'🤖 AI is playing…',b:'AI steals every match, then places. Your turn is next!',c:'#7c3aed'},
  };
  const tp=tips[A.tutStep]||tips.select;
  return`<div id="tiptop" style="border:2px solid ${tp.c};background:${tp.c}18;margin-bottom:6px;">
    <div style="flex:1;">
      <div style="font-size:11px;font-weight:700;color:${tp.c};margin-bottom:2px;">${tp.t}</div>
      <div style="font-size:10px;color:#d1d5db;line-height:1.5;">${tp.b}</div>
    </div>
    <button class="btn bgr" onclick="startMenu()" style="font-size:10px;padding:2px 8px;flex-shrink:0;">Skip</button>
  </div>`;
}
function updTip(){
  const G=A.G,pid=0;
  if(G.phase==='over')return;
  if(G.turn!==pid){A.tutStep='ai_watch';return;}
  if(G.sel===null){A.tutStep=G.mode==='steal'?'endturn':'select';return;}
  const sc=G.players[pid].hand[G.sel];
  const hs=G.players.filter(p=>p.id!==pid).some(a=>{const t=topOf(a.pile);return t&&t.r===sc?.r&&!G.frozen.includes(a.id);});
  A.tutStep=hs?'steal':'place';
}

// ── Event handlers ────────────────────────────────────────────
function onHand(i){
  const pid=A.session?.myPid??0;
  if(A.G.turn!==pid||A.G.phase!=='play')return;
  const was=A.G.sel===i;
  A.G={...A.G,sel:was?null:i};
  was?SFX.desel():SFX.pick();
  if(A.isTut)updTip();
  renderGame();
}
function onPile(targetId){
  const pid=A.session?.myPid??0;
  if(A.G.turn!==pid||A.G.phase!=='play'||A.G.sel===null)return;
  const wasMode=A.G.mode;
  const next=doAction(A.G,pid,targetId);
  if(next===A.G)return;
  if(next.mode==='steal')SFX.steal();else SFX.place();
  A.G=next;
  if(A.isTut){updTip();if(A.G.phase==='play'&&A.G.turn!==0)schedAI();}
  else if(A.session)pushState();
  renderGame();
}
function endTurnNow(){
  const pid=A.session?.myPid??0;
  if(A.G.turn!==pid||A.G.mode!=='steal')return;
  SFX.draw();
  A.G=checkOver(endTurn({...A.G,log:[...A.G.log,`↩️ ${A.G.players[pid].name} ends turn`]},pid));
  if(A.isTut){updTip();if(A.G.phase==='play'&&A.G.turn!==0)schedAI();}
  else if(A.session)pushState();
  renderGame();
}
async function pushState(){const room=await loadRoom(A.session.code);if(room){room.game=A.G;await saveRoom(A.session.code,room);}}

// ── Game over ─────────────────────────────────────────────────
function showOver(){
  const G=A.G;
  const myName=A.session?G.players[A.session.myPid]?.name:'You';
  const isW=G.winner===myName;
  isW?SFX.win():SFX.lose();
  const pool=A.session?.stakeUsd?G.players.length*A.session.stakeUsd:0;
  const d=document.createElement('div');d.className='mbg';d.style.zIndex='300';
  d.innerHTML=`<div style="text-align:center;padding:32px 40px;border-radius:20px;border:4px solid #f59e0b;background:linear-gradient(160deg,#180900,#2c1800);max-width:360px;width:100%;">
    <div style="font-size:50px;margin-bottom:10px;">${isW?'🏆':G.winner==='Tie'?'🤝':'🤖'}</div>
    <div style="font-size:22px;font-weight:900;color:#fbbf24;margin-bottom:8px;letter-spacing:.1em;">${isW?'KO AU TE TOA!':G.winner==='Tie'?'HE ŌRITE!':G.winner+' WINS!'}</div>
    <div style="color:#fef3c7;line-height:2;font-size:10px;margin-bottom:12px;">${G.players.map(p=>`${p.name}: ${p.pile.length} cards`).join(' · ')}</div>
    ${pool&&G.winner!=='Tie'?`<div style="font-size:15px;color:#34d399;font-weight:700;margin-bottom:10px;">💰 $${pool} → ${G.winner}</div>`:''}
    <div style="display:flex;gap:8px;justify-content:center;flex-wrap:wrap;">
      <button class="btn bg" onclick="startMenu()">← Menu</button>
      ${A.isTut?`<button class="btn bgn" onclick="this.closest('.mbg').remove();startTut()">🔄 Again</button>`:''}
    </div>
  </div>`;
  document.body.appendChild(d);
}

// ── Tutorial AI ───────────────────────────────────────────────
function schedAI(){
  clearTimers();
  if(A.G.turn===0||A.G.phase!=='play')return;
  const pid=A.G.turn;
  A.aiT.push(setTimeout(()=>{
    if(A.G.turn!==pid||A.G.phase!=='play')return;
    A.G=runAI(A.G,pid);updTip();renderGame();
    if(A.G.phase==='play'&&A.G.turn!==0)schedAI();
  },900+pid*200));
}
function runAI(G,pid){
  const ps=cloneP(G.players);let deck=[...G.deck],logs=[...G.log];
  let didSteal=false,again=true;
  while(again){again=false;
    for(let opp=0;opp<G.players.length;opp++){
      if(opp===pid)continue;
      const top=topOf(ps[opp].pile);if(!top)continue;
      const mi=ps[pid].hand.findIndex(c=>c.r===top.r);if(mi===-1)continue;
      const card=ps[pid].hand.splice(mi,1)[0];
      const st=[...ps[opp].pile];
      ps[pid].pile=[...ps[pid].pile,...st,card];ps[opp].pile=[];
      if(opp===0)SFX.aiSteal();
      didSteal=true;
      logs.push(`🤖 ${ps[pid].name} stole ${st.length}+1 from ${ps[opp].name} with ${card.r}! (pile: ${ps[pid].pile.length})`);
      again=true;break;
    }
  }
  if(!didSteal&&ps[pid].hand.length>0){
    const sorted=[...ps[pid].hand].sort((a,b)=>RV(a.r)-RV(b.r));
    const pl=sorted[0];ps[pid].hand.splice(ps[pid].hand.findIndex(c=>c.id===pl.id),1);
    ps[pid].pile.push(pl);SFX.place();
    logs.push(`📤 ${ps[pid].name} placed ${pl.r}${pl.s} (pile: ${ps[pid].pile.length})`);
  }
  const{players:ps2,deck:d2}=drawToThree(ps,deck,pid);
  const drew=ps2[pid].hand.length-ps[pid].hand.length;
  if(drew>0){SFX.draw();logs.push(`§ ${ps2[pid].name} drew ${drew}`);}
  const nxt=(pid+1)%G.players.length;
  return checkOver({...G,players:ps2,deck:d2,log:logs,turn:nxt,sel:null,mode:null,steals:0,frozen:[]});
}

// ── MetaMask ──────────────────────────────────────────────────
async function connectWallet(){if(!window.ethereum)throw new Error('MetaMask not installed');return(await window.ethereum.request({method:'eth_requestAccounts'}))[0];}
async function getBalance(a){const h=await window.ethereum.request({method:'eth_getBalance',params:[a,'latest']});return(parseInt(h,16)/1e18).toFixed(4);}
async function getChain(){const h=await window.ethereum.request({method:'eth_chainId'});const id=parseInt(h,16);return{1:'Ethereum',137:'Polygon',56:'BSC',8453:'Base',10:'Optimism',42161:'Arbitrum',11155111:'Sepolia'}[id]||`Chain ${id}`;}
async function getEthPrice(){try{const r=await fetch('https://api.coingecko.com/api/v3/simple/price?ids=ethereum&vs_currencies=usd');const d=await r.json();return d?.ethereum?.usd||3000;}catch{return 3000;}}
function usdToWei(usd,ep){return'0x'+BigInt(Math.round(usd/ep*1e18)).toString(16);}
async function sendStake(from,to,usd,ep){return window.ethereum.request({method:'eth_sendTransaction',params:[{from,to,value:usdToWei(usd,ep),gas:'0x5208'}]});}

// ── Room storage ──────────────────────────────────────────────
async function loadRoom(c){try{const r=await window.storage.get(`raupatu-room-${c}`,true);return r?JSON.parse(r.value):null;}catch{return null;}}
async function saveRoom(c,room){try{await window.storage.set(`raupatu-room-${c}`,JSON.stringify(room),true);}catch{}}
const randCode=()=>Math.random().toString(36).slice(2,6).toUpperCase();

// ── Show menu screens ─────────────────────────────────────────
function showMenu(html){
  $('app').style.display='none';$('handarea').style.display='none';
  $('menu').style.display='flex';$('menu').style.flexDirection='column';
  $('menu').innerHTML=html;
}

function startMenu(){
  clearTimers();A.isTut=false;A.G=null;A.session=null;
  const mcs=[
    {ic:'📖',ti:'Ngā Ture',su:'Rules & Guide',co:'#C9A84C',fn:'showRules()'},
    {ic:'🎓',ti:'Tutorial',su:'Learn vs AI',co:'#7c3aed',fn:'startTut()'},
    {ic:'🎮',ti:'Free Play',su:'Create or join',co:'#059669',fn:'showFree()'},
    {ic:'💰',ti:'Premium',su:'$1–$100 stake',co:'#be123c',fn:'showPremium()'},
  ];
  showMenu(`<div style="flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:28px;gap:22px;position:relative;overflow:hidden;">
    <div style="position:absolute;top:8%;left:5%;font-size:58px;opacity:.04;pointer-events:none;--r:-15deg;animation:fl 3s ease-in-out infinite;">♠</div>
    <div style="position:absolute;top:10%;right:6%;font-size:58px;opacity:.04;pointer-events:none;--r:12deg;animation:fl 3.5s ease-in-out infinite;">♥</div>
    <div style="position:absolute;bottom:18%;left:4%;font-size:58px;opacity:.04;pointer-events:none;--r:20deg;animation:fl 4s ease-in-out infinite;">♦</div>
    <div style="position:absolute;bottom:14%;right:5%;font-size:58px;opacity:.04;pointer-events:none;--r:-10deg;animation:fl 3.2s ease-in-out infinite;">♣</div>
    <div style="text-align:center;position:relative;z-index:1;">
      <div style="font-size:36px;font-weight:900;letter-spacing:.18em;color:#C9A84C;animation:tp 3s ease-in-out infinite;">✦ RAUPATU ✦</div>
      <div style="font-size:9px;color:#a16207;letter-spacing:.3em;margin-top:4px;">NGERI TĀHAE KĀRI</div>
      <div style="font-size:8px;color:#78350f;letter-spacing:.18em;margin-top:2px;">THE CARD STEALING GAME · 2–4 PLAYERS</div>
    </div>
    <div class="mcards" style="position:relative;z-index:1;max-width:540px;">
      ${mcs.map(c=>`<div class="mcard" onclick="${c.fn}"
        onmouseover="this.style.borderColor='${c.co}';this.style.boxShadow='0 0 24px ${c.co}44'"
        onmouseout="this.style.borderColor='rgba(255,255,255,.1)';this.style.boxShadow='none'">
        <div style="font-size:32px;">${c.ic}</div>
        <div><div style="font-size:14px;font-weight:900;color:#fef3c7;">${c.ti}</div>
        <div style="font-size:9px;color:#9ca3af;margin-top:2px;">${c.su}</div></div>
      </div>`).join('')}
    </div>
    <div style="font-size:8px;color:#4a3020;letter-spacing:.12em;position:relative;z-index:1;">KL-1.0 KAITIAKI LICENCE · OK SHAQ RECORDS · AOTEAROA</div>
  </div>`);
}

function showRules(){
  document.querySelector('.mbg')?.remove();
  const rules=[
    ['🎯','Objective','Most cards in your pile when deck AND all hands are empty.'],
    ['🂠','Hand','Hold up to 3 cards. After your turn, draw back to 3 automatically. When deck is gone, play out your hand.'],
    ['⚖️','Match','Rank only — suits don\'t matter. Any 7 beats any 7.'],
    ['🔥','Steal','Match an opponent\'s top pile card → take their whole pile + your card all go onto your pile. Chain multiple steals in one turn.'],
    ['📤','Place','Play 1 card onto YOUR OWN pile only. Ends your turn immediately (even after stealing).'],
    ['🚫','Frozen','A pile just stolen this turn can\'t be stolen again this turn.'],
    ['↩️','End Turn','After stealing, tap End Turn to draw to 3 without placing.'],
    ['💰','Premium','$1/$2/$5/$10/$20/$50/$100 MetaMask buy-in. Winner takes pool.'],
  ];
  const d=document.createElement('div');d.className='mbg';
  d.onclick=e=>{if(e.target===d)d.remove();};
  d.innerHTML=`<div class="mbox">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:16px;">
      <div><div style="font-size:18px;font-weight:900;color:#C9A84C;letter-spacing:.15em;">✦ NGĀ TURE ✦</div>
      <div style="font-size:8px;color:#fbbf24;letter-spacing:.2em;">RULES OF RAUPATU</div></div>
      <button onclick="this.closest('.mbg').remove()" style="background:rgba(255,255,255,.08);border:none;color:#9ca3af;font-size:18px;cursor:pointer;border-radius:7px;width:30px;height:30px;">✕</button>
    </div>
    ${rules.map(([ic,ti,bo])=>`<div style="margin-bottom:10px;padding:9px 11px;border-radius:10px;background:rgba(255,255,255,.04);border:1px solid rgba(201,168,76,.2);">
      <div style="display:flex;gap:9px;"><span style="font-size:17px;flex-shrink:0;">${ic}</span><div>
        <div style="font-size:11px;font-weight:700;color:#C9A84C;margin-bottom:2px;">${ti}</div>
        <div style="font-size:9.5px;color:#d1d5db;line-height:1.6;">${bo}</div>
      </div></div></div>`).join('')}
    <button class="btn bg" onclick="this.closest('.mbg').remove()" style="width:100%;margin-top:8px;">Kia ora! Close</button>
  </div>`;
  document.body.appendChild(d);
}

function startTut(){
  clearTimers();A.isTut=true;A.session=null;
  A.G=freshGame(['You','Hine-AI','Tūhoe-AI','Rangi-AI']);A.tutStep='select';
  renderGame();
  const d=document.createElement('div');d.className='mbg';
  d.innerHTML=`<div style="text-align:center;padding:30px 26px;border-radius:20px;border:3px solid #C9A84C;background:linear-gradient(160deg,#0c1a0c,#111a08);max-width:360px;width:100%;">
    <div style="font-size:46px;margin-bottom:10px;">🎴</div>
    <div style="font-size:18px;font-weight:900;color:#C9A84C;letter-spacing:.1em;margin-bottom:8px;">TŪTURU MAI!</div>
    <div style="font-size:10.5px;color:#d1d5db;line-height:1.7;margin-bottom:20px;">
      Play vs 3 AI opponents and learn the rules.<br>
      <b style="color:#10b981;">Green glow</b> = you can steal that pile.<br>
      <b style="color:#3b82f6;">Blue glow</b> = tap to place on your pile.<br>
      Your hand is shown at the bottom of the screen.
    </div>
    <div style="display:flex;gap:8px;justify-content:center;">
      <button class="btn bg" id="tg">🎮 Let's Play!</button>
      <button class="btn bgr" onclick="startMenu()">Skip →</button>
    </div>
  </div>`;
  document.body.appendChild(d);
  $('tg').onclick=()=>{d.remove();schedAI();};
  localStorage.setItem('raupatu_tut','1');
}

function showFree(){
  clearTimers();A.isTut=false;
  showMenu(`<div style="flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:24px;gap:14px;">
    <div style="text-align:center;">
      <div style="font-size:22px;font-weight:900;color:#059669;">🎮 Free Rooms</div>
      <div style="font-size:9px;color:#6b7280;margin-top:3px;">No buy-in · Play for fun</div>
    </div>
    <div style="width:100%;max-width:320px;display:flex;flex-direction:column;gap:9px;">
      <input class="inp" id="fn" placeholder="Your name…" maxlength="16" style="border-color:#059669;">
      <button class="btn bgn" onclick="doFH()" style="width:100%;">🏠 Create Room</button>
      <div style="display:flex;gap:7px;">
        <input class="inp" id="fc" placeholder="Room code…" maxlength="4" style="flex:1;" oninput="this.value=this.value.toUpperCase()">
        <button class="btn brd" onclick="doFJ()">Join →</button>
      </div>
      <div id="ferr" style="color:#f87171;font-size:10px;text-align:center;display:none;"></div>
    </div>
    <button class="btn bgr" onclick="startMenu()">← Back</button>
  </div>`);
}
async function doFH(){const n=$('fn')?.value.trim();if(!n)return setE('ferr','Enter your name');const c=randCode();await saveRoom(c,{code:c,seats:[{pid:0,name:n,joined:true},null,null,null],started:false,hostPid:0,game:null,premium:false});A.session={code:c,myPid:0,myName:n,premium:false};showWait();}
async function doFJ(){const n=$('fn')?.value.trim(),c=$('fc')?.value.trim().toUpperCase();if(!n)return setE('ferr','Enter your name');if(!c||c.length<4)return setE('ferr','Enter 4-letter code');const room=await loadRoom(c);if(!room)return setE('ferr','Room not found');if(room.started)return setE('ferr','Already started');const slot=room.seats.findIndex(s=>s===null);if(slot===-1)return setE('ferr','Room full');room.seats[slot]={pid:slot,name:n,joined:true};await saveRoom(c,room);A.session={code:c,myPid:slot,myName:n,premium:false};showWait();}
function setE(id,m){const e=$(id);if(e){e.textContent=m;e.style.display='block';}}

function showPremium(){
  clearTimers();A.isTut=false;
  if(!A.ethPrice)getEthPrice().then(p=>{A.ethPrice=p;updE();});
  showMenu(`<div style="flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:22px 16px;gap:13px;overflow-y:auto;">
    <div style="text-align:center;">
      <div style="font-size:22px;font-weight:900;color:#be123c;">💰 Premium Rooms</div>
      <div style="font-size:9px;color:#6b7280;margin-top:3px;">MetaMask buy-in · Winner takes pool</div>
    </div>
    <div class="wpanel" style="max-width:360px;">
      <div style="font-size:9px;color:#fda4af;font-weight:700;margin-bottom:9px;letter-spacing:.1em;">💳 WALLET</div>
      <div id="wc"><button class="btn bor" onclick="doConn()" style="width:100%;display:flex;align-items:center;justify-content:center;gap:9px;"><span style="font-size:20px;">🦊</span> Connect MetaMask</button></div>
    </div>
    <div style="width:100%;max-width:360px;">
      <div style="font-size:9px;color:#fda4af;font-weight:700;margin-bottom:7px;letter-spacing:.1em;">🎰 BUY-IN AMOUNT</div>
      <div class="sgrid">${STAKES.map(a=>`<button class="sbtn${A.stake===a?' on':''}" data-s="${a}" onclick="pickStake(${a})"><span style="font-size:13px;">$${a}</span><span class="sE" data-u="${a}" style="font-size:7.5px;opacity:.65;">${A.ethPrice?(a/A.ethPrice).toFixed(5)+' ETH':'…'}</span></button>`).join('')}</div>
      <div style="margin-top:8px;padding:7px 12px;border-radius:10px;background:rgba(201,168,76,.08);border:1px solid rgba(201,168,76,.25);display:flex;justify-content:space-between;align-items:center;">
        <div style="font-size:10px;color:#fbbf24;font-weight:700;">Selected</div>
        <div style="text-align:right;"><div style="font-size:15px;font-weight:900;color:#fbbf24;" id="susd">$${A.stake}</div><div style="font-size:8px;color:#a16207;" id="seth">${A.ethPrice?(A.stake/A.ethPrice).toFixed(6)+' ETH':'…'}</div></div>
      </div>
    </div>
    <div style="width:100%;max-width:360px;display:flex;flex-direction:column;gap:8px;">
      <input class="inp" id="pn" placeholder="Your name…" maxlength="16" style="border-color:#be123c;">
      <button class="btn brd" id="hbtn" onclick="doPH()" disabled style="width:100%;">🏠 Host — $<span id="hsk">${A.stake}</span> buy-in</button>
      <div style="display:flex;gap:7px;">
        <input class="inp" id="pc" placeholder="Room code…" maxlength="4" style="flex:1;" oninput="this.value=this.value.toUpperCase()">
        <button class="btn bpu" id="jbtn" onclick="doPJ()" disabled>Stake &amp; Join →</button>
      </div>
      <div id="perr" style="color:#f87171;font-size:10px;text-align:center;display:none;"></div>
      <div id="txst" style="display:none;"></div>
      <div style="font-size:8px;color:#4a3020;text-align:center;line-height:1.6;">Host wallet holds pool · Smart contract escrow recommended for production</div>
    </div>
    <button class="btn bgr" onclick="startMenu()">← Back</button>
  </div>`);
  if(A.wallet)renderWallet();
}
function pickStake(a){A.stake=a;document.querySelectorAll('.sbtn').forEach(b=>b.classList.toggle('on',+b.dataset.s===a));const s=$('susd');if(s)s.textContent=`$${a}`;const e=$('seth');if(e)e.textContent=A.ethPrice?(a/A.ethPrice).toFixed(6)+' ETH':'…';const h=$('hsk');if(h)h.textContent=a;}
function updE(){document.querySelectorAll('.sE').forEach(el=>{const u=+el.dataset.u;el.textContent=A.ethPrice?(u/A.ethPrice).toFixed(5)+' ETH':'…';});const e=$('seth');if(e)e.textContent=A.ethPrice?(A.stake/A.ethPrice).toFixed(6)+' ETH':'…';}
async function doConn(){try{const a=await connectWallet();const[b,c,p]=await Promise.all([getBalance(a),getChain(),getEthPrice()]);A.wallet={addr:a,balance:b,chain:c};A.ethPrice=p;renderWallet();updE();}catch(e){setE('perr',e.message||'Failed');}}
function renderWallet(){const w=A.wallet;const sh=`${w.addr.slice(0,6)}…${w.addr.slice(-4)}`;const wc=$('wc');if(wc)wc.innerHTML=`<div style="display:flex;flex-direction:column;gap:6px;">
  <div style="display:flex;justify-content:space-between;"><span style="font-size:11px;color:#fda4af;font-weight:700;">🦊 ${sh}</span><span style="font-size:9px;color:#6b7280;background:rgba(0,0,0,.4);padding:1px 7px;border-radius:6px;">${w.chain}</span></div>
  <div style="display:flex;justify-content:space-between;border-top:1px solid rgba(255,255,255,.06);padding-top:5px;"><span style="font-size:11px;color:#9ca3af;">Balance</span><span style="font-size:12px;font-weight:700;color:#fbbf24;">${w.balance} ETH</span></div>
  <div style="display:flex;justify-content:space-between;"><span style="font-size:11px;color:#9ca3af;">ETH/USD</span><span style="font-size:10px;color:#6b7280;">$${A.ethPrice?A.ethPrice.toLocaleString():'…'}</span></div>
</div>`;const hb=$('hbtn');if(hb)hb.disabled=false;const jb=$('jbtn');if(jb)jb.disabled=false;}
function txSt(h){const e=$('txst');if(e){e.innerHTML=h;e.style.display=h?'block':'none';}}
async function doPH(){if(!A.wallet)return setE('perr','Connect wallet first');const n=$('pn')?.value.trim();if(!n)return setE('perr','Enter your name');txSt(`<div style="text-align:center;font-size:9.5px;color:#fbbf24;padding:5px;border:1px solid rgba(201,168,76,.2);border-radius:7px;">⏳ Creating room…</div>`);const c=randCode();await saveRoom(c,{code:c,seats:[{pid:0,name:n,addr:A.wallet.addr,joined:true,paid:true},null,null,null],started:false,hostPid:0,game:null,premium:true,stakeUsd:A.stake,treasury:A.wallet.addr,pool:A.stake});txSt(`<div style="text-align:center;font-size:9.5px;color:#34d399;padding:5px;border:1px solid rgba(52,211,153,.2);border-radius:7px;">✅ Room created</div>`);A.session={code:c,myPid:0,myName:n,premium:true,stakeUsd:A.stake,treasury:A.wallet.addr};setTimeout(showWait,500);}
async function doPJ(){if(!A.wallet)return setE('perr','Connect wallet first');const n=$('pn')?.value.trim(),c=$('pc')?.value.trim().toUpperCase();if(!n)return setE('perr','Enter name');if(!c||c.length<4)return setE('perr','Enter code');const room=await loadRoom(c);if(!room)return setE('perr','Room not found');if(!room.premium)return setE('perr','Not a premium room');if(room.started)return setE('perr','Already started');const slot=room.seats.findIndex(s=>s===null);if(slot===-1)return setE('perr','Room full');const rs=room.stakeUsd||1;txSt(`<div style="text-align:center;font-size:9.5px;color:#fbbf24;padding:5px;border:1px solid rgba(201,168,76,.2);border-radius:7px;animation:gp 1s infinite;">⏳ MetaMask — send $${rs}…</div>`);try{const ep=A.ethPrice||await getEthPrice();const tx=await sendStake(A.wallet.addr,room.treasury,rs,ep);room.seats[slot]={pid:slot,name:n,addr:A.wallet.addr,joined:true,paid:true,txHash:tx};room.pool=(room.pool||0)+rs;await saveRoom(c,room);txSt(`<div style="text-align:center;font-size:9.5px;color:#34d399;padding:5px;border:1px solid rgba(52,211,153,.2);border-radius:7px;">✅ $${rs} staked</div>`);A.session={code:c,myPid:slot,myName:n,premium:true,stakeUsd:rs,treasury:room.treasury};setTimeout(showWait,700);}catch(e){txSt('');setE('perr',e.message||'Transaction rejected');}}

function showWait(){
  clearTimers();const{code,myPid,premium}=A.session;
  showMenu(`<div style="flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:24px;gap:14px;">
    <div style="text-align:center;">
      <div style="font-size:18px;font-weight:900;color:${premium?'#be123c':'#059669'};">${premium?'💰 Premium':'🎮 Free'} Room</div>
      <div id="pool" style="font-size:12px;color:#34d399;margin-top:3px;"></div>
    </div>
    <div style="text-align:center;padding:14px 28px;border-radius:16px;border:3px solid #C9A84C;background:rgba(0,0,0,.7);">
      <div style="font-size:10px;color:#a16207;margin-bottom:3px;letter-spacing:.15em;">SHARE THIS CODE</div>
      <div style="font-size:40px;font-weight:900;letter-spacing:.3em;color:#fbbf24;text-shadow:0 0 18px rgba(251,191,36,.6);">${code}</div>
    </div>
    <div style="width:100%;max-width:320px;" id="seats"></div>
    <div style="display:flex;gap:8px;flex-wrap:wrap;justify-content:center;">
      ${myPid===0?`<button class="btn bg" id="sbtn" onclick="doStart()" disabled>🎮 Start (<span id="cnt">0</span>/4)</button>`:
        `<div style="font-size:10px;color:#a16207;padding:9px 18px;border-radius:10px;border:1px solid #78350f;background:rgba(0,0,0,.4);">⏳ Waiting for host…</div>`}
      <button class="btn bgr" onclick="startMenu()">← Leave</button>
    </div>
    <div style="font-size:8px;color:#6b7280;">Polling every 2s…</div>
  </div>`);

  async function tick(){
    const room=await loadRoom(code);if(!room)return;
    if(room.started&&room.game){clearTimers();A.G=room.game;renderGame();return;}
    const seats=room.seats,pool=room.pool||0,filled=seats.filter(Boolean);
    const se=$('seats');
    if(se)se.innerHTML=seats.map((s,i)=>{const C=SEAT[i];return`<div class="sslot" style="${s?`border-color:${C.ring};background:${C.bg}`:''}">
      <div style="width:26px;height:26px;border-radius:50%;background:${s?C.ring:'rgba(255,255,255,.12)'};display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:900;color:#fff;">${i+1}</div>
      <div style="flex:1;"><div style="font-size:12px;font-weight:700;color:${s?C.lbl:'#6b7280'};">${s?s.name:'Waiting…'}</div>
      ${i===0&&s?`<div style="font-size:8px;color:#a16207;">Host${premium?' · Holds pool':''}</div>`:''}
      ${s&&s.pid===myPid?`<div style="font-size:8px;color:#34d399;">← You</div>`:''}
      ${premium&&s?.paid?`<div style="font-size:8px;color:#34d399;">✅ Staked</div>`:''}
      </div>${s?`<div style="font-size:14px;">✓</div>`:''}</div>`;}).join('');
    const pl=$('pool');if(pl)pl.textContent=premium?`💰 Pool: $${pool}`:'';
    const cnt=$('cnt');if(cnt)cnt.textContent=filled.length;
    const sb=$('sbtn');if(sb){sb.disabled=filled.length<2;sb.style.opacity=filled.length<2?.4:1;}
  }
  tick();A.pollId=setInterval(tick,2000);
}
async function doStart(){const room=await loadRoom(A.session.code);if(!room)return;const names=room.seats.filter(Boolean).map(s=>s.name);if(names.length<2)return;const game=freshGame(names);room.started=true;room.game=game;await saveRoom(A.session.code,room);A.G=game;clearTimers();renderGame();}
function leaveGame(){clearTimers();startMenu();}

Object.assign(window,{startMenu,showRules,startTut,showFree,showPremium,showWait,
  doFH,doFJ,doPH,doPJ,doStart,leaveGame,doConn,pickStake,onHand,onPile,endTurnNow});

localStorage.getItem('raupatu_tut')?startMenu():startTut();
</script>
</body>
</html>
