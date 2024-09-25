<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PALM STORE</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: #fff;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
        }
        .logo {
            text-align: center;
            margin-bottom: 20px;
        }
        .logo img {
            max-width: 100px; /* Ukuran logo diperkecil */
        }
        .form-group {
            margin-bottom: 10px; /* Margin dikurangi */
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-size: 12px; /* Ukuran font diperkecil */
        }
        .form-group input, .form-group select {
            width: 100%;
            padding: 8px; /* Padding diperkecil */
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 12px; /* Ukuran font input diperkecil */
        }
        button {
            background-color: #28a745;
            color: white;
            padding: 8px 12px; /* Padding tombol diperkecil */
            border: none;
            border-radius: 5px;
            font-size: 12px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        .receipt {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            background: #fafafa;
            font-size: 12px; /* Ukuran font di area kwitansi diperkecil */
        }
        .receipt h3 {
            margin-bottom: 5px;
            font-size: 14px; /* Ukuran heading kwitansi */
        }
        .invoice-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        .invoice-header img {
            max-width: 100px; /* Ukuran logo diperkecil */
        }
        .invoice-details {
            margin-top: 10px;
            width: 100%;
            font-size: 12px;
        }
        .invoice-details th, .invoice-details td {
            padding: 6px; /* Padding tabel diperkecil */
            border: 1px solid #ccc;
            text-align: left;
        }
        .invoice-details th {
            background-color: #f4f4f4;
        }
        .total {
            text-align: right;
            font-size: 14px; /* Ukuran font total diperkecil */
            font-weight: bold;
            padding-right: 10px;
        }
        .change {
            text-align: right;
            font-size: 14px; /* Ukuran font kembalian diperkecil */
            font-weight: bold;
            padding-right: 10px;
        }

        /* CSS untuk mode cetak */
        @media print {
            @page {
                size: A5 portrait;
                margin: 0.1cm; /* Margin lebih kecil */
            }
            body * {
                visibility: hidden;
            }
            .receipt, .receipt * {
                visibility: visible;
            }
            .receipt {
                position: absolute;
                top: 0;
                left: 0;
                width: 96%;
            }
            button {
                display: none;
            }
        }

        /* CSS Responsive */
        @media (max-width: 768px) {
            .invoice-header {
                flex-direction: column;
                text-align: center;
            }
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Sistem Pembayaran</h1>

    <div class="logo">
        <img src="palm.JPG" alt="Logo Perusahaan">
    </div>

    <form id="paymentForm">
        <div class="form-group">
            <label for="companyName">Nama Toko</label>
            <input type="text" id="companyName" value="PALM STORE" disabled>
        </div>

        <div class="form-group">
            <label for="invoiceNumber">Nomor Invoice</label>
            <input type="text" id="invoiceNumber" value="" disabled>
        </div>

        <div class="form-group">
            <label for="name">Nama Pemesan</label>
            <input type="text" id="name" name="name" required>
        </div>

        <div class="form-group">
            <label for="date">Hari/Tanggal</label>
            <input type="text" id="date" value="" disabled>
        </div>

        <div class="form-group">
            <label for="description">Keterangan Barang yang Dipesan</label>
            <input type="text" id="description" placeholder="Contoh: Kaos Always Monday, Arang Briket, Rokok Palm" required>
        </div>

        <div class="form-group">
            <label for="quantity">Jumlah Barang</label>
            <input type="number" id="quantity" name="quantity" required>
        </div>

        <div class="form-group">
            <label for="amount">Harga per Barang (Rp)</label>
            <input type="number" id="amount" name="amount" required>
        </div>

        <div class="form-group">
            <label for="paymentMethod">Metode Pembayaran</label>
            <select id="paymentMethod" name="paymentMethod" required>
                <option value="Transfer Bank">Transfer Bank</option>
                <option value="Dompet Digital">Dompet Digital</option>
                <option value="Cash">Cash</option>
            </select>
        </div>

        <div class="form-group" id="bankSelection" style="display: none;">
            <label for="bank">Pilih Bank</label>
            <select id="bank" name="bank">
                <option value="BCA 5170474149 ( Rizky Amanda )">BCA 5170474149 ( Rizky Amanda )</option>
                <option value="Bank B">BNI</option>
                <option value="Bank C">BRI</option>
                <option value="Bank D">MANDIRI</option>
            </select>
        </div>

        <div class="form-group" id="walletSelection" style="display: none;">
            <label for="wallet">Pilih Dompet Digital</label>
            <select id="wallet" name="wallet">
                <option value="Dompet Digital A">DANA</option>
                <option value="Dompet Digital B">OVO</option>
                <option value="Dompet Digital C">BIT COIN</option>
            </select>
        </div>

        <div class="form-group" id="paidAmountGroup" style="display: none;">
            <label for="paidAmount">Jumlah Uang Pembayaran (Rp)</label>
            <input type="number" id="paidAmount" name="paidAmount">
        </div>

        <div class="total" id="totalPayment" style="display:none;">
            <strong>Total Pembayaran: Rp <span id="totalAmount"></span></strong>
        </div>

        <button type="submit">Bayar</button>
    </form>

    <div class="receipt" id="receipt" style="display: none;">
        <div class="invoice-header">
            <h3>Kwitansi Pembayaran</h3>
            <img src="palm.JPG" alt="Logo Perusahaan">
        </div>

        <p><strong>Nama Toko:</strong> PALM STORE</p>
        <p><strong>Nomor Invoice:</strong> <span id="receiptInvoiceNumber"></span></p> <!-- Menambahkan nomor invoice -->
        <p><strong>Hari/Tanggal:</strong> <span id="receiptDate"></span></p>
        <p><strong>Nama Pemesan:</strong> <span id="receiptName"></span></p>

        <table class="invoice-details">
            <thead>
                <tr>
                    <th>Keterangan Barang</th>
                    <th>Jumlah</th>
                    <th>Harga per Barang (Rp)</th>
                    <th>Total (Rp)</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><span id="receiptDescription"></span></td>
                    <td><span id="receiptQuantity"></span></td>
                    <td>Rp <span id="receiptAmount"></span></td>
                    <td>Rp <span id="receiptTotal"></span></td>
                </tr>
            </tbody>
        </table>

        <p class="total">Total Pembayaran: Rp <span id="receiptTotalFinal"></span></p>
        <p class="change">Kembalian: Rp <span id="receiptChange"></span></p>
        <p><strong>Metode Pembayaran:</strong> <span id="receiptPaymentMethod"></span></p>
        <p><strong>Bank:</strong> <span id="receiptBank"></span></p> <!-- Menampilkan bank yang dipilih -->
        <p><strong>Dompet Digital:</strong> <span id="receiptWallet"></span></p> <!-- Menampilkan dompet digital yang dipilih -->

        <button onclick="printReceipt()">Print Kwitansi</button>
    </div>
</div>

<script>
    function generateInvoiceNumber() {
        const date = new Date();
        return 'INV-' + date.getFullYear() + (date.getMonth() + 1).toString().padStart(2, '0') + date.getDate().toString().padStart(2, '0') + '-' + Math.floor(Math.random() * 10000);
    }

    // Mengupdate total pembayaran
    function updateTotalPayment() {
        const quantity = document.getElementById('quantity').value;
        const amount = document.getElementById('amount').value;
        const total = quantity * amount;
        document.getElementById('totalAmount').textContent = total;
        document.getElementById('totalPayment').style.display = 'block';
    }

    // Fungsi untuk mencetak kwitansi
    function printReceipt() {
        window.print();
    }

    // Event listener untuk menampilkan pilihan bank dan dompet digital
    document.getElementById('paymentMethod').addEventListener('change', function() {
        const bankSelection = document.getElementById('bankSelection');
        const walletSelection = document.getElementById('walletSelection');
        const paidAmountGroup = document.getElementById('paidAmountGroup');

        if (this.value === 'Transfer Bank') {
            bankSelection.style.display = 'block';
            walletSelection.style.display = 'none';
            paidAmountGroup.style.display = 'none'; // Menyembunyikan input jumlah uang pembayaran
        } else if (this.value === 'Dompet Digital') {
            walletSelection.style.display = 'block';
            bankSelection.style.display = 'none';
            paidAmountGroup.style.display = 'none'; // Menyembunyikan input jumlah uang pembayaran
        } else {
            bankSelection.style.display = 'none';
            walletSelection.style.display = 'none';
            paidAmountGroup.style.display = 'block'; // Menampilkan input jumlah uang pembayaran untuk Kartu Kredit
        }
    });

    // Event listener untuk memperbarui total pembayaran saat input berubah
    document.getElementById('paymentForm').addEventListener('input', updateTotalPayment);

    document.getElementById('paymentForm').addEventListener('submit', function(event) {
        event.preventDefault(); // Menghentikan form dari pengiriman

        const name = document.getElementById('name').value;
        const description = document.getElementById('description').value;
        const quantity = document.getElementById('quantity').value;
        const amount = document.getElementById('amount').value;
        const paymentMethod = document.getElementById('paymentMethod').value;
        const paidAmount = document.getElementById('paidAmount').value;
        const bank = document.getElementById('bank').value; // Mendapatkan bank yang dipilih
        const wallet = document.getElementById('wallet').value; // Mendapatkan dompet digital yang dipilih
        const total = quantity * amount;
        const change = paidAmount - total;

        // Dapatkan tanggal sekarang
        const today = new Date().toLocaleDateString();

        // Tampilkan kwitansi
        const invoiceNumber = generateInvoiceNumber(); // Menghasilkan nomor invoice
        document.getElementById('invoiceNumber').value = invoiceNumber;
        document.getElementById('receiptInvoiceNumber').textContent = invoiceNumber; // Tampilkan nomor invoice di kwitansi
        document.getElementById('receiptName').textContent = name;
        document.getElementById('receiptDescription').textContent = description;
        document.getElementById('receiptQuantity').textContent = quantity;
        document.getElementById('receiptAmount').textContent = amount;
        document.getElementById('receiptTotal').textContent = total;
        document.getElementById('receiptTotalFinal').textContent = total;
        document.getElementById('receiptPaymentMethod').textContent = paymentMethod;
        document.getElementById('receiptChange').textContent = change >= 0 ? change : 0; // Tampilkan kembalian
        document.getElementById('receiptDate').textContent = today;
        document.getElementById('receiptBank').textContent = paymentMethod === "Transfer Bank" ? bank : ""; // Tampilkan bank yang dipilih di kwitansi jika Transfer Bank
        document.getElementById('receiptWallet').textContent = paymentMethod === "Dompet Digital" ? wallet : ""; // Tampilkan dompet digital yang dipilih di kwitansi jika Dompet Digital
        document.getElementById('date').value = today;

        // Tampilkan kwitansi
        document.getElementById('receipt').style.display = 'block';
    });
</script>

</body>
</html>
