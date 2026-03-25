<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LuxeStep | Premium Sneaker Store</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #ffffff;
            --card-bg: #ffffff;
            --text: #111111;
            --accent: #ff3b30;
            --star: #ffcc00;
            --wa: #25d366;
            --fb: #0084ff;
            --gray: #f6f6f8;
            --radius: 16px;
            --shadow: 0 8px 25px rgba(0,0,0,0.06);
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }

        body { 
            font-family: 'Inter', sans-serif; 
            margin: 0; background: var(--bg); color: var(--text); 
            -webkit-tap-highlight-color: transparent;
            overflow-x: hidden;
        }

        header { 
            padding: 15px 4% 10px; border-bottom: 1px solid rgba(0,0,0,0.05); 
            position: sticky; top: 0; background: rgba(255,255,255,0.9); 
            backdrop-filter: blur(15px); z-index: 1000;
        }
        .logo { 
            font-weight: 900; font-size: 16px; letter-spacing: 4px; 
            text-transform: uppercase; text-align: center; margin-bottom: 12px;
        }
        
        .search-container { position: relative; margin-bottom: 12px; }
        .search-bar {
            width: 100%; padding: 12px 15px 12px 40px; border-radius: 12px;
            border: 1px solid transparent; background: var(--gray); font-size: 14px;
            box-sizing: border-box; outline: none; transition: 0.3s;
        }
        .search-bar:focus { border-color: #000; background: #fff; box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
        .search-icon { position: absolute; left: 15px; top: 50%; transform: translateY(-50%); color: #888; }

        .menu-scroll { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 5px; scrollbar-width: none; }
        .menu-scroll::-webkit-scrollbar { display: none; }
        .menu-item { 
            background: var(--gray); padding: 8px 18px; border-radius: 20px; 
            font-size: 11px; font-weight: 700; cursor: pointer; border: none;
            transition: 0.3s; white-space: nowrap; color: #666;
        }
        .menu-item.active { background: #000; color: #fff; }

        .container { padding: 12px; max-width: 1200px; margin: 0 auto; }
        .grid { 
            display: grid; 
            grid-template-columns: repeat(2, 1fr); /* 2 columns for mobile */
            gap: 12px; 
        }

        @media (min-width: 768px) {
            .grid { grid-template-columns: repeat(4, 1fr); }
        }

        .card { 
            background: var(--card-bg); border-radius: var(--radius); overflow: hidden; 
            position: relative; border: 1px solid #f2f2f2; cursor: pointer;
            transition: 0.3s cubic-bezier(0.2, 0, 0.2, 1);
        }
        .card:active { transform: scale(0.96); }

        .img-holder { position: relative; aspect-ratio: 1/1; background: #fdfdfd; overflow: hidden; display: flex; align-items: center; justify-content: center; }
        .card img { width: 90%; height: 90%; object-fit: contain; transition: 0.5s ease; }
        
        .sold-tag { position: absolute; inset: 0; background: rgba(255,255,255,0.7); display: flex; align-items: center; justify-content: center; z-index: 10; backdrop-filter: blur(2px); }
        .sold-text { background: #000; color: #fff; padding: 5px 10px; font-size: 9px; font-weight: 800; border-radius: 5px; }
        .badge { position: absolute; top: 10px; left: 10px; padding: 4px 8px; border-radius: 6px; font-size: 9px; font-weight: 800; background: var(--accent); color: #fff; z-index: 5; }

        .info { padding: 12px; }
        .item-name { font-size: 12px; font-weight: 600; color: #444; margin-bottom: 4px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .new-p { font-weight: 800; font-size: 15px; color: #000; margin-bottom: 4px; }
        
        .ratings { display: flex; align-items: center; gap: 3px; color: var(--star); font-size: 10px; }
        .rating-text { color: #aaa; font-size: 10px; margin-left: 2px; }

        .modal { 
            display: none; position: fixed; top: 50%; left: 50%; 
            transform: translate(-50%, -45%) scale(0.9); 
            background: white; border-radius: 28px; z-index: 4000; width: 90%; max-width: 400px;
            max-height: 85vh; overflow-y: auto; transition: 0.3s ease; opacity: 0;
        }
        .modal.active { display: block; transform: translate(-50%, -50%) scale(1); opacity: 1; }
        .modal-img { width: 100%; aspect-ratio: 1/1; object-fit: contain; background: #f9f9f9; display: block; }
        .modal-details { padding: 25px; }
        .modal-title { font-size: 22px; font-weight: 900; margin-bottom: 5px; line-height: 1.2; }
        .modal-price { font-size: 20px; font-weight: 700; color: var(--accent); margin-bottom: 10px; }
        
        .order-btn {
            display: flex; align-items: center; justify-content: center; gap: 10px;
            width: 100%; padding: 16px; border-radius: 15px; border: none;
            margin-bottom: 10px; font-weight: 800; font-size: 13px; cursor: pointer;
            text-decoration: none; transition: 0.3s;
        }
        .btn-wa { background: #e7f9ee; color: #1fb354; }
        .btn-fb { background: #e7f3ff; color: #0084ff; }
        .btn-wa:hover { background: var(--wa); color: #fff; }
        .btn-fb:hover { background: var(--fb); color: #fff; }

        .overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.4); backdrop-filter: blur(8px); z-index: 3900; opacity: 0; transition: 0.3s; }
        .close-modal-btn { position: absolute; top: 15px; right: 15px; background: rgba(255,255,255,0.9); border: none; width: 32px; height: 32px; border-radius: 50%; cursor: pointer; z-index: 4001; font-size: 18px; font-weight: bold; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }

        .admin-actions { position: absolute; top: 5px; right: 5px; display: none; flex-direction: column; gap: 4px; z-index: 25; }
        .adm-mode .admin-actions { display: flex; }
        .adm-btn { font-size: 8px; padding: 6px 8px; border: none; border-radius: 6px; cursor: pointer; color: white; font-weight: 800; }
        input, select { width: 100%; padding: 14px; margin: 8px 0; border: none; border-radius: 12px; background: var(--gray); outline: none; font-size: 14px; box-sizing: border-box; }
        .btn-black { background: #000; color: #fff; border: none; padding: 16px; border-radius: 12px; width: 100%; font-weight: 800; cursor: pointer; margin-top: 10px; }
    </style>
</head>
<body id="bodyTag">

    <header>
        <div class="logo">LUXESTEP</div>
        <div class="search-container">
            <span class="search-icon">🔍</span>
            <input type="text" id="searchInput" class="search-bar" placeholder="Search sneakers..." oninput="handleSearch()">
        </div>
        <div class="menu-scroll">
            <button class="menu-item active" onclick="filterCat('All', this)">All</button>
            <button class="menu-item" onclick="filterCat('Shoes', this)">Shoes</button>
            <button class="menu-item" onclick="filterCat('Cap', this)">Cap</button>
            <button class="menu-item" onclick="filterCat('T-Shirt', this)">T-Shirt</button>
            <button class="menu-item" onclick="showModal('loginModal')" style="opacity:0.5; font-weight:400; background:none; border:1px dashed #ccc;">Admin</button>
        </div>
    </header>

    <div class="container">
        <div id="productGrid" class="grid">
            <p style="grid-column: 1/-1; text-align: center; color: #999;">Loading products...</p>
        </div>
        
        <div style="text-align: center; margin-top: 50px; padding-bottom: 80px;">
            <button id="addBtn" onclick="showModal('adminModal')" style="display:none; margin: 20px auto; padding: 14px 28px; border-radius: 30px; border: none; background: #000; color: #fff; font-weight: 800; cursor:pointer;">+ ADD PRODUCT</button>
            <button id="logoutBtn" onclick="logoutAdmin()" style="display:none; margin: 10px auto; color: #ff3b30; background: none; border: none; font-size: 12px; font-weight: 700; text-decoration: underline; cursor:pointer;">LOGOUT ADMIN</button>
            <p style="font-size: 10px; color: #ccc; margin-top: 20px;">© 2026 LUXESTEP STORE</p>
        </div>
    </div>

    <div id="viewModal" class="modal">
        <button class="close-modal-btn" onclick="closeModal()">×</button>
        <div id="viewContent"></div>
    </div>

    <div id="loginModal" class="modal">
        <div style="padding: 25px;">
            <h3 style="text-align: center; margin: 0 0 15px 0;">Admin Login</h3>
            <input type="password" id="adminPass" placeholder="Password">
            <button class="btn-black" onclick="checkLogin()">LOGIN</button>
        </div>
    </div>

    <div id="adminModal" class="modal">
        <div style="padding: 25px;">
            <h3 style="text-align: center; margin: 0 0 15px 0;">New Product</h3>
            <input type="text" id="pName" placeholder="Product Name">
            <input type="number" id="pPrice" placeholder="Price (₱)">
            <select id="pCat">
                <option value="Shoes">Shoes</option>
                <option value="Cap">Cap</option>
                <option value="T-Shirt">T-Shirt</option>
            </select>
            <input type="file" id="pFile" accept="image/*">
            <button class="btn-black" id="uploadBtn" onclick="uploadItem()">POST NOW</button>
        </div>
    </div>

    <div id="overlay" class="overlay" onclick="closeModal()"></div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, onValue, set } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyDDNemQfmyd89Fk94FJ0B6tlk_u_isGelA",
            authDomain: "crush-855cb.firebaseapp.com",
            databaseURL: "https://crush-855cb-default-rtdb.firebaseio.com",
            projectId: "crush-855cb",
            storageBucket: "crush-855cb.firebasestorage.app",
            messagingSenderId: "32796590966",
            appId: "1:32796590966:web:0fe591b0d7cca6aaf07057",
            measurementId: "G-R2K7TH1265"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);
        const shopRef = ref(db, 'luxe_products');

        // Expose to window so our other functions can use them
        window.firebaseDB = db;
        window.shopRef = shopRef;
        window.dbSet = set;
        window.dbRef = ref;

        // Listen for data changes (This makes it appear on all devices!)
        onValue(shopRef, (snapshot) => {
            const data = snapshot.val();
            window.shopData = data ? Object.values(data) : [];
            // We keep the keys to handle delete/update easily
            window.rawKeys = data ? Object.keys(data) : [];
            render();
        });
    </script>

    <script>
        const IMGBB_API_KEY = "496a17374c90fa8256924b705f324e7b"; 
        window.shopData = [];
        let isAdmin = localStorage.getItem('isLuxeAdmin') === 'true'; 
        let currentFilter = "All";
        let searchQuery = "";

        function render() {
            const grid = document.getElementById('productGrid');
            const body = document.getElementById('bodyTag');
            
            isAdmin ? body.classList.add('adm-mode') : body.classList.remove('adm-mode');
            document.getElementById('addBtn').style.display = isAdmin ? 'block' : 'none';
            document.getElementById('logoutBtn').style.display = isAdmin ? 'block' : 'none';

            let filtered = window.shopData.map((p, index) => ({...p, originalIndex: index}));

            if(currentFilter !== "All") filtered = filtered.filter(p => p.cat === currentFilter);
            if(searchQuery) filtered = filtered.filter(p => p.name.toLowerCase().includes(searchQuery.toLowerCase()));

            if(filtered.length === 0) {
                grid.innerHTML = `<p style="grid-column: 1/-1; text-align: center; color: #999; padding: 40px;">No products found.</p>`;
                return;
            }

            grid.innerHTML = filtered.map((p, index) => {
                const firebaseKey = window.rawKeys[p.originalIndex];
                return `
                <div class="card" onclick="viewProduct(${p.originalIndex})" style="animation: fadeInUp 0.4s ease forwards ${index * 0.05}s; opacity: 0;">
                    <div class="admin-actions">
                        <button class="adm-btn" style="background:#333" onclick="event.stopPropagation(); toggleSold('${firebaseKey}', ${p.originalIndex})">${p.sold ? 'RESTOCK' : 'SOLD'}</button>
                        <button class="adm-btn" style="background:#ff3b30" onclick="event.stopPropagation(); deleteItem('${firebaseKey}')">DEL</button>
                    </div>
                    <div class="img-holder">
                        ${p.sold ? '<div class="sold-tag"><span class="sold-text">SOLD OUT</span></div>' : '<div class="badge">NEW</div>'}
                        <img src="${p.img}" alt="product" loading="lazy">
                    </div>
                    <div class="info">
                        <div class="item-name">${p.name}</div>
                        <div class="new-p">₱${Number(p.price).toLocaleString()}</div>
                        <div class="ratings">
                            <span>★★★★★</span>
                            <span class="rating-text">(5.0)</span>
                        </div>
                    </div>
                </div>
            `}).join('');
        }

        function handleSearch() {
            searchQuery = document.getElementById('searchInput').value;
            render();
        }

        function viewProduct(idx) {
            const p = window.shopData[idx];
            const content = document.getElementById('viewContent');
            content.innerHTML = `
                <img src="${p.img}" class="modal-img">
                <div class="modal-details">
                    <div style="font-size: 10px; color: #999; font-weight: 800; text-transform: uppercase; margin-bottom: 5px;">${p.cat}</div>
                    <div class="modal-title">${p.name}</div>
                    <div class="modal-price">₱${Number(p.price).toLocaleString()}</div>
                    <div class="ratings" style="margin-bottom: 20px; font-size: 14px;">
                        <span>★★★★★</span>
                        <span class="rating-text" style="font-size: 12px;">5.0 Rating</span>
                    </div>
                    ${p.sold ? '<button class="order-btn" style="background:#f0f0f0; color:#aaa;">OUT OF STOCK</button>' : `
                        <a href="https://wa.me/639085123194?text=Boss! Interested ko ani: ${p.name}" target="_blank" class="order-btn btn-wa">WHATSAPP ORDER</a>
                        <a href="https://m.me/61577519363119" target="_blank" class="order-btn btn-fb">MESSENGER MESSAGE</a>
                    `}
                </div>
            `;
            showModal('viewModal');
        }

        function showModal(id) { 
            const modal = document.getElementById(id);
            const overlay = document.getElementById('overlay');
            modal.style.display = 'block';
            overlay.style.display = 'block';
            setTimeout(() => { modal.classList.add('active'); overlay.style.opacity = '1'; }, 10);
        }
        
        function closeModal() { 
            const modals = document.querySelectorAll('.modal');
            const overlay = document.getElementById('overlay');
            modals.forEach(m => m.classList.remove('active'));
            overlay.style.opacity = '0';
            setTimeout(() => { modals.forEach(m => m.style.display = 'none'); overlay.style.display = 'none'; }, 300);
        }

        function checkLogin() {
            if(document.getElementById('adminPass').value === "admin") {
                isAdmin = true;
                localStorage.setItem('isLuxeAdmin', 'true');
                closeModal();
                render();
            } else { alert("Wrong password!"); }
        }

        function logoutAdmin() {
            isAdmin = false;
            localStorage.setItem('isLuxeAdmin', 'false');
            render();
        }

        async function uploadItem() {
            const file = document.getElementById('pFile').files[0];
            const name = document.getElementById('pName').value;
            const price = document.getElementById('pPrice').value;
            const cat = document.getElementById('pCat').value;
            const btn = document.getElementById('uploadBtn');

            if(!file || !name || !price) return alert("Fill all fields!");
            btn.disabled = true; btn.innerText = "Uploading Image...";

            const formData = new FormData();
            formData.append("image", file);

            try {
                const res = await fetch(`https://api.imgbb.com/1/upload?key=${IMGBB_API_KEY}`, { method: "POST", body: formData });
                const data = await res.json();
                if(data.success) {
                    const newId = Date.now();
                    const newProduct = { name, price, cat, img: data.data.url, sold: false };
                    
                    // Save to Firebase
                    await window.dbSet(window.dbRef(window.firebaseDB, 'luxe_products/' + newId), newProduct);
                    
                    closeModal();
                    document.getElementById('pName').value = "";
                    document.getElementById('pPrice').value = "";
                    document.getElementById('pFile').value = "";
                }
            } catch(e) { alert("Error uploading: " + e.message); }
            finally { btn.disabled = false; btn.innerText = "POST NOW"; }
        }

        async function toggleSold(key, idx) { 
            const updatedProduct = {...window.shopData[idx], sold: !window.shopData[idx].sold};
            await window.dbSet(window.dbRef(window.firebaseDB, 'luxe_products/' + key), updatedProduct);
        }

        async function deleteItem(key) { 
            if(confirm("Delete item?")) { 
                await window.dbSet(window.dbRef(window.firebaseDB, 'luxe_products/' + key), null);
            } 
        }
        
        function filterCat(cat, el) {
            currentFilter = cat;
            document.querySelectorAll('.menu-item').forEach(b => b.classList.remove('active'));
            el.classList.add('active');
            render();
        }
    </script>
</body>
</html>
