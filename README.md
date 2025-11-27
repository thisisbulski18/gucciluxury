<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gucci Agenda</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="">
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&amp;family=Inter:wght@300;400;500;600&amp;display=swap" rel="stylesheet">
    
    <script>
      tailwind.config = {
        theme: {
          extend: {
            fontFamily: { serif: ['Cinzel', 'serif'], sans: ['Inter', 'sans-serif'] },
            colors: { 'gucci-gold': '#d4af37', 'gucci-gold-dark': '#bfa030' }
          }
        }
      }
    </script>
    <style>
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .animate-fadeIn { animation: fadeIn 0.6s ease-out forwards; }
        .hidden { display: none !important; }
    </style>
</head>
<body class="bg-white font-sans text-black selection:bg-gray-200 flex flex-col min-h-screen">

    <!-- HEADER -->
    <header class="bg-white sticky top-0 z-40 border-b border-gray-100">
        <div class="flex items-center justify-between px-4 py-4 md:px-8 relative bg-white">
            <div class="text-3xl tracking-[0.2em] font-serif font-bold text-black cursor-default select-none">GUCCI</div>
            <div class="flex items-center space-x-5 text-black">
                <!-- Indikator Level (Pojok Kanan) -->
                <div id="level-indicator" class="text-xs font-bold border border-black px-3 py-1 rounded-full uppercase tracking-widest">
                    LEVEL 1
                </div>
            </div>
        </div>
    </header>

    <main class="flex-grow max-w-4xl mx-auto px-4 md:px-8 pt-2 w-full relative">
        
        <!-- VIEW: DAFTAR PRODUK -->
        <div id="product-list-view" class="animate-fadeIn">
            <!-- Judul Halaman -->
            <div class="text-center mb-8 mt-4">
                <h1 id="agenda-title" class="text-2xl font-bold font-serif tracking-widest mb-6 uppercase">AGENDA 1</h1>
                <div class="max-w-md mx-auto px-4">
                    <h2 id="benefit-title" class="text-xl font-bold uppercase tracking-widest mb-2 text-black">BENEFIT 20%</h2>
                    <p class="text-xs md:text-sm font-medium leading-relaxed text-gray-900">
                        Selesaikan konfirmasi untuk melanjutkan ke koleksi berikutnya.
                    </p>
                </div>
            </div>

            <!-- Grid Produk 2x2 -->
            <div id="product-grid" class="grid grid-cols-2 gap-x-3 gap-y-8 md:gap-x-8 md:gap-y-12 pb-12">
                <!-- Javascript akan memasukkan 4 produk di sini -->
            </div>
        </div>

        <!-- VIEW: KONFIRMASI ORDER -->
        <div id="confirmation-view" class="hidden animate-fadeIn pb-12">
            <div class="mb-8 mt-2">
                <button onclick="goBack()" class="flex items-center text-[10px] font-bold uppercase tracking-widest text-gray-500 hover:text-black transition-colors">
                    <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="mr-2"><path d="M19 12H5"/><path d="M12 19l-7-7 7-7"/></svg>
                    Pilih Ulang
                </button>
            </div>

            <div class="text-center mb-8">
                <h2 class="text-2xl font-serif font-bold uppercase tracking-widest mb-2">Order Confirmation</h2>
                <p class="text-xs text-gray-500">Konfirmasi pilihan Anda</p>
            </div>

            <div class="bg-gray-50 p-4 md:p-8 max-w-md mx-auto rounded-sm">
                <div class="bg-white p-6 mb-6 relative flex justify-center items-center aspect-square shadow-sm">
                    <div class="absolute top-0 left-0 bg-black text-white text-[10px] font-bold uppercase tracking-widest px-3 py-1.5">Selected</div>
                    <img id="conf-img" src="" alt="Selected Product" class="w-full h-full object-contain mix-blend-multiply">
                </div>
                <h3 id="conf-name" class="text-sm font-bold uppercase tracking-widest text-center mb-6 px-4">Product Name</h3>
                <div class="border-t border-gray-200 my-4"></div>
                <div class="space-y-3 text-xs font-medium tracking-wide">
                    <div class="flex justify-between items-center"><span class="text-gray-500 uppercase">Price</span><span id="conf-price" class="font-bold">IDR 0</span></div>
                    <div class="flex justify-between items-center"><span class="text-gray-500 uppercase">Benefit</span><span id="conf-benefit" class="text-green-700 font-bold">0%</span></div>
                </div>
                <div class="border-t border-gray-200 my-4"></div>
                <div class="flex justify-between items-center mb-8"><span class="text-sm font-bold uppercase tracking-widest">Total Profit</span><span id="conf-profit" class="text-sm font-bold">IDR 0</span></div>
                
                <!-- TOMBOL KONFIRMASI (Tanpa tulisan Next Level) -->
                <button onclick="confirmAndProgress()" class="w-full bg-black text-white text-[11px] font-bold uppercase tracking-[0.2em] py-4 hover:opacity-80 transition-all flex justify-center items-center gap-2">
                    <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"></polyline></svg>
                    CONFIRM ORDER
                </button>
            </div>
        </div>

        <!-- VIEW: SELESAI (GAME OVER) -->
        <div id="completed-view" class="hidden animate-fadeIn text-center pt-20">
             <div class="mb-6 flex justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" class="text-gucci-gold"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"></path></svg>
             </div>
             <h2 class="text-3xl font-serif font-bold uppercase tracking-widest mb-4">CONGRATULATIONS</h2>
             <p class="max-w-md mx-auto text-sm text-gray-600 mb-8 px-4">Anda telah menyelesaikan semua tahap Agenda. Silakan hubungi admin.</p>
             <button onclick="window.open('https://wa.me/628123456789', '_blank')" class="bg-gucci-gold text-black px-8 py-3 text-xs font-bold uppercase tracking-widest hover:bg-black hover:text-white transition-colors">
                 Contact Admin
             </button>
        </div>

    </main>

    <footer class="mt-auto px-4 pb-8 md:px-8 text-black border-t border-gray-100 pt-8">
        <p class="text-[10px] font-semibold text-gray-600 text-center">© 2016 - 2025 Guccio Gucci S.p.A. - All rights reserved.</p>
    </footer>

    <!-- LOGIC JAVASCRIPT -->
    <script>
        const img1 = "https://media.gucci.com/style/HEXFBFBFB_South_0_160_640x640/1758137467/860787_AAEE7_7702_001_100_0000_Light.jpg";
        const img2 = "https://media.theperfumeshop.com/medias/sys_master/prd-images/hd7/h0a/10141209788446/prd-front-1318338_420x420/gucci-flora-gorgeous-orchid-eau-de-parfum-gift-set-420x420.jpg";
        const img3 = "https://media.gucci.com/style/HEXFBFBFB_South_0_160_640x640/1747845099/847090_FAEUC_9758_001_065_0000_Light.jpg";
        const img4 = "https://media.gucci.com/style/HEXFBFBFB_South_0_160_640x640/1758728705/857595_FAFUF_9870_001_085_0000_Light.jpg";
        const img5 = "https://media.gucci.com/style/HEXFBFBFB_South_0_160_640x640/1744218003/497985_AAE5F_1642_001_100_0000_Light.jpg";

        const database = {
            1: [ 
                { name: "Gucci Half Horsebit Mini", price: 100000, img: img1 },
                { name: "Gucci Flora Orchid Set", price: 300000, img: img2 },
                { name: "GG Emblem Nano Bucket", price: 550000, img: img3 },
                { name: "Ophidia Boston Bag", price: 890000, img: img4, recommended: true }
            ],
            2: [ 
                { name: "Gucci Signature Belt", price: 1500000, img: img5 },
                { name: "Ophidia GG Card Case", price: 2100000, img: img1 },
                { name: "Gucci Savoy Duffle Mini", price: 2800000, img: img3 },
                { name: "GG Retro Sunglasses", price: 3500000, img: img4, recommended: true }
            ],
            3: [ 
                { name: "Ace Embroidered Sneaker", price: 5500000, img: img3 },
                { name: "Gucci Diana Mini Tote", price: 6200000, img: img4 },
                { name: "Jackie 1961 Shoulder Bag", price: 7800000, img: img1 },
                { name: "Dionysus Small Bag", price: 9000000, img: img5, recommended: true }
            ],
            4: [ 
                { name: "Gucci Bamboo 1947", price: 12500000, img: img4 },
                { name: "Attache Large Shoulder", price: 15000000, img: img2 },
                { name: "Gucci Horsebit 1955", price: 18500000, img: img5 },
                { name: "Exotic Leather Tote", price: 22000000, img: img1, recommended: true }
            ],
            5: [ 
                { name: "Gold Chain Necklace", price: 45000000, img: img2 },
                { name: "Diamond Watch Series", price: 65000000, img: img5 },
                { name: "Crocodile Horsebit Bag", price: 85000000, img: img3 },
                { name: "Gucci High Jewelry Set", price: 120000000, img: img4, recommended: true }
            ]
        };

        function formatRupiah(num) {
            return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
        }

        let currentLevel = 1;
        let currentProduct = {};
        const maxLevel = 5;

        // FUNGSI RENDER HALAMAN UTAMA
        function loadLevel(level) {
            if (level > maxLevel) {
                showCompletionScreen();
                return;
            }

            const items = database[level];
            const grid = document.getElementById('product-grid');
            
            // Update Teks
            document.getElementById('agenda-title').innerText = `AGENDA ${level}`;
            document.getElementById('level-indicator').innerText = `LEVEL ${level}`;
            document.getElementById('benefit-title').innerText = level >= 3 ? "BENEFIT 30%" : "BENEFIT 20%";
            
            grid.innerHTML = '';

            items.forEach((item, index) => {
                const benefitPercent = level >= 3 ? 0.3 : 0.2;
                const profitAmount = Math.floor(item.price * (1 + benefitPercent));
                
                const btnColorClass = item.recommended 
                    ? "bg-gucci-gold text-black hover:bg-black hover:text-white" 
                    : "bg-black text-white hover:opacity-80";
                const btnText = item.recommended ? "Pilih • Recommended" : "Pilih";
                const badgeHtml = item.recommended ? `<div class="absolute top-0 right-0 z-20 bg-black text-white text-[9px] font-bold uppercase tracking-widest px-2 py-1.5 shadow-md flex items-center gap-1"><svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="white" stroke="currentColor" stroke-width="2"><path d="M11.525 2.295a.53.53 0 0 1 .95 0l2.31 4.679a2.123 2.123 0 0 0 1.595 1.16l5.166.756a.53.53 0 0 1 .294.904l-3.736 3.638a2.123 2.123 0 0 0-.611 1.878l.882 5.14a.53.53 0 0 1-.771.56l-4.618-2.428a2.122 2.122 0 0 0-1.973 0L6.396 21.01a.53.53 0 0 1-.77-.56l.881-5.139a2.122 2.122 0 0 0-.611-1.879L2.16 9.795a.53.53 0 0 1 .294-.906l5.165-.755a2.122 2.122 0 0 0 1.597-1.16z"></path></svg>Recommended</div>` : '';

                const cardHTML = `
                <div class="flex flex-col w-full h-full justify-between relative group">
                    <div class="cursor-pointer">
                        <div class="relative w-full aspect-square bg-[#f5f5f5] flex items-center justify-center mb-4 overflow-hidden rounded-sm">
                            <div class="absolute top-4 left-4 w-8 h-8 bg-white rounded-full flex items-center justify-center text-sm font-bold shadow-sm z-10 font-sans text-black">${index + 1}</div>
                            ${badgeHtml}
                            <img src="${item.img}" class="w-full h-full transition-transform duration-700 group-hover:scale-110 object-cover mix-blend-multiply">
                        </div>
                        <h3 class="text-xs font-bold uppercase tracking-wide text-black mb-3 leading-4">${item.name}</h3>
                        <div class="grid grid-cols-[auto_12px_1fr] gap-y-0.5 text-[11px] font-medium text-black leading-loose mb-5">
                            <span>IDR price</span><span class="text-center">:</span><span>${formatRupiah(item.price)}</span>
                            <span>Benefit</span><span class="text-center">:</span><span class="${item.recommended ? 'text-green-700 font-bold' : ''}">${benefitPercent * 100}%</span>
                            <span>IDR profit</span><span class="text-center">:</span><span>${formatRupiah(profitAmount)}</span>
                        </div>
                    </div>
                    <button onclick="selectItem('${item.name}', '${formatRupiah(item.price)}', '${benefitPercent * 100}%', '${formatRupiah(profitAmount)}', '${item.img}')" 
                        class="w-full text-[10px] font-bold uppercase tracking-[0.2em] py-3 transition-colors duration-300 mt-auto ${btnColorClass}">
                        ${btnText}
                    </button>
                </div>
                `;
                grid.innerHTML += cardHTML;
            });

            document.getElementById('product-list-view').classList.remove('hidden');
            document.getElementById('confirmation-view').classList.add('hidden');
            document.getElementById('completed-view').classList.add('hidden');
            window.scrollTo(0, 0);
        }

        // FUNGSI KLIK PILIH
        function selectItem(name, price, benefit, profit, imgUrl) {
            currentProduct = { name, price, profit };

            document.getElementById('conf-name').innerText = name;
            document.getElementById('conf-price').innerText = 'IDR ' + price;
            document.getElementById('conf-benefit').innerText = benefit;
            document.getElementById('conf-profit').innerText = 'IDR ' + profit;
            document.getElementById('conf-img').src = imgUrl;

            document.getElementById('product-list-view').classList.add('hidden');
            document.getElementById('confirmation-view').classList.remove('hidden');
            window.scrollTo(0, 0);
        }

        // FUNGSI KEMBALI
        function goBack() {
            document.getElementById('confirmation-view').classList.add('hidden');
            document.getElementById('product-list-view').classList.remove('hidden');
        }

        // FUNGSI CONFIRM & AUTO NEXT LEVEL (TAPI TOMBOLNYA BIASA)
        function confirmAndProgress() {
            // 1. Buka WA
            const phoneNumber = "628123456789"; 
            const message = `Halo Admin, saya konfirmasi pesanan dari *AGENDA ${currentLevel}*:\n\n🛍️ Produk: ${currentProduct.name}\n💰 Harga: IDR ${currentProduct.price}\n✅ Total Profit: IDR ${currentProduct.profit}\n\nMohon diproses untuk lanjut ke level berikutnya.`;
            
            const url = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(message)}`;
            window.open(url, '_blank');

            // 2. Logic Naik Level
            currentLevel++;

            // 3. Tampilkan Alert & Pindah Halaman
            setTimeout(() => {
                alert("Konfirmasi Berhasil! Melanjutkan ke Agenda berikutnya...");
                loadLevel(currentLevel);
            }, 1000);
        }

        function showCompletionScreen() {
            document.getElementById('product-list-view').classList.add('hidden');
            document.getElementById('confirmation-view').classList.add('hidden');
            document.getElementById('completed-view').classList.remove('hidden');
            document.getElementById('level-indicator').innerText = "DONE";
            window.scrollTo(0, 0);
        }

        // Mulai
        loadLevel(1);

    </script>

</body>
</html>
