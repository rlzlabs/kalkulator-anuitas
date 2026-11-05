# kalkulator-anuitas
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

        /* Neumorphism Background */
        body {
            background-color: #e0e5ec;
            color: #4d5b6b;
            padding: 30px 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
        }

        .container {
            max-width: 850px;
            width: 100%;
        }

        h1 {
            text-align: center;
            margin-bottom: 30px;
            color: #3182ce;
            font-weight: 700;
            letter-spacing: 1px;
            text-shadow: 2px 2px 4px rgba(163,177,198,0.5), -2px -2px 4px rgba(255,255,255,0.8);
        }

        /* 3D Extruded Card Effect */
        .neu-card {
            background-color: #e0e5ec;
            border-radius: 20px;
            box-shadow: 9px 9px 16px rgba(163,177,198,0.6), 
                       -9px -9px 16px rgba(255,255,255, 0.6);
            padding: 30px;
            margin-bottom: 30px;
        }

        /* Biodata Text */
        .identitas h2 {
            color: #3182ce;
            margin-bottom: 15px;
        }
        .identitas p, .identitas li {
            color: #4d5b6b;
            margin-bottom: 10px;
        }
        .identitas ul {
            list-style-position: inside;
            margin-top: 10px;
        }

        /* Form Inputs (3D Inset/Deboss Effect) */
        .input-group {
            margin-bottom: 25px;
        }
        .input-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            font-size: 14px;
            color: #64748b;
        }
        .input-group input {
            width: 100%;
            padding: 16px;
            background-color: #e0e5ec;
            border: none;
            border-radius: 12px;
            color: #2d3748;
            font-size: 16px;
            font-weight: 500;
            box-shadow: inset 6px 6px 10px 0 rgba(163,177,198, 0.7), 
                        inset -6px -6px 10px 0 rgba(255,255,255, 0.8);
            outline: none;
        }
        .input-group input::placeholder {
            color: #94a3b8;
        }

        /* 3D Button */
        button {
            width: 100%;
            padding: 18px;
            background-color: #e0e5ec;
            color: #3182ce;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 700;
            letter-spacing: 1px;
            cursor: pointer;
            box-shadow: 6px 6px 10px 0 rgba(163,177,198, 0.7), 
                       -6px -6px 10px 0 rgba(255,255,255, 0.8);
            transition: all 0.2s ease-in-out;
            margin-top: 10px;
        }
        /* Efek saat tombol ditekan (masuk ke dalam) */
        button:active {
            box-shadow: inset 6px 6px 10px 0 rgba(163,177,198, 0.7), 
                        inset -6px -6px 10px 0 rgba(255,255,255, 0.8);
            color: #2b6cb0;
        }

        /* Result Area */
        .hidden {
            display: none;
        }
        .result-card h2 {
            text-align: center;
            color: #3182ce;
            margin-bottom: 25px;
        }
        .table-responsive {
            overflow-x: auto;
            border-radius: 12px;
            box-shadow: inset 4px 4px 8px rgba(163,177,198, 0.5), 
                        inset -4px -4px 8px rgba(255,255,255, 0.7);
            padding: 10px;
        }

        /* Table Design */
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 14px;
        }
        th, td {
            padding: 15px;
            text-align: right;
            border-bottom: 1px solid rgba(163,177,198, 0.3);
        }
        th:first-child, td:first-child {
            text-align: center;
        }
        th {
            color: #3182ce;
            font-weight: 700;
            border-bottom: 2px solid rgba(163,177,198, 0.5);
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
        <div class="neu-card identitas">
            <h2>Tugas Akhir Semester 3</h2>
            <p>Pelajaran: <strong>Matematika</strong></p>
            <p>Materi: <strong>Anuitas</strong></p>
            <p>Kelas: <strong>XI-5</strong></p>
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
        <div class="neu-card">
            <div class="input-group">
                <label>JUMLAH PINJAMAN / MODAL (Rp)</label>
                <input type="number" id="pinjaman" placeholder="Contoh: 10000000">
            </div>
            <div class="input-group">
                <label>SUKU BUNGA PER BULAN (%)</label>
                <input type="number" id="bunga" placeholder="Contoh: 2">
            </div>
            <div class="input-group">
                <label>TENOR / JANGKA WAKTU (Bulan)</label>
                <input type="number" id="tenor" placeholder="Contoh: 12">
            </div>
            <button onclick="hitungAnuitas()">HITUNG ANUITAS</button>
        </div>

        <!-- Tabel Hasil -->
        <div id="result-section" class="neu-card hidden">
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
