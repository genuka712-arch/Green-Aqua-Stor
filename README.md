<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Green Aqua - Aquatic Plants Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .bg-aqua-green { background-color: #e0f4f1; }
        .text-aqua-dark { color: #0f4c43; }
        .border-aqua { border-color: #b2e0da; }
    </style>
</head>
<body class="bg-aqua-green font-sans text-slate-900 min-h-screen flex flex-col">

    <nav class="bg-white text-slate-900 border-b border-aqua sticky top-0 z-50 shadow-sm">
        <div class="max-w-6xl mx-auto px-4 py-3 flex justify-between items-center">
            <a href="#" class="flex items-center gap-3">
                <img src="logo.png" alt="Green Aqua Logo" class="h-10 w-auto object-contain">
                <span class="text-xl font-bold tracking-wide text-emerald-950">Green Aqua</span>
            </a>
            <button onclick="toggleCart()" class="relative p-2 bg-emerald-50 hover:bg-emerald-100 text-emerald-900 rounded-full transition">
                🛒 <span id="cart-count" class="absolute -top-1 -right-1 bg-amber-500 text-white text-xs w-5 h-5 flex items-center justify-center rounded-full font-bold">0</span>
            </button>
        </div>
    </nav>

    <main class="max-w-6xl mx-auto px-4 py-8 flex-1 w-full">
        <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4 mb-6">
            <div>
                <h1 class="text-2xl font-bold text-emerald-950 mb-1">Premium Aquatic Plants</h1>
                <p class="text-gray-600">Select your plants and checkout directly via WhatsApp.</p>
                
                <div class="flex items-center gap-1 mt-2 bg-white/80 w-fit px-3 py-1 rounded-full border border-aqua shadow-sm">
                    <span class="text-amber-500 text-sm">⭐⭐⭐⭐⭐</span>
                    <span class="text-xs font-semibold text-emerald-950">4.9/5 (120+ Ratings)</span>
                </div>
            </div>

            <div class="w-full md:max-w-md relative">
                <input type="text" id="search-input" oninput="searchProducts()" placeholder="🔍 Search plants by name or details..." class="w-full px-4 py-2.5 rounded-xl border border-gray-300 focus:outline-emerald-700 bg-white shadow-sm text-sm">
            </div>
        </div>
        
        <div class="flex flex-wrap gap-2 mb-8" id="category-filters">
            <button onclick="filterCategory('all', this)" class="px-4 py-2 rounded-full text-sm font-medium bg-emerald-800 text-white shadow-sm transition">
                All Plants
            </button>
            <button onclick="filterCategory('foreground', this)" class="px-4 py-2 rounded-full text-sm font-medium bg-white border border-gray-200 text-gray-700 hover:bg-gray-50 transition">
                Foreground
            </button>
            <button onclick="filterCategory('background', this)" class="px-4 py-2 rounded-full text-sm font-medium bg-white border border-gray-200 text-gray-700 hover:bg-gray-50 transition">
                Background
            </button>
            <button onclick="filterCategory('floating', this)" class="px-4 py-2 rounded-full text-sm font-medium bg-white border border-gray-200 text-gray-700 hover:bg-gray-50 transition">
                Floating Plants
            </button>
        </div>

        <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
            </div>
    </main>

    <footer class="bg-emerald-950 text-emerald-100 border-t border-emerald-900 mt-12">
        <div class="max-w-6xl mx-auto px-4 py-8 grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
            <div>
                <div class="flex items-center gap-2 mb-3">
                    <img src="logo.png" alt="Green Aqua" class="h-8 w-auto brightness-0 invert">
                    <span class="font-bold text-lg text-white">Green Aqua Plants</span>
                </div>
                <p class="text-sm text-emerald-200/80 max-w-sm">Your premium local source for high-quality foreground, background, and floating aquatic plants.</p>
            </div>
            <div class="space-y-2 md:text-right">
                <h4 class="text-white font-semibold text-sm tracking-wider uppercase">Contact Us</h4>
                <p class="text-sm">📞 Phone: <span id="footer-phone" class="text-emerald-300"></span></p>
                <p class="text-sm">📍 Address: <span id="footer-address" class="text-emerald-300"></span></p>
            </div>
        </div>
        <div class="text-center text-xs text-emerald-300/40 py-4 border-t border-emerald-900/60">
            &copy; 2026 Green Aqua. All rights reserved.
        </div>
    </footer>

    <div id="cart-drawer" class="fixed inset-0 bg-black/50 z-50 hidden flex justify-end">
        <div class="bg-white w-full max-w-md h-full p-6 flex flex-col shadow-2xl overflow-y-auto">
            <div class="flex justify-between items-center border-b pb-4">
                <h2 class="text-lg font-bold text-emerald-900">Your Shopping Cart</h2>
                <button onclick="toggleCart()" class="text-gray-500 hover:text-black text-2xl">&times;</button>
            </div>
            
            <div id="cart-items" class="flex-1 py-4 space-y-4">
                </div>

            <div class="border-t pt-4 space-y-3">
                <h3 class="text-sm font-semibold text-gray-700">Delivery Details:</h3>
                <input type="text" id="cust-name" placeholder="Customer Name" class="w-full p-2 border border-gray-300 rounded text-sm focus:outline-emerald-600">
                <input type="text" id="cust-address" placeholder="Delivery Address" class="w-full p-2 border border-gray-300 rounded text-sm focus:outline-emerald-600">
                
                <h3 class="text-sm font-semibold text-gray-700 pt-2">Payment Method:</h3>
                <div class="flex gap-4">
                    <label class="flex items-center gap-2 text-sm cursor-pointer">
                        <input type="radio" name="payment-method" value="bank" checked onclick="handlePaymentChange('bank')" class="accent-emerald-700"> Bank Deposit
                    </label>
                    <label class="flex items-center gap-2 text-sm cursor-pointer">
                        <input type="radio" name="payment-method" value="cod" onclick="handlePaymentChange('cod')" class="accent-emerald-700"> Cash on Delivery (COD)
                    </label>
                </div>

                <div id="nic-container" class="hidden">
                    <input type="text" id="cust-nic" placeholder="NIC Number (ID Card)" class="w-full p-2 border border-emerald-300 bg-emerald-50/50 rounded text-sm focus:outline-emerald-600">
                </div>
                
                <div class="border-t pt-3 mt-2">
                    <h3 class="text-sm font-semibold text-gray-700 mb-1">Shopping Experience Survey:</h3>
                    <p class="text-xs text-gray-500 mb-2">Are you satisfied with our online store system?</p>
                    <div class="flex flex-wrap gap-3">
                        <label class="flex items-center gap-1 text-xs cursor-pointer text-gray-700">
                            <input type="radio" name="satisfaction" value="Highly Satisfied 😍" checked class="accent-emerald-700"> Highly Satisfied 😍
                        </label>
                        <label class="flex items-center gap-1 text-xs cursor-pointer text-gray-700">
                            <input type="radio" name="satisfaction" value="Satisfied 🙂" class="accent-emerald-700"> Satisfied 🙂
                        </label>
                        <label class="flex items-center gap-1 text-xs cursor-pointer text-gray-700">
                            <input type="radio" name="satisfaction" value="Neutral 😐" class="accent-emerald-700"> Neutral 😐
                        </label>
                    </div>
                </div>
            </div>

            <div id="bank-info" class="mt-4 p-3 bg-emerald-50 border border-emerald-200 rounded-lg">
                <h4 class="text-xs font-bold text-emerald-900 tracking-wider uppercase mb-1">🏦 Bank Deposit Details</h4>
                <p class="text-sm text-gray-700">Bank: <span class="font-semibold" id="bank-name-text">Commercial Bank</span></p>
                <p class="text-sm text-gray-700">Account No: <span class="font-bold text-emerald-800" id="bank-acc-text">8001XXXXXX</span></p>
                <p class="text-xs text-amber-700 mt-2">⚠️ Please send the deposit slip screenshot in the WhatsApp chat.</p>
            </div>

            <div id="cod-info" class="mt-4 p-3 bg-amber-50 border border-amber-200 rounded-lg hidden">
                <h4 class="text-xs font-bold text-amber-900 tracking-wider uppercase mb-1">📦 Cash on Delivery Rules</h4>
                <p class="text-xs text-gray-700">Order will be verified using your NIC. Please pay the cash directly to the courier agent upon delivery.</p>
            </div>

            <div class="border-t pt-4 mt-4">
                <div class="flex justify-between font-bold text-lg mb-4">
                    <span>Total Amount:</span>
                    <span id="cart-total">LKR 0.00</span>
                </div>
                <button onclick="sendToWhatsApp()" class="w-full bg-emerald-600 text-white py-3 rounded-lg font-medium hover:bg-emerald-700 transition flex items-center justify-center gap-2 shadow">
                    💬 Send Order via WhatsApp
                </button>
            </div>
        </div>
    </div>

    <div id="details-modal" class="fixed inset-0 bg-black/60 z-50 hidden flex items-center justify-center p-4 backdrop-blur-sm">
        <div class="bg-white w-full max-w-lg rounded-2xl overflow-hidden shadow-2xl relative flex flex-col max-h-[90vh]">
            <button onclick="closeDetails()" class="absolute top-3 right-3 bg-black/50 hover:bg-black/70 text-white w-8 h-8 rounded-full flex items-center justify-center z-10 font-bold transition">&times;</button>
            
            <img id="modal-img" src="" alt="" class="w-full h-64 object-cover">
            
            <div class="p-6 overflow-y-auto flex-1">
                <span id="modal-category" class="text-[10px] uppercase tracking-wider font-bold bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded-full"></span>
                <h2 id="modal-name" class="text-2xl font-bold text-emerald-950 mt-2"></h2>
                <p id="modal-price" class="text-xl font-bold text-emerald-700 mt-1"></p>
                
                <p id="modal-desc" class="text-gray-600 text-sm mt-3 leading-relaxed border-t pt-3"></p>
                
                <div class="grid grid-cols-3 gap-2 mt-4 bg-slate-50 p-3 rounded-xl border border-slate-100 text-center">
                    <div>
                        <span class="block text-[10px] text-gray-400 uppercase font-bold">Light</span>
                        <span id="modal-light" class="text-xs font-semibold text-slate-700"></span>
                    </div>
                    <div>
                        <span class="block text-[10px] text-gray-400 uppercase font-bold">CO2</span>
                        <span id="modal-co2" class="text-xs font-semibold text-slate-700"></span>
                    </div>
                    <div>
                        <span class="block text-[10px] text-gray-400 uppercase font-bold">Growth</span>
                        <span id="modal-growth" class="text-xs font-semibold text-slate-700"></span>
                    </div>
                </div>
            </div>
            
            <div class="p-4 bg-slate-50 border-t border-slate-100 flex gap-3">
                <button id="modal-add-btn" class="flex-1 bg-emerald-800 text-white py-3 rounded-xl font-medium hover:bg-emerald-900 transition shadow">
                    + Add to Cart
                </button>
            </div>
        </div>
    </div>

    <script>
        const STORE_DETAILS = {
            whatsappNumber: "947XXXXXXXX",      
            phone: "+94 7X XXX XXXX",          
            address: "Your Store Address, SL", 
            bankName: "Commercial Bank",       
            bankAccount: "8001XXXXXX"          
        };

        const products = [
            { id: 1, name: "Anubias Nana", price: 450, category: "foreground", desc: "Low light plant, perfect for attaching to driftwood or rocks. Highly durable and great for beginners.", img: "anubias.jpg", light: "Low", co2: "Low/No", growth: "Slow" },
            { id: 2, name: "Java Moss (Cup)", price: 350, category: "foreground", desc: "Excellent for shrimp tanks and breeding setups. Provides great hiding spots for baby fish.", img: "javamoss.jpg", light: "Low to Medium", co2: "Low", growth: "Medium" },
            { id: 3, name: "Amazon Sword Plant", price: 280, category: "background", desc: "Beautiful background plant with broad green leaves. Requires nutrient-rich substrate or root tabs.", img: "swordplant.jpg", light: "Medium", co2: "Low", growth: "Medium" },
            { id: 4, name: "Vallisneria", price: 200, category: "background", desc: "Tall, grass-like background plant that spreads easily via runners to form a dense jungle look.", img: "vallisneria.jpg", light: "Medium", co2: "Low", growth: "Fast" },
            { id: 5, name: "Water Lettuce", price: 150, category: "floating", desc: "Floating rosette plant. Trailing roots offer great protection for fish fry and absorb excess nitrates.", img: "waterlettuce.jpg", light: "Medium to High", co2: "No", growth: "Fast" },
            { id: 6, name: "Frogbit", price: 180, category: "floating", desc: "Popular floating plant with round, bright green leaves. Perfect for shading low-light plants below.", img: "frogbit.jpg", light: "Medium", co2: "No", growth: "Fast" }
        ];

        let cart = [];
        let currentCategory = 'all';
        let searchQuery = '';

        function loadConfig() {
            document.getElementById('footer-phone').innerText = STORE_DETAILS.phone;
            document.getElementById('footer-address').innerText = STORE_DETAILS.address;
            document.getElementById('bank-name-text').innerText = STORE_DETAILS.bankName;
            document.getElementById('bank-acc-text').innerText = STORE_DETAILS.bankAccount;
        }

        function renderProducts() {
            const grid = document.getElementById('product-grid');
            
            const filteredProducts = products.filter(p => {
                const matchesCategory = currentCategory === 'all' || p.category === currentCategory;
                const matchesSearch = p.name.toLowerCase().includes(searchQuery) || p.desc.toLowerCase().includes(searchQuery);
                return matchesCategory && matchesSearch;
            });

            if (filteredProducts.length === 0) {
                grid.innerHTML = `<div class="col-span-full text-center py-12 bg-white/80 border border-gray-200 text-gray-500 rounded-xl text-sm">No plants found matching your search.</div>`;
                return;
            }

            grid.innerHTML = filteredProducts.map(p => `
                <div class="bg-white border border-gray-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition flex flex-col justify-between">
                    <div>
                        <div class="relative cursor-pointer" onclick="openDetails(${p.id})">
                            <img src="${p.img}" alt="${p.name}" class="w-full h-52 object-cover">
                            <span class="absolute top-2 left-2 bg-emerald-900/90 text-white text-[10px] uppercase tracking-wider font-bold px-2 py-0.5 rounded-full shadow-sm">
                                ${p.category}
                            </span>
                        </div>
                        <div class="p-4">
                            <h3 onclick="openDetails(${p.id})" class="font-semibold text-lg text-emerald-950 hover:text-emerald-700 cursor-pointer transition">${p.name}</h3>
                            <p class="text-xs text-gray-500 mt-1 italic line-clamp-2 leading-relaxed">${p.desc}</p>
                            <button onclick="openDetails(${p.id})" class="text-emerald-700 font-medium text-xs mt-2 hover:underline">🔍 View Plant Details</button>
                        </div>
                    </div>
                    <div class="p-4 pt-0">
                        <div class="border-t border-gray-100 pt-3 flex justify-between items-center">
                            <span class="text-emerald-700 font-bold">LKR ${p.price}.00</span>
                            <button onclick="addToCart(${p.id})" class="bg-emerald-800 text-white px-3 py-1.5 rounded-md text-xs font-medium hover:bg-emerald-900 transition">
                                + Add to Cart
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function searchProducts() {
            searchQuery = document.getElementById('search-input').value.toLowerCase().trim();
            renderProducts();
        }

        function openDetails(id) {
            const product = products.find(p => p.id === id);
            if (!product) return;

            document.getElementById('modal-img').src = product.img;
            document.getElementById('modal-img').alt = product.name;
            document.getElementById('modal-category').innerText = product.category;
            document.getElementById('modal-name').innerText = product.name;
            document.getElementById('modal-price').innerText = `LKR ${product.price}.00`;
            document.getElementById('modal-desc').innerText = product.desc;
            
            document.getElementById('modal-light').innerText = product.light || "N/A";
            document.getElementById('modal-co2').innerText = product.co2 || "N/A";
            document.getElementById('modal-growth').innerText = product.growth || "N/A";

            const addBtn = document.getElementById('modal-add-btn');
            addBtn.onclick = function() {
                addToCart(product.id);
                closeDetails();
            };

            document.getElementById('details-modal').classList.remove('hidden');
        }

        function closeDetails() {
            document.getElementById('details-modal').classList.add('hidden');
        }

        function filterCategory(category, buttonElement) {
            currentCategory = category;
            document.querySelectorAll('#category-filters button').forEach(btn => {
                btn.className = "px-4 py-2 rounded-full text-sm font-medium bg-white border border-gray-200 text-gray-700 hover:bg-gray-50 transition";
            });
            buttonElement.className = "px-4 py-2 rounded-full text-sm font-medium bg-emerald-800 text-white shadow-sm transition";
            renderProducts();
        }

        function toggleCart() {
            document.getElementById('cart-drawer').classList.toggle('hidden');
        }

        function handlePaymentChange(method) {
            const nicContainer = document.getElementById('nic-container');
            const bankInfo = document.getElementById('bank-info');
            const codInfo = document.getElementById('cod-info');

            if (method === 'cod') {
                nicContainer.classList.remove('hidden');
                codInfo.classList.remove('hidden');
                bankInfo.classList.add('hidden');
            } else {
                nicContainer.classList.add('hidden');
                codInfo.classList.add('hidden');
                bankInfo.classList.remove('hidden');
            }
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            const exist = cart.find(item => item.id === id);
            if (exist) {
                exist.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }
            updateCart();
        }

        function updateCart() {
            const cartItems = document.getElementById('cart-items');
            const cartCount = document.getElementById('cart-count');
            const cartTotal = document.getElementById('cart-total');

            cartCount.innerText = cart.reduce((sum, item) => sum + item.quantity, 0);

            if (cart.length === 0) {
                cartItems.innerHTML = `<p class="text-gray-500 text-center py-8">Your cart is empty.</p>`;
                cartTotal.innerText = "LKR 0.00";
                return;
            }

            let total = 0;
            cartItems.innerHTML = cart.map(item => {
                total += item.price * item.quantity;
                return `
                    <div class="flex items-center justify-between border-b pb-2">
                        <div>
                            <h4 class="font-medium text-sm text-gray-800">${item.name}</h4>
                            <p class="text-gray-500 text-xs">LKR ${item.price} x ${item.quantity}</p>
                        </div>
                        <button onclick="removeFromCart(${item.id})" class="text-red-500 text-xs hover:underline">Remove</button>
                    </div>
                `;
            }).join('');

            cartTotal.innerText = `LKR ${total.toLocaleString()}.00`;
        }

        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCart();
        }

        function sendToWhatsApp() {
            if (cart.length === 0) return alert("Your cart is empty!");
            
            const name = document.getElementById('cust-name').value.trim();
            const address = document.getElementById('cust-address').value.trim();
            const method = document.querySelector('input[name="payment-method"]:checked').value;
            const nic = document.getElementById('cust-nic').value.trim();
            const satisfaction = document.querySelector('input[name="satisfaction"]:checked').value;

            if (!name || !address) {
                return alert("Please fill in your Name and Delivery Address.");
            }

            if (method === 'cod' && !nic) {
                return alert("Please enter your NIC Number for Cash on Delivery verification.");
            }

            let message = `🌱 *NEW ORDER - GREEN AQUA* 🌱\n\n`;
            message += `👤 *Customer Details:*\n`;
            message += `Name: ${name}\n`;
            message += `Address: ${address}\n`;
            
            if (method === 'cod') {
                message += `ID/NIC: ${nic}\n`;
            }
            message += `\n📦 *Order Items:*\n`;

            let total = 0;
            cart.forEach(item => {
                let itemTotal = item.price * item.quantity;
                total += itemTotal;
                message += `- ${item.name} (x${item.quantity}) = LKR ${itemTotal}\n`;
            });

            message += `\n💵 *Total Amount:* LKR ${total.toLocaleString()}.00\n`;
            
            if (method === 'cod') {
                message += `💳 *Payment Method:* Cash on Delivery (COD)\n`;
            } else {
                message += `💳 *Payment Method:* Bank Deposit\n`;
            }

            message += `🥰 *Store Satisfaction:* ${satisfaction}\n\n`;

            if (method === 'cod') {
                message += `Please confirm my order. I will pay cash upon arrival!`;
            } else {
                message += `I will send the payment slip right below this message! 👇`;
            }

            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://wa.me/${STORE_DETAILS.whatsappNumber}?text=${encodedMessage}`;

            window.open(whatsappUrl, '_blank');
        }

        loadConfig();
        renderProducts();
    </script>
</body>
</html>
