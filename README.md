# daily-action-note
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#172554">
<title>1日の行動ノート</title>
<style>
:root{--bg:#f4f6fb;--card:#fff;--ink:#172033;--muted:#687386;--line:#e6eaf1;--navy:#172554;--accent:#4263eb}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--ink);font-family:system-ui,-apple-system,"Noto Sans JP",sans-serif}
header{background:var(--navy);color:#fff;padding:24px 18px 28px}header .wrap,main{max-width:980px;margin:auto}
h1{font-size:25px;margin:0 0 6px}header p{margin:0;color:#cbd5e1;font-size:14px}
main{padding:18px 14px 50px}.top{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap;margin-bottom:16px}
input,select,button{font:inherit}input,select{border:1px solid var(--line);border-radius:10px;padding:10px;background:#fff;color:var(--ink);min-width:0}
.date{font-weight:700}.grid{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.card{background:var(--card);border:1px solid var(--line);border-radius:16px;padding:17px;box-shadow:0 3px 14px #17255408}
h2{font-size:17px;margin:0 0 14px}.formgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.field{display:flex;flex-direction:column;gap:5px}.field label{font-size:12px;color:var(--muted);font-weight:650}
.wide{grid-column:1/-1}.primary{border:0;background:var(--accent);color:#fff;border-radius:10px;padding:12px 16px;font-weight:700;cursor:pointer}.primary:hover{filter:brightness(.95)}
.stats{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}.stat{background:#f6f8ff;border-radius:12px;padding:12px}.stat small{color:var(--muted)}.stat strong{display:block;font-size:22px;margin-top:3px}
.breakdown{display:flex;flex-direction:column;gap:11px}.barrow{display:grid;grid-template-columns:75px 1fr 65px;gap:9px;align-items:center;font-size:13px}.track{height:10px;background:#edf0f6;border-radius:99px;overflow:hidden}.fill{height:100%;border-radius:99px}
.timeline{display:flex;flex-direction:column;gap:8px}.event{display:grid;grid-template-columns:105px 1fr auto;gap:10px;align-items:center;border:1px solid var(--line);border-radius:12px;padding:10px}.eventtime{font-size:13px;color:var(--muted);font-variant-numeric:tabular-nums}.eventname{font-weight:700}.eventmeta{font-size:12px;color:var(--muted);margin-top:3px}.dot{display:inline-block;width:9px;height:9px;border-radius:50%;margin-right:6px}
.delete{border:0;background:#f1f3f8;color:#5b6475;border-radius:8px;padding:7px 9px;cursor:pointer}.empty{color:var(--muted);font-size:14px;padding:14px 0;text-align:center}
.full{margin-top:14px}.hint{font-size:12px;color:var(--muted);line-height:1.6;margin:12px 0 0}
 .clock-layout{display:grid;grid-template-columns:minmax(240px,440px) minmax(160px,1fr);gap:18px;align-items:center}
#clockChart{width:100%;height:auto;max-width:440px;display:block;margin:auto}
.clock-legend{display:flex;flex-direction:column;gap:8px;font-size:13px}
.legend-row{display:flex;justify-content:space-between;gap:12px;align-items:center}
.legend-name{display:flex;align-items:center;gap:7px;min-width:0}
.legend-swatch{width:11px;height:11px;border-radius:3px;flex:none}
.bar-chart{width:100%;height:260px;display:block}
@media(max-width:700px){.grid{grid-template-columns:1fr}.event{grid-template-columns:88px 1fr auto}.card{padding:14px}.formgrid{gap:8px}.clock-layout{grid-template-columns:1fr}.clock-legend{max-width:440px;width:100%;margin:auto}}
@media(max-width:380px){.formgrid{grid-template-columns:1fr}.wide{grid-column:auto}.event{grid-template-columns:1fr auto}.eventtime{grid-column:1/-1}}
</style>
</head>
<body>
<header><div class="wrap"><h1>1日の行動ノート</h1><p>勉強・部活・ゲームなど、何をどれくらいしたかを記録しよう。</p></div></header>
<main>
  <div class="top"><input class="date" type="date" id="date"><span id="dayTotal" style="font-weight:700">合計 0時間</span></div>
  <div class="grid">
    <section class="card">
      <h2>行動を記録</h2>
      <form id="entryForm" class="formgrid">
        <div class="field"><label for="category">行動</label><select id="category">
          <option>勉強</option><option>部活</option><option>学校</option><option>ゲーム</option><option>睡眠</option><option>食事</option><option>移動</option><option>休憩</option><option>その他</option>
        </select></div>
        <div class="field"><label for="custom">自由入力（任意）</label><input id="custom" placeholder="例：数学、サッカー"></div>
        <div class="field"><label for="start">開始時刻</label><input id="start" type="time" value="16:00" required></div>
        <div class="field"><label for="end">終了時刻</label><input id="end" type="time" value="17:00" required></div>
        <div class="field wide"><label for="memo">メモ（任意）</label><input id="memo" placeholder="例：英単語を30個覚えた"></div>
        <button class="primary wide" type="submit">＋ 記録を追加</button>
      </form>
      <p class="hint">※ 1つの記録は同じ日付内で入力してください。記録はこのブラウザに保存されます。</p>
    </section>
    <section class="card">
      <h2>今日のまとめ</h2>
      <div class="stats">
        <div class="stat"><small>記録した時間</small><strong id="totalHours">0時間</strong></div>
        <div class="stat"><small>行動の種類</small><strong id="kindCount">0種類</strong></div>
      </div>
      <h2 style="margin-top:18px">行動ごとの時間</h2>
      <div id="breakdown" class="breakdown"><div class="empty">まだ記録がありません</div></div>
    </section>
  </div>
  <section class="card full">
    <h2>24時間の行動時計</h2>
    <p class="hint" style="margin-top:-6px">円の上が0時、時計回りに時間が進みます。色の区間で、その時間に何をしていたか確認できます。</p>
    <div class="clock-layout">
      <canvas id="clockChart" width="440" height="440" aria-label="24時間の行動を示す時計グラフ"></canvas>
      <div id="clockLegend" class="clock-legend"><div class="empty">記録すると時計に表示されます。</div></div>
    </div>
  </section>
  <section class="card full">
    <h2>週間の行動時間</h2>
    <p class="hint" style="margin-top:-6px">選択した日を含む7日間の合計を、日ごと・行動別に表示します。</p>
    <canvas id="weekChart" class="bar-chart" height="260" aria-label="週間の行動時間グラフ"></canvas>
  </section>
  <section class="card full">
    <h2>月間の行動時間</h2>
    <p class="hint" style="margin-top:-6px">選択した日が含まれる月の、日ごとの行動時間です。</p>
    <canvas id="monthChart" class="bar-chart" height="280" aria-label="月間の行動時間グラフ"></canvas>
  </section>
  <section class="card full">
    <h2>1日のタイムライン</h2>
    <div id="timeline" class="timeline"><div class="empty">行動を記録すると、ここに表示されます。</div></div>
  </section>
</main>
<script>
const colors={勉強:"#4263eb",部活:"#16a085",学校:"#8b5cf6",ゲーム:"#e58b32",睡眠:"#64748b",食事:"#e45b79",移動:"#0ea5a4",休憩:"#9aa3b2",その他:"#b7791f"};
const $=id=>document.getElementById(id);
const today=new Date();const localDate=new Date(today.getTime()-today.getTimezoneOffset()*60000).toISOString().slice(0,10);
$("date").value=localDate;
let entries=JSON.parse(localStorage.getItem("daily-action-notes-v1")||"[]");
const mins=t=>{const [h,m]=t.split(":").map(Number);return h*60+m};
const fmt=n=>{const h=Math.floor(n/60),m=n%60;return h?`${h}時間${m?m+"分":""}`:`${m}分`};
const save=()=>localStorage.setItem("daily-action-notes-v1",JSON.stringify(entries));
function render(){
 const date=$("date").value, items=entries.filter(x=>x.date===date).sort((a,b)=>a.start.localeCompare(b.start));
 const totals={};items.forEach(x=>totals[x.name]=(totals[x.name]||0)+x.duration);
 const total=items.reduce((s,x)=>s+x.duration,0);
 $("dayTotal").textContent=`合計 ${fmt(total)}`;$("totalHours").textContent=fmt(total);$("kindCount").textContent=Object.keys(totals).length+"種類";
 const breakdown=$("breakdown");
 if(!items.length)breakdown.innerHTML='<div class="empty">まだ記録がありません</div>';
 else breakdown.innerHTML=Object.entries(totals).sort((a,b)=>b[1]-a[1]).map(([name,n])=>`<div class="barrow"><span>${escapeHtml(name)}</span><div class="track"><div class="fill" style="width:${total?100*n/total:0}%;background:${colors[name]||"#8b9bb4"}"></div></div><strong style="text-align:right">${fmt(n)}</strong></div>`).join("");
 const timeline=$("timeline");
 if(!items.length)timeline.innerHTML='<div class="empty">行動を記録すると、ここに表示されます。</div>';
 else timeline.innerHTML=items.map(x=>`<div class="event"><div class="eventtime">${x.start} – ${x.end}</div><div><div class="eventname"><span class="dot" style="background:${colors[x.category]||"#8b9bb4"}"></span>${escapeHtml(x.name)}</div><div class="eventmeta">${fmt(x.duration)}${x.memo?" ・ "+escapeHtml(x.memo):""}</div></div><button class="delete" data-delete="${x.id}" aria-label="削除">削除</button></div>`).join("");
 drawClock(items);
 drawPeriodChart("weekChart",date,"week");
 drawPeriodChart("monthChart",date,"month");
}
function colorFor(x){return colors[x.category]||"#8b9bb4";}
function drawClock(items){
 const canvas=$("clockChart"),ctx=canvas.getContext("2d"),size=canvas.width,c=size/2,outer=184,inner=112;
 ctx.clearRect(0,0,size,size);
 // Background ring represents the full 24 hours; uncovered periods remain pale.
 ctx.beginPath();ctx.arc(c,c,outer,0,Math.PI*2);ctx.arc(c,c,inner,0,Math.PI*2,true);ctx.fillStyle="#edf0f6";ctx.fill("evenodd");
 const sorted=[...items].sort((a,b)=>a.start.localeCompare(b.start));
 sorted.forEach(x=>{
   const a=mins(x.start)/1440*Math.PI*2-Math.PI/2,b=mins(x.end)/1440*Math.PI*2-Math.PI/2;
   ctx.beginPath();ctx.arc(c,c,outer,a,b);ctx.arc(c,c,inner,b,a,true);ctx.closePath();ctx.fillStyle=colorFor(x);ctx.fill();
 });
 // Hour ticks and labels
 for(let h=0;h<24;h++){
   const a=h/24*Math.PI*2-Math.PI/2, r1=outer+5,r2=outer+(h%3===0?15:9);
   ctx.beginPath();ctx.moveTo(c+Math.cos(a)*r1,c+Math.sin(a)*r1);ctx.lineTo(c+Math.cos(a)*r2,c+Math.sin(a)*r2);
   ctx.strokeStyle="#64748b";ctx.lineWidth=h%3===0?2:1;ctx.stroke();
   if(h%3===0){ctx.fillStyle="#475569";ctx.font="12px system-ui";ctx.textAlign="center";ctx.textBaseline="middle";ctx.fillText(String(h).padStart(2,"0"),c+Math.cos(a)*(outer+29),c+Math.sin(a)*(outer+29));}
 }
 ctx.fillStyle="#172033";ctx.textAlign="center";ctx.textBaseline="middle";ctx.font="bold 23px system-ui";ctx.fillText("24時間",c,c-8);
 ctx.fillStyle="#687386";ctx.font="12px system-ui";ctx.fillText("選択日の行動",c,c+16);
 const totals={};items.forEach(x=>totals[x.name]=(totals[x.name]||0)+x.duration);
 const legend=$("clockLegend");
 if(!items.length){legend.innerHTML='<div class="empty">この日の記録はありません。<br>行動を追加すると時計に色がつきます。</div>';return;}
 legend.innerHTML=Object.entries(totals).sort((a,b)=>b[1]-a[1]).map(([name,n])=>{
   const item=items.find(x=>x.name===name);
   return `<div class="legend-row"><span class="legend-name"><i class="legend-swatch" style="background:${colorFor(item)}"></i>${escapeHtml(name)}</span><strong>${fmt(n)}</strong></div>`;
 }).join("")+`<div class="hint">記録のない時間：${fmt(Math.max(0,1440-items.reduce((s,x)=>s+x.duration,0)))}</div>`;
}
function dateObj(s){const [y,m,d]=s.split("-").map(Number);return new Date(y,m-1,d);}
function keyDate(d){return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,"0")}-${String(d.getDate()).padStart(2,"0")}`;}
function drawPeriodChart(id,date,period){
 const canvas=$(id),ctx=canvas.getContext("2d"),rect=canvas.getBoundingClientRect();
 const w=Math.max(300,Math.floor(rect.width||canvas.parentElement.clientWidth||600)),h=period==="week"?260:280,dpr=window.devicePixelRatio||1;
 canvas.width=w*dpr;canvas.height=h*dpr;canvas.style.height=h+"px";ctx.setTransform(dpr,0,0,dpr,0,0);ctx.clearRect(0,0,w,h);
 let days=[];
 const selected=dateObj(date);
 if(period==="week"){
   const start=new Date(selected);start.setDate(start.getDate()-((start.getDay()+6)%7));
   for(let i=0;i<7;i++){const d=new Date(start);d.setDate(start.getDate()+i);days.push(d);}
 }else{
   const y=selected.getFullYear(),m=selected.getMonth(),count=new Date(y,m+1,0).getDate();
   for(let i=1;i<=count;i++)days.push(new Date(y,m,i));
 }
 const names=[...new Set(entries.filter(x=>days.some(d=>keyDate(d)===x.date)).map(x=>x.name))];
 const daily=days.map(d=>{const k=keyDate(d),o={};entries.filter(x=>x.date===k).forEach(x=>o[x.name]=(o[x.name]||0)+x.duration);return o;});
 const max=Math.max(60,...daily.map(o=>Object.values(o).reduce((a,b)=>a+b,0)));
 const left=period==="week"?38:32,right=12,top=18,bottom=period==="week"?38:42,plotH=h-top-bottom,plotW=w-left-right;
 ctx.font="11px system-ui";ctx.textAlign="right";ctx.textBaseline="middle";
 for(let i=0;i<=4;i++){const y=top+plotH-i*plotH/4,val=max*i/4;ctx.strokeStyle="#e8ecf3";ctx.beginPath();ctx.moveTo(left,y);ctx.lineTo(w-right,y);ctx.stroke();ctx.fillStyle="#64748b";ctx.fillText(val>=60?(val/60).toFixed(val%60?1:0)+"h":Math.round(val)+"m",left-6,y);}
 const gap=period==="week"?8:Math.max(1,Math.min(5,plotW/days.length*.18)),barW=Math.max(2,(plotW-gap*(days.length-1))/days.length);
 daily.forEach((o,i)=>{let y=top+plotH;names.forEach(name=>{const val=o[name]||0;if(!val)return;const bh=val/max*plotH;y-=bh;ctx.fillStyle=colorFor(entries.find(x=>x.name===name));ctx.fillRect(left+i*(barW+gap),y,barW,bh);});
   ctx.fillStyle="#64748b";ctx.textAlign="center";ctx.textBaseline="top";
   const label=period==="week"?["月","火","水","木","金","土","日"][i]:String(i+1);
   if(period==="week"||days.length<=16||i%2===0)ctx.fillText(label,left+i*(barW+gap)+barW/2,top+plotH+8);
 });
 const legendY=h-12;let lx=left;ctx.font="10px system-ui";ctx.textAlign="left";ctx.textBaseline="middle";
 names.slice(0,5).forEach(name=>{ctx.fillStyle=colorFor(entries.find(x=>x.name===name));ctx.fillRect(lx,legendY-4,8,8);lx+=12;ctx.fillStyle="#475569";const label=name.length>7?name.slice(0,7)+"…":name;ctx.fillText(label,lx,legendY);lx+=ctx.measureText(label).width+12;});
 if(!names.length){ctx.fillStyle="#687386";ctx.textAlign="center";ctx.fillText("この期間の記録はありません",w/2,h/2);}
}
window.addEventListener("resize",()=>{render();});
function escapeHtml(s){return String(s).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));}
$("entryForm").addEventListener("submit",e=>{
 e.preventDefault();const start=$("start").value,end=$("end").value;
 if(!start||!end||mins(end)<=mins(start)){alert("終了時刻は開始時刻より後に設定してください。");return;}
 const category=$("category").value,name=$("custom").value.trim()||category;
 entries.push({id:Date.now().toString(36)+Math.random().toString(36).slice(2,7),date:$("date").value,category,name,start,end,duration:mins(end)-mins(start),memo:$("memo").value.trim()});
 save();$("custom").value="";$("memo").value="";render();
});
$("timeline").addEventListener("click",e=>{const id=e.target.dataset.delete;if(!id)return;entries=entries.filter(x=>x.id!==id);save();render();});
$("date").addEventListener("change",render);
render();
</script>
</body>
</html>
