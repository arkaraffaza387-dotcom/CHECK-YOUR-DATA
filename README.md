<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cek Status Pendaftaran</title>
<style>
  body { font-family: sans-serif; background: #f4f4f9; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
  .card { background: white; padding: 30px; border-radius: 10px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); width: 100%; max-width: 400px; text-align: center; }
  h2 { margin-top: 0; color: #333; }
  input { width: 90%; padding: 12px; margin: 10px 0; border: 1px solid #ddd; border-radius: 5px; font-size: 16px; }
  button { width: 100%; padding: 12px; background: #007BFF; color: white; border: none; border-radius: 5px; font-size: 16px; cursor: pointer; font-weight: bold; }
  button:hover { background: #0056b3; }
  
  /* Hasil */
  .result-box { margin-top: 20px; text-align: left; display: none; background: #fafafa; padding: 15px; border-radius: 8px; border: 1px solid #eee; }
  .row { margin-bottom: 10px; display: flex; justify-content: space-between; border-bottom: 1px solid #e0e0e0; padding-bottom: 5px; }
  .row:last-child { border-bottom: none; }
  .label { font-weight: bold; color: #555; }
  .value { font-weight: bold; color: #000; text-align: right; }
  
  .success { color: green; }
  .fail { color: red; }
  .error { color: red; text-align: center; margin-top: 10px; display: none; }
</style>
</head>
<body>

<div class="card">
  <h2>Cek Status Pendaftaran</h2>
  <input type="email" id="emailInput" placeholder="Masukkan Email...">
  <button onclick="cekStatus()">CEK SEKARANG</button>
  
  <div id="errorMsg" class="error">Email tidak ditemukan!</div>

  <div id="resultBox" class="result-box">
    <div class="row">
      <span class="label">NAMA</span>
      <span class="value" id="outNama"></span>
    </div>
    <div class="row">
      <span class="label">VERTIKA</span>
      <span class="value" id="outVertika"></span>
    </div>
    <div class="row">
      <span class="label">STATUS</span>
      <span class="value" id="outStatus"></span>
    </div>
  </div>
</div>

<script>
  // DATABASE SEDERHANA DI DALAM HTML
  const database = [
    {
      email: "amba@gmail.com",
      nama: "AZFER.ID",
      vertika: "BERHASIL",
      status: "ADMIN + OWNER"
    },
    {
      email: "admin1@gmail.com",
      nama: "JASTEB ADMIN",
      vertika: "GAGAL",
      status: "GAGAL"
    },
    {
      email: "admin2@gmail.com",
      nama: "ARKA GAMES",
      vertika: "BERHASL",
      status: "ADMIN"
    }
  ];

  function cekStatus() {
    const inputEmail = document.getElementById('emailInput').value.toLowerCase().trim();
    const resultBox = document.getElementById('resultBox');
    const errorMsg = document.getElementById('errorMsg');
    
    // Reset tampilan
    resultBox.style.display = 'none';
    errorMsg.style.display = 'none';

    if (!inputEmail) {
      alert("Masukkan email terlebih dahulu!");
      return;
    }

    // Cari data
    const user = database.find(u => u.email === inputEmail);

    if (user) {
      // Jika ditemukan
      document.getElementById('outNama').innerText = user.nama;
      
      const vertikaEl = document.getElementById('outVertika');
      vertikaEl.innerText = user.vertika;
      vertikaEl.className = 'value ' + (user.vertika === 'BERHASIL' ? 'success' : 'fail');

      document.getElementById('outStatus').innerText = user.status;
      
      resultBox.style.display = 'block';
    } else {
      // Jika tidak ditemukan
      errorMsg.style.display = 'block';
    }
  }
</script>

</body>
</html>
