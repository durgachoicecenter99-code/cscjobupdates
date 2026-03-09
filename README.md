<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CSC Job Updates</title>

<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:Arial,Helvetica,sans-serif}

body{
background-image:url('logo-bg.png');
background-size:cover;
background-position:center;
background-attachment:fixed;
color:white;
}

/* overlay for readability */
body::before{
content:"";
position:fixed;
left:0;
right:0;
top:0;
bottom:0;
background:rgba(0,0,0,0.55);
z-index:-1;
}

header{
display:flex;
align-items:center;
justify-content:center;
gap:10px;
background:rgba(185,28,28,0.9);
padding:14px;
font-size:22px;
font-weight:bold;
backdrop-filter:blur(6px);
}

header img{
width:40px;
height:40px;
border-radius:50%;
}

.profile{
text-align:center;
padding:20px 10px;
}

.profile img{
width:120px;
height:120px;
border-radius:50%;
margin-bottom:10px;
box-shadow:0 0 20px rgba(255,255,255,0.3);
}

.container{
padding:14px;
max-width:540px;
margin:auto;
}

.sectionTitle{
margin-top:24px;
margin-bottom:10px;
font-size:16px;
color:#ffb4b4;
font-weight:bold;
}

.searchBox{
width:100%;
padding:12px;
border-radius:10px;
border:none;
margin-bottom:10px;
}

.filter{
display:grid;
grid-template-columns:1fr 1fr 1fr;
gap:8px;
margin-bottom:10px;
}

.filter button{
background:#ef4444;
border:none;
padding:8px;
color:white;
border-radius:8px;
font-size:12px;
cursor:pointer;
transition:0.25s;
}

.filter button:hover{
transform:scale(1.08);
background:#dc2626;
}

/* glass cards */
.card{
background:rgba(30,58,138,0.75);
border-radius:14px;
padding:16px;
margin-bottom:12px;
text-align:center;
transition:0.35s;
box-shadow:0 10px 25px rgba(0,0,0,0.6);
position:relative;
backdrop-filter:blur(6px);
}

.card:hover{
transform:translateY(-5px) scale(1.05);
background:rgba(29,78,216,0.85);
box-shadow:0 15px 35px rgba(0,0,0,0.7);
}

.card a{
text-decoration:none;
color:white;
font-size:15px;
font-weight:bold;
display:block;
}

.deleteBtn{
position:absolute;
right:10px;
top:10px;
background:#ef4444;
border:none;
color:white;
padding:4px 8px;
border-radius:6px;
font-size:12px;
cursor:pointer;
}

.social{
display:grid;
grid-template-columns:1fr 1fr 1fr;
gap:10px;
}

.button{
background:#ef4444;
padding:14px;
border-radius:12px;
text-align:center;
font-weight:bold;
transition:0.3s;
}

.button:hover{
transform:scale(1.07);
background:#dc2626;
}

.button a{
color:white;
text-decoration:none;
}

.adminLogin,.adminPanel{
background:rgba(2,6,23,0.8);
padding:15px;
border-radius:10px;
margin-top:20px;
backdrop-filter:blur(6px);
}

.adminPanel input, .adminPanel select{
width:100%;
padding:10px;
margin:6px 0;
border-radius:6px;
border:none;
}

.adminPanel button,.adminLogin button{
width:100%;
padding:10px;
background:#ef4444;
border:none;
color:white;
border-radius:6px;
font-weight:bold;
cursor:pointer;
}

footer{
text-align:center;
font-size:12px;
margin-top:35px;
padding:20px;
color:#ddd;
}

</style>
</head>

<body>

<header>
<img src="logo.png">
CSC JOB UPDATES
</header>

<div class="profile">
<img src="logo.png">
<div>@csc_job_updates</div>
</div>

<div class="container">

<div class="sectionTitle">Join Channels</div>

<div class="social">
<div class="button"><a href="https://whatsapp.com/channel/0029VaB2q8hH5JLrbc43ft42">WhatsApp</a></div>
<div class="button"><a href="https://instagram.com/csc_job_updates">Instagram</a></div>
<div class="button"><a href="https://www.youtube.com/channel/UCNTfyCDfc-KBqN-njLc5HAQ">YouTube</a></div>
</div>

