<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dasterku</title>
<style>
body{font-family:Arial;margin:0;background:#f7f3ee}
header{background:#e8dccb;padding:15px;text-align:center;font-size:22px;font-weight:bold}
.container{padding:15px}
.card{background:#fff;border-radius:10px;padding:10px;margin-bottom:12px}
.row{display:flex;justify-content:space-between;align-items:center}
button{background:#c6a87d;border:none;padding:8px 12px;border-radius:6px;color:#fff}
select,input{padding:6px;width:100%;margin-top:5px}
.total{font-size:18px;font-weight:bold}
.checkout{position:fixed;bottom:0;left:0;right:0;background:#fff;padding:10px;border-top:1px solid #ddd}
</style>
</head>
<body>

<header>🧺 Dasterku</header>

<div class="container" id="produk"></div>

<div class="checkout">
<textarea id="catatan" placeholder="Catatan pembeli..." style="width:100%"></textarea>
<p class="total">Total: Rp <span id="total">0</span></p>
<button onclick="checkout()">Chat Admin WhatsApp</button>
</div>

<script>
const wa = "6281234567890"; // GANTI NOMOR WA KAMU
const produk = [
 {nama:"Daster Mawar",harga:45000},
 {nama:"Daster Santai",harga:48000},
 {nama:"Daster Harian",harga:42000},
 {nama:"Daster Premium",harga:55000}
];

let total = 0;

function render(){
 const el = document.getElementById("produk");
 produk.forEach((p,i)=>{
  el.innerHTML += `
  <div class="card">
   <b>${p.nama}</b><br>Rp ${p.harga}
   <select id="u${i}">
    <option>S</option><option>M</option><option>L</option><option>XL</option>
   </select>
   <div class="row">
    <input type="number" id="q${i}" value="0" min="0" onchange="hitung()">
   </div>
  </div>`;
 });
}

function hitung(){
 total = 0;
 produk.forEach((p,i)=>{
  total += p.harga * (parseInt(document.getElementById("q"+i).value)||0);
 });
 document.getElementById("total").innerText = total.toLocaleString();
}

function checkout(){
 let pesan = "Halo Admin Dasterku%0A%0APesanan:%0A";
 produk.forEach((p,i)=>{
  let q = document.getElementById("q"+i).value;
  if(q>0){
   pesan += `- ${p.nama} (${document.getElementById("u"+i).value}) x${q}%0A`;
  }
 });
 pesan += `%0ATotal: Rp ${total.toLocaleString()}%0A`;
 pesan += `Catatan: ${document.getElementById("catatan").value}`;
 window.open(`https://wa.me/${wa}?text=${pesan}`);
}

render();
</script>

</body>
</html>
