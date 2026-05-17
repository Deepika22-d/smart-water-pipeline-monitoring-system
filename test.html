<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Water Dashboard</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body{
  margin:0;
  font-family:'Segoe UI';
  background:linear-gradient(135deg,#141e30,#243b55);
  color:white;
}

.container{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
  gap:15px;
  padding:15px;
}

.card{
  background:rgba(255,255,255,0.05);
  padding:20px;
  border-radius:15px;
  backdrop-filter:blur(10px);
}

.tank{
  width:120px;
  height:120px;
  border:5px solid cyan;
  border-radius:50%;
  margin:auto;
  overflow:hidden;
  position:relative;
}

.fill{
  position:absolute;
  bottom:0;
  width:100%;
  height:0%;
  background:cyan;
  transition:0.5s;
}

.motorIcon{
  font-size:50px;
}
.on{color:#00ffcc; animation:spin 1s linear infinite;}
.off{color:#555;}

@keyframes spin{
  from{transform:rotate(0deg);}
  to{transform:rotate(360deg);}
}

.ok{color:#00ffcc;}
.warn{color:orange;}
.leak{color:red; animation:blink 1s infinite;}

@keyframes blink{
  50%{opacity:0.3;}
}

.alert{
  padding:10px;
  border-radius:10px;
  font-weight:bold;
}

canvas{
  background:white;
  border-radius:10px;
}
</style>
</head>

<body>

<h1 style="text-align:center">💧 Smart Water Dashboard</h1>

<div class="container">

<div class="card">
<h2>Tank Level</h2>
<div class="tank">
<div id="tankFill" class="fill"></div>
</div>
<p id="tankText">--%</p>
<p id="tankAlert"></p>
</div>

<div class="card">
<h2>Motor Status</h2>
<div id="motorIcon" class="motorIcon off">⚙️</div>
<p id="motorText">OFF</p>
</div>

<div class="card">
<h2>Main Pipeline</h2>
<p>IN: <span id="m_in">--</span></p>
<p>OUT: <span id="m_out">--</span></p>
<p id="m_status">--</p>
</div>

<div class="card">
<h2>Sub Pipeline</h2>
<p>IN: <span id="s_in">--</span></p>
<p>OUT: <span id="s_out">--</span></p>
<p id="s_status">--</p>
</div>

<div class="card">
<h2>Main Warning</h2>
<div id="mainWarn" class="alert">No Issues</div>
</div>

<div class="card">
<h2>Sub Warning</h2>
<div id="subWarn" class="alert">No Issues</div>
</div>

<div class="card">
<h2>Total Flow</h2>
<p>Main Total: <span id="mainTotal">0</span></p>
<p>Sub Total: <span id="subTotal">0</span></p>
</div>

<div class="card">
<h2>Main Graph</h2>
<canvas id="mainChart"></canvas>
</div>

<div class="card">
<h2>Sub Graph</h2>
<canvas id="subChart"></canvas>
</div>

</div>

<script>

// 🔴 CHANGE IP HERE
let ws = new WebSocket("ws:192.168.137.146:81/");

let mainChart = new Chart(document.getElementById("mainChart"),{
  type:'line',
  data:{
    labels:[],
    datasets:[
      {label:"Main IN",data:[],borderColor:"cyan"},
      {label:"Main OUT",data:[],borderColor:"yellow"}
    ]
  },
  options:{animation:false}
});

let subChart = new Chart(document.getElementById("subChart"),{
  type:'line',
  data:{
    labels:[],
    datasets:[
      {label:"Sub IN",data:[],borderColor:"green"},
      {label:"Sub OUT",data:[],borderColor:"red"}
    ]
  },
  options:{animation:false}
});

let mainTotal=0;
let subTotal=0;

ws.onopen=()=>console.log("Connected");
ws.onerror=()=>console.log("Error");
ws.onclose=()=>console.log("Disconnected");

ws.onmessage=function(e){

  let d=JSON.parse(e.data);

  // TANK
  tankText.innerHTML=d.tank+"%";
  tankFill.style.height=d.tank+"%";

  if(d.tank<25){
    tankAlert.innerHTML="⚠ LOW WATER";
    tankAlert.className="warn";
  }else{
    tankAlert.innerHTML="OK";
    tankAlert.className="ok";
  }

  // MOTOR
  if(d.motor=="ON"){
    motorIcon.className="motorIcon on";
    motorText.innerHTML="ON";
  }else{
    motorIcon.className="motorIcon off";
    motorText.innerHTML="OFF";
  }

  // MAIN
  m_in.innerHTML=d.m_in;
  m_out.innerHTML=d.m_out;

  if(d.m_status=="NORMAL"){
    m_status.innerHTML="NORMAL";
    m_status.className="ok";
    mainWarn.innerHTML="No Issues";
    mainWarn.className="alert ok";
  }
  else if(d.m_status=="THEFT"){
    m_status.innerHTML="⚠ THEFT";
    m_status.className="warn";
    mainWarn.innerHTML="⚠ Water Theft Detected";
    mainWarn.className="alert warn";
  }
  else{
    m_status.innerHTML="🚨 DAMAGE";
    m_status.className="leak";
    mainWarn.innerHTML="🚨 PIPE DAMAGE";
    mainWarn.className="alert leak";
  }

  // SUB
  s_in.innerHTML=d.s_in;
  s_out.innerHTML=d.s_out;

  if(d.s_status=="NORMAL"){
    s_status.innerHTML="NORMAL";
    s_status.className="ok";
    subWarn.innerHTML="No Issues";
    subWarn.className="alert ok";
  }
  else if(d.s_status=="LEAK"){
    s_status.innerHTML="⚠ LEAK";
    s_status.className="warn";
    subWarn.innerHTML="⚠ Minor Leak";
    subWarn.className="alert warn";
  }
  else{
    s_status.innerHTML="🚨 FULL DAMAGE";
    s_status.className="leak";
    subWarn.innerHTML="🚨 PIPE BROKEN";
    subWarn.className="alert leak";
  }

  // TOTAL FLOW
  mainTotal += d.m_out;
  subTotal += d.s_out;

  mainTotal = Math.max(0, mainTotal);
  subTotal = Math.max(0, subTotal);

  mainTotalEl.innerHTML = mainTotal.toFixed(2);
  subTotalEl.innerHTML = subTotal.toFixed(2);

  // GRAPH
  let t=new Date().toLocaleTimeString();

  mainChart.data.labels.push(t);
  mainChart.data.datasets[0].data.push(d.m_in);
  mainChart.data.datasets[1].data.push(d.m_out);

  subChart.data.labels.push(t);
  subChart.data.datasets[0].data.push(d.s_in);
  subChart.data.datasets[1].data.push(d.s_out);

  if(mainChart.data.labels.length>15){
    mainChart.data.labels.shift();
    mainChart.data.datasets.forEach(x=>x.data.shift());
    subChart.data.labels.shift();
    subChart.data.datasets.forEach(x=>x.data.shift());
  }

  mainChart.update();
  subChart.update();
};

</script>

</body>
</html>
