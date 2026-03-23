<!DOCTYPE html>
<html lang="my">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
    <title>Bot Father — Game Sharing Platform</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700;14..32,800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body { background: #0A0E1A; font-family: 'Inter', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; padding: 0; }
        .app-container { max-width: 480px; width: 100%; background: #0F1322; border-radius: 32px; overflow: hidden; box-shadow: 0 20px 40px rgba(0,0,0,0.5); margin: 16px auto; }
        .main-content { height: calc(100vh - 100px); overflow-y: auto; padding-bottom: 20px; scroll-behavior: smooth; }
        .main-content::-webkit-scrollbar { width: 4px; }
        .main-content::-webkit-scrollbar-track { background: #1E243B; }
        .main-content::-webkit-scrollbar-thumb { background: #FF7A2F; border-radius: 10px; }
        .status-bar { padding: 12px 20px 4px; display: flex; justify-content: space-between; font-size: 14px; font-weight: 500; color: #8E9AAF; }
        .main-header { display: flex; justify-content: space-between; align-items: center; padding: 8px 20px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); }
        .logo { display: flex; align-items: center; gap: 8px; }
        .logo-icon { background: linear-gradient(135deg, #FF7A2F, #FF3A6F); width: 36px; height: 36px; border-radius: 12px; display: flex; align-items: center; justify-content: center; }
        .logo-icon i { font-size: 22px; color: white; }
        .logo-text { font-size: 24px; font-weight: 800; background: linear-gradient(135deg, #FFF, #B9C8FF); -webkit-background-clip: text; background-clip: text; color: transparent; }
        .header-icons i { font-size: 22px; color: #B9C3E8; margin-left: 18px; cursor: pointer; }
        .featured-section { padding: 16px 0 8px; }
        .section-label { padding: 0 20px 12px; display: flex; justify-content: space-between; align-items: baseline; }
        .section-label h3 { font-size: 18px; font-weight: 700; color: white; }
        .section-label span { font-size: 13px; color: #FF7A2F; cursor: pointer; }
        .featured-carousel { overflow-x: auto; scroll-snap-type: x mandatory; scrollbar-width: none; padding: 0 16px; display: flex; gap: 16px; -webkit-overflow-scrolling: touch; }
        .featured-carousel::-webkit-scrollbar { display: none; }
        .featured-card { flex: 0 0 85%; scroll-snap-align: start; background: linear-gradient(145deg, #1E253F, #11162A); border-radius: 28px; overflow: hidden; padding: 16px; display: flex; align-items: center; gap: 16px; cursor: pointer; transition: transform 0.1s; }
        .featured-card:active { transform: scale(0.98); }
        .featured-card .game-icon { width: 70px; height: 70px; border-radius: 20px; background: rgba(255,255,255,0.1); display: flex; align-items: center; justify-content: center; overflow: hidden; }
        .featured-card .game-icon img { width: 100%; height: 100%; object-fit: cover; }
        .featured-info { flex: 1; }
        .featured-info h4 { font-size: 18px; font-weight: 700; color: white; }
        .featured-info p { font-size: 12px; color: #B0BBE0; margin: 4px 0; }
        .play-badge { background: #FF7A2F; padding: 6px 14px; border-radius: 40px; font-size: 12px; font-weight: bold; display: inline-block; color: white; }
        .category-row { margin: 24px 0 12px; }
        .row-header { display: flex; justify-content: space-between; align-items: baseline; padding: 0 20px 10px; }
        .row-header h4 { font-size: 18px; font-weight: 700; color: #EFF3FF; }
        .row-header a { font-size: 12px; color: #FF7A2F; text-decoration: none; cursor: pointer; }
        .games-horizontal { display: flex; gap: 16px; overflow-x: auto; scroll-snap-type: x mandatory; padding: 0 20px 12px; scrollbar-width: thin; -webkit-overflow-scrolling: touch; }
        .games-horizontal::-webkit-scrollbar { height: 3px; }
        .game-item { flex: 0 0 130px; scroll-snap-align: start; background: #181E2F; border-radius: 24px; padding: 12px 8px; text-align: center; cursor: pointer; transition: 0.1s; }
        .game-item:active { transform: scale(0.96); background: #252D45; }
        .game-item img { width: 80px; height: 80px; object-fit: cover; border-radius: 20px; margin-bottom: 10px; }
        .game-item .game-name { font-size: 13px; font-weight: 600; color: white; margin: 8px 0 4px; }
        .game-item .game-category { font-size: 10px; color: #8F9BB9; }
        .bottom-nav { position: sticky; bottom: 0; background: rgba(12,16,27,0.96); backdrop-filter: blur(20px); border-top: 1px solid rgba(255,255,255,0.07); display: flex; justify-content: space-around; padding: 10px 20px 22px; width: 100%; z-index: 10; }
        .nav-item { display: flex; flex-direction: column; align-items: center; gap: 4px; color: #5F6A8A; cursor: pointer; }
        .nav-item i { font-size: 22px; }
        .nav-item span { font-size: 11px; font-weight: 500; }
        .nav-item.active { color: #FF7A2F; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85); backdrop-filter: blur(5px); justify-content: center; align-items: center; z-index: 2000; }
        .modal-content { background: #181E2F; max-width: 420px; width: 90%; border-radius: 32px; padding: 24px; color: white; max-height: 85vh; overflow-y: auto; }
        .modal-content h3 { font-size: 24px; margin-bottom: 16px; }
        .modal-content img { width: 100%; border-radius: 20px; margin-bottom: 16px; }
        .post-stats { display: flex; gap: 20px; margin: 16px 0; justify-content: space-around; }
        .like-btn, .share-btn { background: #2A3150; padding: 8px 16px; border-radius: 40px; cursor: pointer; display: inline-flex; align-items: center; gap: 8px; }
        .like-btn.liked { background: #FF3A6F; }
        .comments-section { margin-top: 20px; border-top: 1px solid #2A3150; padding-top: 16px; }
        .comment-item { background: #0F1322; border-radius: 20px; padding: 10px; margin-bottom: 10px; }
        .comment-user { font-weight: bold; color: #FF7A2F; }
        .comment-time { font-size: 10px; color: #8F9BB9; margin-left: 8px; }
        .comment-text { margin-top: 4px; color: #EFF3FF; }
        .comment-form { margin-top: 16px; display: flex; gap: 8px; }
        .comment-form input { flex: 1; padding: 10px; background: #0F1322; border: 1px solid #2A3150; border-radius: 40px; color: white; }
        .comment-form button { background: #FF7A2F; border: none; padding: 8px 16px; border-radius: 40px; color: white; cursor: pointer; }
        .share-buttons { display: flex; gap: 12px; margin-top: 12px; justify-content: center; }
        .share-buttons i { font-size: 24px; cursor: pointer; color: #B9C3E8; }
        .btn-primary { background: linear-gradient(95deg, #FF7A2F, #FF3A6F); border: none; padding: 12px 20px; border-radius: 60px; font-weight: 700; color: white; cursor: pointer; font-size: 14px; transition: 0.1s; }
        .btn-primary:active { transform: scale(0.96); }
        .btn-outline { background: transparent; border: 1px solid #FF7A2F; color: #FF7A2F; padding: 8px 16px; border-radius: 40px; cursor: pointer; }
        .profile-avatar { width: 100px; height: 100px; border-radius: 50%; margin: 0 auto 16px; overflow: hidden; }
        .profile-info { text-align: center; margin: 20px 0; }
        .post-list-item { background: #181E2F; margin: 8px 0; padding: 12px; border-radius: 20px; display: flex; justify-content: space-between; align-items: center; }
        .delete-btn { background: #FF3A6F; border: none; padding: 6px 12px; border-radius: 40px; color: white; cursor: pointer; font-size: 12px; }
        .form-group { margin-bottom: 16px; text-align: left; }
        .form-group label { display: block; margin-bottom: 6px; font-size: 14px; font-weight: 500; }
        .form-group input, .form-group select, .form-group textarea { width: 100%; padding: 10px; background: #0F1322; border: 1px solid #2A3150; border-radius: 20px; color: white; font-family: inherit; }
        .form-group input[type="file"] { padding: 6px; background: #0F1322; color: #B9C3E8; }
        .back-link { display: inline-block; margin: 10px 20px 0; color: #FF7A2F; cursor: pointer; }
        .cover-preview { max-width: 100%; max-height: 150px; border-radius: 16px; margin-top: 8px; display: none; }
    </style>
</head>
<body>
<div class="app-container">
    <div class="status-bar"><span>9:41</span><span><i class="fas fa-signal"></i> <i class="fas fa-battery-full"></i></span></div>
    <div class="main-header">
        <div class="logo"><div class="logo-icon"><i class="fas fa-robot"></i></div><div class="logo-text">Bot Father</div></div>
        <div class="header-icons">
            <i class="fas fa-search" id="searchIcon"></i>
            <i class="far fa-bell" id="bellIcon"></i>
        </div>
    </div>
    <div class="main-content" id="mainContent"></div>
    <div class="bottom-nav">
        <div class="nav-item" data-tab="home"><i class="fas fa-home"></i><span>Home</span></div>
        <div class="nav-item" data-tab="discover"><i class="fas fa-compass"></i><span>Discover</span></div>
        <div class="nav-item" data-tab="arcade"><i class="fas fa-trophy"></i><span>Arcade</span></div>
        <div class="nav-item" data-tab="profile"><i class="fas fa-user"></i><span>Profile</span></div>
    </div>
</div>

<!-- Modals -->
<div id="gameModal" class="modal"><div class="modal-content" id="modalContent"></div></div>
<div id="authModal" class="modal"><div class="modal-content"><h3 id="authModalTitle"></h3><div id="authForm"><div class="form-group"><label>အသုံးပြုသူအမည်</label><input type="text" id="authUsername"></div><div class="form-group"><label>စကားဝှက်</label><input type="password" id="authPassword"></div><button class="btn-primary" id="authSubmitBtn"></button><p style="margin-top:16px; font-size:12px;"><span id="authToggleText"></span> <a href="#" id="authToggleLink" style="color:#FF7A2F;"></a></p></div><button class="btn-primary" id="closeAuthBtn" style="background:#2A3150; margin-top:12px;">ပိတ်ရန်</button></div></div>
<div id="editProfileModal" class="modal"><div class="modal-content"><h3>ပရိုဖိုင် တည်းဖြတ်ရန်</h3><div class="form-group"><label>အသုံးပြုသူအမည်</label><input type="text" id="editUsername"></div><div class="form-group"><label>ပရိုဖိုင်ပုံ URL</label><input type="text" id="editAvatar"></div><div class="form-group"><label>စကားဝှက်အသစ်</label><input type="password" id="editPassword"></div><button class="btn-primary" id="saveProfileBtn">သိမ်းမည်</button><button class="btn-primary" id="closeEditProfileBtn" style="background:#2A3150; margin-top:12px;">ပိတ်ရန်</button></div></div>
<div id="postModal" class="modal"><div class="modal-content"><h3>ဂိမ်းပို့စ်အသစ် တင်ရန်</h3><div class="form-group"><label>ခေါင်းစဉ်</label><input type="text" id="postTitle"></div><div class="form-group"><label>အမျိုးအစား</label><select id="postCategory"><option value="🔥 Bot Originals">🔥 Bot Originals</option><option value="👥 Multiplayer & IO">👥 Multiplayer & IO</option><option value="🏎️ Racing & Driving">🏎️ Racing & Driving</option><option value="🔫 Action & Shooting">🔫 Action & Shooting</option><option value="🧩 Puzzle & Brain">🧩 Puzzle & Brain</option></select></div><div class="form-group"><label>ကာဗာပုံ (ဖိုင်တင်ရန်)</label><input type="file" id="postCoverFile" accept="image/*"><img id="coverPreview" class="cover-preview"></div><div class="form-group"><label>အကြောင်းအရာ</label><textarea id="postDesc" rows="3"></textarea></div><div class="form-group"><label>Game Code (iframe)</label><textarea id="postGameCode" rows="4"></textarea></div><button class="btn-primary" id="submitPostBtn">ပို့စ်တင်မည်</button><button class="btn-primary" id="closePostBtn" style="background:#2A3150; margin-top:12px;">ပိတ်ရန်</button></div></div>

<script>
    // ---------- DATA ----------
    let posts = [];
    let users = {};
    let currentUser = null;
    let currentView = 'home';
    let selectedCategory = null;

    const ADMIN_USERNAME = "Ardamjamedv7";
    const ADMIN_PASSWORD = "admin123";

    // Load all data from localStorage
    function loadAllData() {
        const storedUsers = localStorage.getItem('botfather_users');
        if (storedUsers) {
            users = JSON.parse(storedUsers);
        } else {
            users = {};
            users[ADMIN_USERNAME] = { username: ADMIN_USERNAME, password: ADMIN_PASSWORD, avatar: "https://placehold.co/100x100/FF7A2F/white?text=Admin", isAdmin: true };
            users["demo"] = { username: "demo", password: "demo", avatar: "", isAdmin: false };
            saveUsers();
        }

        const storedPosts = localStorage.getItem('botfather_posts');
        if (storedPosts) {
            posts = JSON.parse(storedPosts);
        } else {
            posts = [
                { id: Date.now()+1, title: "Drift Hunters", category: "🏎️ Racing & Driving", cover: "https://placehold.co/400x200/FF7A2F/white?text=Drift+Hunters", description: "Drift racing game.", gameCode: "<iframe width='100%' height='200' src='https://www.crazygames.com/embed/drift-hunters' frameborder='0'></iframe>", createdAt: new Date().toISOString(), likes: 0, comments: [] },
                { id: Date.now()+2, title: "Venge.io", category: "🔥 Bot Originals", cover: "https://placehold.co/400x200/3EC1D3/white?text=Venge.io", description: "Shooter game.", gameCode: "<iframe width='100%' height='200' src='https://www.crazygames.com/embed/venge-io' frameborder='0'></iframe>", createdAt: new Date().toISOString(), likes: 0, comments: [] },
                { id: Date.now()+3, title: "Slither.io", category: "👥 Multiplayer & IO", cover: "https://placehold.co/400x200/6BDB5E/white?text=Slither.io", description: "IO game.", gameCode: "<iframe width='100%' height='200' src='https://www.crazygames.com/embed/slitherio' frameborder='0'></iframe>", createdAt: new Date().toISOString(), likes: 0, comments: [] },
                { id: Date.now()+4, title: "Moto X3M", category: "🏎️ Racing & Driving", cover: "https://placehold.co/400x200/F9C74F/white?text=Moto+X3M", description: "Stunt racing.", gameCode: "<iframe width='100%' height='200' src='https://www.crazygames.com/embed/moto-x3m' frameborder='0'></iframe>", createdAt: new Date().toISOString(), likes: 0, comments: [] }
            ];
            savePosts();
        }

        const storedCurrent = localStorage.getItem('botfather_current_user');
        if (storedCurrent) currentUser = JSON.parse(storedCurrent);
        else currentUser = null;
    }

    function saveUsers() { localStorage.setItem('botfather_users', JSON.stringify(users)); }
    function savePosts() { localStorage.setItem('botfather_posts', JSON.stringify(posts)); }
    function saveCurrentUser() { if (currentUser) localStorage.setItem('botfather_current_user', JSON.stringify(currentUser)); else localStorage.removeItem('botfather_current_user'); }

    // User functions
    function register(username, password) {
        if (users[username]) { alert('အသုံးပြုသူအမည် ရှိပြီးသား'); return false; }
        users[username] = { username, password, avatar: "", isAdmin: false };
        saveUsers();
        return true;
    }
    function login(username, password) {
        const user = users[username];
        if (user && user.password === password) {
            currentUser = { username: user.username, avatar: user.avatar || "", isAdmin: user.isAdmin || false };
            saveCurrentUser();
            return true;
        }
        return false;
    }
    function logout() { currentUser = null; saveCurrentUser(); render(); }
    function updateUserProfile(username, newAvatar, newPassword) {
        if (users[username]) {
            if (newAvatar !== undefined) users[username].avatar = newAvatar;
            if (newPassword && newPassword.trim() !== '') users[username].password = newPassword;
            saveUsers();
            if (currentUser && currentUser.username === username) {
                currentUser.avatar = users[username].avatar;
                saveCurrentUser();
            }
            return true;
        }
        return false;
    }

    // Post functions
    function addPost(title, category, coverBase64, description, gameCode) {
        posts.push({ 
            id: Date.now(), 
            title, 
            category, 
            cover: coverBase64 || "https://placehold.co/400x200/FF7A2F/white?text=Game", 
            description: description || "", 
            gameCode: gameCode || "", 
            createdAt: new Date().toISOString(),
            likes: 0,
            comments: []
        });
        savePosts();
    }
    function deletePost(postId) {
        if (!currentUser || !currentUser.isAdmin) return;
        posts = posts.filter(p => p.id !== postId);
        savePosts();
        render();
    }

    // Like a post
    function likePost(postId) {
        if (!currentUser) { alert('Like လုပ်ရန် အကောင့်ဝင်ပါ။'); return; }
        const post = posts.find(p => p.id === postId);
        if (post) {
            post.likes = (post.likes || 0) + 1;
            savePosts();
            const modal = document.getElementById('gameModal');
            if (modal.style.display === 'flex') {
                openPostModalDetail(postId);
            }
            render();
        }
    }

    // Add comment
    function addComment(postId, commentText) {
        if (!currentUser) { alert('မှတ်ချက်ရေးရန် အကောင့်ဝင်ပါ။'); return; }
        if (!commentText.trim()) return;
        const post = posts.find(p => p.id === postId);
        if (post) {
            if (!post.comments) post.comments = [];
            post.comments.push({
                user: currentUser.username,
                text: commentText.trim(),
                timestamp: new Date().toISOString()
            });
            savePosts();
            const modal = document.getElementById('gameModal');
            if (modal.style.display === 'flex') {
                openPostModalDetail(postId);
            }
            render();
        }
    }

    // Share functions
    function sharePost(post, platform) {
        const url = encodeURIComponent(window.location.href);
        const title = encodeURIComponent(post.title);
        const text = encodeURIComponent(post.description);
        if (platform === 'facebook') {
            window.open(`https://www.facebook.com/sharer/sharer.php?u=${url}`, '_blank');
        } else if (platform === 'twitter') {
            window.open(`https://twitter.com/intent/tweet?text=${title} - ${text}&url=${url}`, '_blank');
        } else if (platform === 'copy') {
            navigator.clipboard.writeText(window.location.href);
            alert('လင့်ခ်ကို ကူးယူပြီးပါပြီ။');
        }
    }

    // Open post detail modal with like, comment, share
    function openPostModalDetail(postId) {
        const post = posts.find(p => p.id === postId);
        if (!post) return;
        const modal = document.getElementById('gameModal');
        const modalContent = document.getElementById('modalContent');
        modalContent.innerHTML = `
            <h3>${escapeHtml(post.title)}</h3>
            <img src="${post.cover}" onerror="this.src='https://placehold.co/400x200/FF7A2F/white?text=Cover'">
            <p>${escapeHtml(post.description)}</p>
            <div>${post.gameCode || '<i>Game code not provided</i>'}</div>
            <div class="post-stats">
                <div class="like-btn" onclick="window.likePost(${post.id})">
                    <i class="fas fa-heart"></i> ${post.likes || 0}
                </div>
                <div class="share-btn" onclick="window.sharePost(${post.id}, 'copy')">
                    <i class="fas fa-share-alt"></i> မျှဝေရန်
                </div>
            </div>
            <div class="share-buttons">
                <i class="fab fa-facebook" onclick="window.sharePost(${post.id}, 'facebook')"></i>
                <i class="fab fa-twitter" onclick="window.sharePost(${post.id}, 'twitter')"></i>
                <i class="fas fa-link" onclick="window.sharePost(${post.id}, 'copy')"></i>
            </div>
            <div class="comments-section">
                <h4>မှတ်ချက်များ (${post.comments?.length || 0})</h4>
                <div id="commentsList"></div>
                <div class="comment-form">
                    <input type="text" id="commentInput" placeholder="မှတ်ချက်ရေးရန်...">
                    <button onclick="window.addCommentFromModal(${post.id})">ပို့ရန်</button>
                </div>
            </div>
        `;
        const commentsDiv = modalContent.querySelector('#commentsList');
        if (post.comments && post.comments.length) {
            post.comments.slice().reverse().forEach(c => {
                const date = new Date(c.timestamp).toLocaleString();
                const div = document.createElement('div');
                div.className = 'comment-item';
                div.innerHTML = `<div><span class="comment-user">${escapeHtml(c.user)}</span><span class="comment-time">${date}</span></div><div class="comment-text">${escapeHtml(c.text)}</div>`;
                commentsDiv.appendChild(div);
            });
        } else {
            commentsDiv.innerHTML = '<p style="color:#8F9BB9;">မှတ်ချက်မရှိသေးပါ။</p>';
        }
        modal.style.display = 'flex';
    }

    // Helper functions
    function escapeHtml(str) { if (!str) return ''; return str.replace(/[&<>]/g, m => ({ '&':'&amp;', '<':'&lt;', '>':'&gt;' }[m])); }

    function createGameCardFromPost(post) {
        const card = document.createElement('div');
        card.className = 'game-item';
        const coverUrl = post.cover && post.cover.trim() !== '' ? post.cover : 'https://placehold.co/100x100/FF7A2F/white?text=Game';
        card.innerHTML = `<img src="${coverUrl}" onerror="this.src='https://placehold.co/100x100/FF7A2F/white?text=Game'"><div class="game-name">${escapeHtml(post.title)}</div><div class="game-category">${escapeHtml(post.category)}</div><div><i class="fas fa-heart" style="color:#FF7A2F;"></i> ${post.likes || 0}</div>`;
        card.addEventListener('click', () => openPostModalDetail(post.id));
        return card;
    }

    // Render functions
    function renderHome() {
        const container = document.getElementById('mainContent');
        container.innerHTML = '';
        const featuredPosts = posts.slice(-5).reverse();
        if (featuredPosts.length) {
            const featDiv = document.createElement('div'); featDiv.className = 'featured-section';
            featDiv.innerHTML = `<div class="section-label"><h3><i class="fas fa-star"></i> အထူးပြသမှုများ</h3><span>👉 ဆွဲပွတ်ကြည့်ရန်</span></div>`;
            const carouselDiv = document.createElement('div'); carouselDiv.className = 'featured-carousel';
            featuredPosts.forEach(post => {
                const card = document.createElement('div'); card.className = 'featured-card';
                card.innerHTML = `<div class="game-icon"><img src="${post.cover}" onerror="this.src='https://placehold.co/70x70/FF7A2F/white?text=Game'"></div><div class="featured-info"><h4>${escapeHtml(post.title)}</h4><p>${escapeHtml(post.category)} · ${new Date(post.createdAt).toLocaleDateString()}</p><span class="play-badge">Play now</span></div>`;
                card.addEventListener('click', () => openPostModalDetail(post.id));
                carouselDiv.appendChild(card);
            });
            featDiv.appendChild(carouselDiv);
            container.appendChild(featDiv);
        }
        const categoriesMap = new Map();
        posts.forEach(p => { if (!categoriesMap.has(p.category)) categoriesMap.set(p.category, []); categoriesMap.get(p.category).push(p); });
        for (let [catName, catPosts] of categoriesMap.entries()) {
            const rowDiv = document.createElement('div'); rowDiv.className = 'category-row';
            const header = document.createElement('div'); header.className = 'row-header';
            header.innerHTML = `<h4>${catName}</h4><a class="see-all-link" data-cat="${catName}">အားလုံး (${catPosts.length}) <i class="fas fa-angle-right"></i></a>`;
            const horiz = document.createElement('div'); horiz.className = 'games-horizontal';
            catPosts.forEach(p => horiz.appendChild(createGameCardFromPost(p)));
            rowDiv.appendChild(header); rowDiv.appendChild(horiz);
            container.appendChild(rowDiv);
        }
        document.querySelectorAll('.see-all-link').forEach(link => {
            link.addEventListener('click', (e) => { e.preventDefault(); selectedCategory = link.getAttribute('data-cat'); currentView = 'category'; renderCategoryView(selectedCategory); setActiveNav('home'); });
        });
    }
    function renderCategoryView(categoryName) {
        const container = document.getElementById('mainContent');
        const catPosts = posts.filter(p => p.category === categoryName);
        container.innerHTML = `<div style="padding:12px 20px 0;"><div class="back-link" id="backToHomeBtn"><i class="fas fa-arrow-left"></i> နောက်သို့</div></div><div class="section-label"><h3>${categoryName}</h3><span>ဂိမ်း ${catPosts.length} ခု</span></div><div class="games-horizontal" style="flex-wrap:wrap; overflow-x:visible; gap:16px; justify-content:flex-start;"></div>`;
        const gridContainer = container.querySelector('.games-horizontal');
        catPosts.forEach(p => gridContainer.appendChild(createGameCardFromPost(p)));
        document.getElementById('backToHomeBtn')?.addEventListener('click', () => { currentView = 'home'; renderHome(); setActiveNav('home'); });
    }
    function renderDiscover() {
        const container = document.getElementById('mainContent');
        container.innerHTML = `<div class="section-label"><h3>📱 ဂိမ်းအားလုံး (${posts.length})</h3><span>ဆွဲပွတ်ကြည့်ရန်</span></div><div class="games-horizontal"></div>`;
        const horiz = container.querySelector('.games-horizontal');
        posts.forEach(p => horiz.appendChild(createGameCardFromPost(p)));
    }
    function renderArcade() {
        const container = document.getElementById('mainContent');
        const topGames = posts.slice(0, 10);
        container.innerHTML = `<div class="section-label"><h3>🏆 Arcade ထိပ်တန်းဂိမ်းများ</h3><span>ဆွဲပွတ်ကြည့်ရန်</span></div><div class="games-horizontal"></div>`;
        const horiz = container.querySelector('.games-horizontal');
        topGames.forEach(p => horiz.appendChild(createGameCardFromPost(p)));
    }
    function renderProfile() {
        const container = document.getElementById('mainContent');
        if (!currentUser) {
            container.innerHTML = `<div class="section-label"><h3>👤 Profile</h3></div><div style="padding:20px;text-align:center;"><p style="color:white;margin-bottom:20px;">အကောင့်ဝင်ရန် လိုအပ်ပါသည်။</p><button class="btn-primary" id="gotoLoginBtn">အကောင့်ဝင်ရန် / စာရင်းသွင်းရန်</button></div>`;
            document.getElementById('gotoLoginBtn')?.addEventListener('click', () => showAuthModal(false));
            return;
        }
        const isAdmin = currentUser.isAdmin;
        const avatarUrl = currentUser.avatar?.trim() || 'https://placehold.co/100x100/FF7A2F/white?text=User';
        container.innerHTML = `<div class="section-label"><h3>👤 ${currentUser.username} ${isAdmin ? '(Admin)' : ''}</h3></div><div style="padding:20px;"><div class="profile-avatar"><img src="${avatarUrl}" style="width:100%;height:100%;border-radius:50%;object-fit:cover;" onerror="this.src='https://placehold.co/100x100/FF7A2F/white?text=User'"></div><div class="profile-info"><p><strong>${currentUser.username}</strong></p><p>Bot Father User</p><p>ဂိမ်းကစားသူ အသုံးပြုသူ</p></div><div class="profile-actions"><button class="btn-outline" id="editProfileBtn">ပရိုဖိုင် တည်းဖြတ်ရန်</button>${isAdmin ? '<button class="btn-outline" id="createPostBtn">+ ပို့စ်အသစ်</button>' : ''}<button class="btn-outline" id="logoutProfileBtn">ထွက်ရန်</button></div><div id="adminPostList"></div></div>`;
        document.getElementById('editProfileBtn')?.addEventListener('click', showEditProfileModal);
        document.getElementById('logoutProfileBtn')?.addEventListener('click', () => { logout(); render(); });
        if (isAdmin) {
            document.getElementById('createPostBtn')?.addEventListener('click', openPostModal);
            const listDiv = document.getElementById('adminPostList');
            if (listDiv) {
                listDiv.innerHTML = '<h4 style="margin:20px 0 10px;">ပို့စ်များ (စီမံရန်)</h4>';
                posts.forEach(post => {
                    const item = document.createElement('div'); item.className = 'post-list-item';
                    item.innerHTML = `<div><b>${escapeHtml(post.title)}</b><br><small>${escapeHtml(post.category)}</small></div><button class="delete-btn" data-id="${post.id}">🗑️ ဖျက်မည်</button>`;
                    listDiv.appendChild(item);
                });
                document.querySelectorAll('.delete-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        e.stopPropagation();
                        const id = parseInt(btn.getAttribute('data-id'));
                        if (confirm('ဤပို့စ်ကို ဖျက်မည်လား?')) deletePost(id);
                    });
                });
            }
        }
    }

    // Modal and UI helpers
    function openPostModal() { 
        document.getElementById('postModal').style.display = 'flex';
        // Reset preview
        document.getElementById('coverPreview').style.display = 'none';
        document.getElementById('postCoverFile').value = '';
    }
    
    // Convert uploaded file to base64
    function handleCoverUpload(file, callback) {
        if (!file) return callback(null);
        const reader = new FileReader();
        reader.onload = function(e) {
            callback(e.target.result);
        };
        reader.onerror = function() {
            alert('ဖိုင်ဖတ်ရန် မအောင်မြင်ပါ။');
            callback(null);
        };
        reader.readAsDataURL(file);
    }

    function submitPost() {
        const title = document.getElementById('postTitle').value.trim();
        const category = document.getElementById('postCategory').value;
        const fileInput = document.getElementById('postCoverFile');
        const desc = document.getElementById('postDesc').value.trim();
        const gameCode = document.getElementById('postGameCode').value.trim();
        if (!title) { alert('ခေါင်းစဉ် ထည့်ပါ'); return; }
        
        if (fileInput.files.length > 0) {
            handleCoverUpload(fileInput.files[0], function(base64) {
                addPost(title, category, base64, desc, gameCode);
                finishPostSubmit();
            });
        } else {
            addPost(title, category, null, desc, gameCode);
            finishPostSubmit();
        }
    }
    
    function finishPostSubmit() {
        document.getElementById('postModal').style.display = 'none';
        document.getElementById('postTitle').value = '';
        document.getElementById('postCoverFile').value = '';
        document.getElementById('postDesc').value = '';
        document.getElementById('postGameCode').value = '';
        document.getElementById('coverPreview').style.display = 'none';
        render();
        alert('ပို့စ်တင်ခြင်း ပြီးပါပြီ။');
    }
    
    function showAuthModal(registerMode) {
        const modal = document.getElementById('authModal');
        const title = document.getElementById('authModalTitle');
        const submitBtn = document.getElementById('authSubmitBtn');
        const toggleText = document.getElementById('authToggleText');
        const toggleLink = document.getElementById('authToggleLink');
        if (registerMode) {
            title.innerText = 'စာရင်းသွင်းရန်'; submitBtn.innerText = 'စာရင်းသွင်းမည်';
            toggleText.innerText = 'အကောင့်ရှိပြီးသား? '; toggleLink.innerText = 'ဝင်ရန်';
        } else {
            title.innerText = 'အကောင့်ဝင်ရန်'; submitBtn.innerText = 'ဝင်မည်';
            toggleText.innerText = 'အကောင့်မရှိသေးဘူး? '; toggleLink.innerText = 'စာရင်းသွင်းရန်';
        }
        document.getElementById('authUsername').value = '';
        document.getElementById('authPassword').value = '';
        modal.style.display = 'flex';
        modal.dataset.mode = registerMode ? 'register' : 'login';
    }
    function closeAuthModal() { document.getElementById('authModal').style.display = 'none'; }
    function handleAuthSubmit() {
        const modal = document.getElementById('authModal');
        const mode = modal.dataset.mode;
        const username = document.getElementById('authUsername').value.trim();
        const password = document.getElementById('authPassword').value;
        if (!username || !password) { alert('အချက်အလက်အားလုံးဖြည့်ပါ'); return; }
        if (mode === 'register') {
            if (register(username, password)) { alert('စာရင်းသွင်းပြီးပါပြီ။ အကောင့်ဝင်ပါ။'); showAuthModal(false); }
        } else {
            if (login(username, password)) { closeAuthModal(); render(); }
            else alert('အသုံးပြုသူအမည် သို့မဟုတ် စကားဝှက် မှားနေပါသည်။');
        }
    }
    function showEditProfileModal() {
        if (!currentUser) return;
        document.getElementById('editUsername').value = currentUser.username;
        document.getElementById('editAvatar').value = currentUser.avatar || '';
        document.getElementById('editPassword').value = '';
        document.getElementById('editProfileModal').style.display = 'flex';
    }
    function closeEditProfileModal() { document.getElementById('editProfileModal').style.display = 'none'; }
    function saveProfileChanges() {
        const newUsername = document.getElementById('editUsername').value.trim();
        const newAvatar = document.getElementById('editAvatar').value.trim();
        const newPassword = document.getElementById('editPassword').value;
        if (!newUsername) { alert('အသုံးပြုသူအမည် လိုအပ်ပါသည်။'); return; }
        if (newUsername !== currentUser.username) {
            if (users[newUsername]) { alert('အသုံးပြုသူအမည် ရှိပြီးသား'); return; }
            const oldUser = users[currentUser.username];
            users[newUsername] = { ...oldUser, username: newUsername, avatar: newAvatar };
            if (newPassword.trim()) users[newUsername].password = newPassword;
            delete users[currentUser.username];
            saveUsers();
            currentUser.username = newUsername;
            currentUser.avatar = newAvatar;
            saveCurrentUser();
        } else {
            updateUserProfile(currentUser.username, newAvatar, newPassword);
        }
        closeEditProfileModal();
        render();
    }
    function setActiveNav(tab) {
        document.querySelectorAll('.nav-item').forEach(item => {
            if (item.getAttribute('data-tab') === tab) item.classList.add('active');
            else item.classList.remove('active');
        });
    }
    function render() {
        if (currentView === 'home') { renderHome(); setActiveNav('home'); }
        else if (currentView === 'category') { if (selectedCategory) renderCategoryView(selectedCategory); else { currentView = 'home'; renderHome(); setActiveNav('home'); } }
        else if (currentView === 'discover') { renderDiscover(); setActiveNav('discover'); }
        else if (currentView === 'arcade') { renderArcade(); setActiveNav('arcade'); }
        else if (currentView === 'profile') { renderProfile(); setActiveNav('profile'); }
    }

    function initBottomNav() {
        document.querySelectorAll('.nav-item').forEach(item => {
            item.addEventListener('click', () => {
                const tab = item.getAttribute('data-tab');
                if (tab === 'home') { currentView = 'home'; selectedCategory = null; render(); }
                else if (tab === 'discover') { currentView = 'discover'; render(); }
                else if (tab === 'arcade') { currentView = 'arcade'; render(); }
                else if (tab === 'profile') { currentView = 'profile'; render(); }
            });
        });
    }
    function initHeader() {
        document.getElementById('searchIcon').addEventListener('click', () => alert('🔍 ရှာဖွေမှု မကြာမီလာမည်။'));
        document.getElementById('bellIcon').addEventListener('click', () => alert('🔔 အသိပေးချက်များ ယခုတွင် မရှိသေးပါ။'));
    }
    function bindModals() {
        document.getElementById('gameModal').addEventListener('click', (e) => { if (e.target === document.getElementById('gameModal')) document.getElementById('gameModal').style.display = 'none'; });
        document.getElementById('closeAuthBtn').addEventListener('click', closeAuthModal);
        document.getElementById('authSubmitBtn').addEventListener('click', handleAuthSubmit);
        document.getElementById('authToggleLink').addEventListener('click', (e) => { e.preventDefault(); const modal = document.getElementById('authModal'); showAuthModal(modal.dataset.mode !== 'register'); });
        document.getElementById('closeEditProfileBtn').addEventListener('click', closeEditProfileModal);
        document.getElementById('saveProfileBtn').addEventListener('click', saveProfileChanges);
        document.getElementById('editProfileModal').addEventListener('click', (e) => { if (e.target === document.getElementById('editProfileModal')) closeEditProfileModal(); });
        document.getElementById('closePostBtn').addEventListener('click', () => document.getElementById('postModal').style.display = 'none');
        document.getElementById('submitPostBtn').addEventListener('click', submitPost);
        
        // Preview cover image when file selected
        const fileInput = document.getElementById('postCoverFile');
        const preview = document.getElementById('coverPreview');
        fileInput.addEventListener('change', function() {
            if (this.files && this.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    preview.src = e.target.result;
                    preview.style.display = 'block';
                };
                reader.readAsDataURL(this.files[0]);
            } else {
                preview.style.display = 'none';
            }
        });
    }

    // Attach global functions for modal calls
    window.likePost = function(postId) { likePost(postId); };
    window.sharePost = function(postId, platform) {
        const post = posts.find(p => p.id === postId);
        if (post) sharePost(post, platform);
    };
    window.addCommentFromModal = function(postId) {
        const input = document.querySelector('#gameModal .comment-form input');
        if (input) addComment(postId, input.value);
        input.value = '';
    };

    function init() { loadAllData(); initBottomNav(); initHeader(); bindModals(); render(); }
    init();
</script>
</body>
</html>
