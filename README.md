<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator Anuitas - Kelompok 8</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        /* Tema Galaxy / Claude Dark Mode */
        body {
            background-color: #0a0a0f;
            /* Pola Bintang di Latar Belakang */
            background-image: 
                radial-gradient(1px 1px at 20px 30px, rgba(255, 255, 255, 0.8) 100%, transparent),
                radial-gradient(1.5px 1.5px at 80px 70px, rgba(255, 255, 255, 0.9) 100%, transparent),
                radial-gradient(1px 1px at 150px 140px, rgba(255, 255, 255, 0.6) 100%, transparent),
                radial-gradient(2px 2px at 250px 90px, rgba(200, 220, 255, 0.9) 100%, transparent);
            background-size: 300px 300px;
            color: #e2e8f0;
            padding: 40px 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            position: relative;
            z-index: 1;
            overflow-x: hidden;
        }

        /* Efek Nebula (Cahaya kosmik ungu & biru di sudut) */
        body::before {
            content: "";
            position: fixed;
            top: -20%; left: -10%; width: 50vw; height: 50vw;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(110, 86, 207, 0.15) 0%, transparent 70%);
            filter: blur(60px);
            z-index: -1;
        }
        body::after {
            content: "";
            position: fixed;
            bottom: -20%; right: -10%; width: 50vw; height: 50vw;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(56, 189, 248, 0.12) 0%, transparent 70%);
            filter: blur(60px);
            z-index: -1;
        }

        .container {
            max-width: 850px;
            width: 100%;
            position: relative;
            z-index: 2;
        }

        h1 {
            text-align: center;
            margin-bottom: 35px;
            background: linear-gradient(135deg, #e0e7ff 0%, #a5b4fc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: 600;
            letter-spacing: 2px;
            font-size: 32px;
        }

        /* Kaca Gelap (Dark Glassmorphism) */
        .glass-card {
            background: rgba(20, 20, 25, 0.6);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            padding: 35px;
            margin-bottom: 30px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5), inset 0 1px 0 rgba(255, 255, 255, 0.1);
        }

        /* Teks Identitas */
        .identitas h2 {
            color: #c7d2fe;
            margin-bottom: 15px;
            font-weight: 500;
            font-size: 22px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 10px;
        }
        .identitas p {
            color: #94a3b8;
            margin-bottom: 8px;
            font-size: 15px;
        }
        .identitas strong {
            color: #e2e8f0;
            font-weight: 500;
        }
        .identitas ul {
            list-style: none;
            margin-top: 15px;
        }
        .identitas li {
            color: #e2e8f0;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }
        .identitas li::before {
            content: "✦";
            color: #818cf8;
            font-size: 14px;
            margin-right: 10px;
            text-shadow: 0 0 10px rgba(129, 140, 248, 0.8);
        }

        /* Form Input */
        .input-group {
            margin-bottom: 25px;
        }
        .input-group label {
            display: block;
            margin-bottom: 10px;
            font-size: 13px;
            color: #94a3b8;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
        }
        .input-group input {
            width: 100%;
            padding: 16px;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 12px;
            color: #fff;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        .input-group input:focus {
            outline: none;
            border-color: #818cf8;
            background: rgba(0, 0, 0, 0.6);
            box-shadow: 0 0 0 3px rgba(129, 140, 248, 0.2);
        }
        .input-group input::placeholder {
            color: #475569;
        }

        /* Tombol Elegan bercahaya */
        button {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%);
            color: #ffffff;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            letter-spacing: 1px;
            cursor: pointer;
            box-shadow: 0 8px 25px rgba(99, 102, 241, 0.4), inset 0 1px 0 rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
            margin-top: 10px;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(99, 102, 241, 0.6), inset 0 1px 0 rgba(255, 255, 255, 0.2);
        }
        button:active {
            transform: translateY(1px);
        }

        /* Area Hasil */
        .hidden {
            display: none;
        }
        .result-card h2 {
            text-align: center;
            color: #c7d2fe;
            margin-bottom: 25px;
            font-weight: 500;
        }
        .table-responsive {
            overflow-x: auto;
        }

        /* Desain Tabel Kosmik */
        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            font-size: 14px;
        }
        th, td {
            padding: 16px;
            text-align: right;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        th:first-child, td:first-child {
            text-align: center;
        }
        th {
            color: #818cf8;
            font-weight: 600;
            text-transform: uppercase;
            font-size: 12px;
            letter-spacing: 1px;
            background: rgba(0, 0, 0, 0.2);
        }
        /* Efek hover pada baris tabel */
        tr:hover td {
            background: rgba(255, 255, 255, 0.03);
        }
        tr:last-child td {
            border-bottom: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>KALKULATOR ANUITAS</h1>

        <!-- Bagian Identitas Kelompok 8 -->
        <div class="glass-card identitas">
            <h2>Laporan Tugas Anuitas</h2>
            <p>Pelajaran: <strong>Matematika</strong></p>
            <p>Materi: <strong>Anuitas</strong></p>
            <p>Kelas: <strong>XI-3</strong></p>
            <p>Guru Pembimbing: <strong>Dewi Lestari, S.Pd.</strong></p>
            <br>
            <p><strong>Anggota Kelompok 8:</strong></p>
            <ul>
                <li>Almira Yudhantara Sasmita</li>
                <li>Ghani Khadyan Khairi</li>
                <li>Shafa Shafiyyah Syahidah</li>
                <li>Syifa Aulia Noor Basith</li>
                <li>Tuanku Iman Semesta Sigand</li>
            </ul>
        </div>

        <!-- Form Input -->
        <div class="glass-card">
            <div class="input-group">
                <label>Jumlah Pinjaman / Modal (Rp)</label>
                <input type="number" id="pinjaman" placeholder="Contoh: 10000000">
            </div>
            <div class="input-group">
                <label>Suku Bunga Per Bulan (%)</label>
                <input type="number" id="bunga" placeholder="Contoh: 2">
            </div>
            <div class="input-group">
                <label>Tenor / Jangka Waktu (Bulan)</label>
                <input type="number" id="tenor" placeholder="Contoh: 12">
            </div>
            <button onclick="hitungAnuitas()">HITUNG ANUITAS</button>
        </div>

        <!-- Tabel Hasil -->
        <div id="result-section" class="glass-card hidden">
            <h2>Besar Anuitas: <span id="hasil-anuitas"></span></h2>
            <div class="table-responsive">
                <table id="tabel-angsuran">
                    <thead>
                        <tr>
                            <th>Bulan</th>
                            <th>Pinjaman Awal</th>
                            <th>Bunga</th>
                            <th>Angsuran Pokok</th>
                            <th>Sisa Pinjaman</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Logika JavaScript -->
    <script>
        function hitungAnuitas() {
            const pinjaman = parseFloat(document.getElementById('pinjaman').value);
            const bungaPersen = parseFloat(document.getElementById('bunga').value);
            const tenor = parseInt(document.getElementById('tenor').value);

            if (isNaN(pinjaman) || isNaN(bungaPersen) || isNaN(tenor) || pinjaman <= 0 || bungaPersen <= 0 || tenor <= 0) {
                alert("Harap masukkan angka yang valid dan lebih dari 0");
                return;
            }

            const i = bungaPersen / 100;
            const anuitas = (pinjaman * i) / (1 - Math.pow(1 + i, -tenor));

            document.getElementById('hasil-anuitas').innerText = formatRupiah(anuitas);
            document.getElementById('result-section').classList.remove('hidden');

            const tbody = document.querySelector('#tabel-angsuran tbody');
            tbody.innerHTML = '';

            let sisaPinjaman = pinjaman;

            for (let bulan = 1; bulan <= tenor; bulan++) {
                const bungaBulanIni = sisaPinjaman * i;
                const pokokBulanIni = anuitas - bungaBulanIni;
                let sisaAkhir = sisaPinjaman - pokokBulanIni;

                if (Math.abs(sisaAkhir) < 1) {
                    sisaAkhir = 0;
                }

                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${bulan}</td>
                    <td>${formatRupiah(sisaPinjaman)}</td>
                    <td>${formatRupiah(bungaBulanIni)}</td>
                    <td>${formatRupiah(pokokBulanIni)}</td>
                    <td>${formatRupiah(sisaAkhir)}</td>
                `;
                tbody.appendChild(tr);

                sisaPinjaman = sisaAkhir;
            }
        }

        function formatRupiah(angka) {
            return new Intl.NumberFormat('id-ID', { 
                style: 'currency', 
                currency: 'IDR' 
            }).format(angka);
        }
    </script>
</body>
</html>