<div class="sectionTitle">🔥 Latest Govt Job Feed</div>

<div class="card"><a href="https://www.freejobalert.com" target="_blank">Check Today Latest Government Jobs</a></div>

<div class="sectionTitle">Search Job Website</div>

<input class="searchBox" id="search" placeholder="Search job website..." onkeyup="searchJobs()">

<div class="filter">
<button onclick="filterCategory('all')">All</button>
<button onclick="filterCategory('railway')">Railway</button>
<button onclick="filterCategory('defence')">Defence</button>
<button onclick="filterCategory('bank')">Bank</button>
<button onclick="filterCategory('cg')">CG Jobs</button>
<button onclick="filterCategory('other')">Other</button>
</div>

<div class="sectionTitle">Government Job Websites</div>

<div id="jobs"></div>

<div class="sectionTitle">🔐 Admin Login</div>

<div class="adminLogin" id="loginBox">
<input type="password" id="adminPass" placeholder="Enter Admin Password">
<button onclick="loginAdmin()">Login</button>
</div>

<div class="adminPanel" id="adminPanel" style="display:none">
<input id="jobName" placeholder="Website Name">
<input id="jobLink" placeholder="Website Link">
<select id="jobCategory">
<option value="railway">Railway</option>
<option value="defence">Defence</option>
<option value="bank">Bank</option>
<option value="cg">CG Job</option>
<option value="other">Other</option>
</select>
<button onclick="addJob()">Add Link</button>
</div>

<footer>
© 2026 CSC Job Updates
</footer>

</div>

<script>

const adminPassword="Tanu@1206";
let isAdmin=false;
let currentFilter="all";

let jobs=[
{name:"India Post GDS",link:"https://indiapostgdsonline.gov.in",cat:"other"},
{name:"Railway RRB",link:"https://www.rrbcdg.gov.in",cat:"railway"},
{name:"Indian Army",link:"https://joinindianarmy.nic.in",cat:"defence"},
{name:"IBPS Bank Jobs",link:"https://www.ibps.in",cat:"bank"},
{name:"CGPSC",link:"https://psc.cg.gov.in",cat:"cg"},
{name:"CG Vyapam",link:"https://vyapam.cgstate.gov.in",cat:"cg"},
{name:"SSC",link:"https://ssc.nic.in",cat:"other"}
];

function renderJobs(){
const container=document.getElementById("jobs");
container.innerHTML="";

jobs.forEach((job,index)=>{
if(currentFilter!="all" && job.cat!==currentFilter) return;

const div=document.createElement("div");

div.className="card";

let del="";

if(isAdmin){

del=`<button class='deleteBtn' onclick='deleteJob(${index})'>Delete</button>`;

}


div.innerHTML=`${del}<a href="${job.link}" target="_blank">📌 ${job.name}</a>`;

container.appendChild(div);

});

}

function addJob(){

if(!isAdmin) return;

const name=document.getElementById("jobName").value;
const link=document.getElementById("jobLink").value;
const cat=document.getElementById("jobCategory").value;

if(name && link){

jobs.push({name:name,link:link,cat:cat});

renderJobs();

}

}

function deleteJob(index){

jobs.splice(index,1);

renderJobs();

}

function loginAdmin(){

const pass=document.getElementById("adminPass").value;

if(pass===adminPassword){

isAdmin=true;

document.getElementById("adminPanel").style.display="block";

document.getElementById("loginBox").style.display="none";

renderJobs();

}else{

alert("Wrong Password");

}

}

function searchJobs(){

const text=document.getElementById("search").value.toLowerCase();

const cards=document.querySelectorAll("#jobs .card");

cards.forEach(card=>{

if(card.innerText.toLowerCase().includes(text)){

card.style.display="block";

}else{

card.style.display="none";

}

});

}

function filterCategory(cat){

currentFilter=cat;

renderJobs();

}

renderJobs();

</script>

</body>
</html>
