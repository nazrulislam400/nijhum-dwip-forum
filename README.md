# nijhum-dwip-forum

<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>নিঝুমদ্বীপ ফোরাম</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css">
<style>
  :root {
    --primary: #3498db;
    --primary-dark: #2980b9;
    --success: #27ae60;
    --wa: #25d366;
    --gray: #95a5a6;
    --bg: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body {
    font-family: 'Noto Sans Bengali', sans-serif;
    background: #f0f2f5;
    min-height: 100vh;
    padding: 70px 0 80px;
    overflow-x: hidden;
  }
  #loader {
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    background: var(--bg); color: white; z-index: 9999;
    display: flex; flex-direction: column; justify-content: center; align-items: center;
    transition: opacity 0.6s;
  }
  .spinner {
    width: 60px; height: 60px; border: 6px solid rgba(255,255,255,0.3);
    border-top: 6px solid white; border-radius: 50%;
    animation: spin 1s linear infinite; margin-bottom: 20px;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  .topbar {
    position: fixed; top: 0; left: 0; right: 0; z-index: 998;
    background: var(--bg); color: white; padding: 18px;
    text-align: center; font-size: 22px; font-weight: 700;
    box-shadow: 0 4px 20px rgba(0,0,0,0.2);
  }
  .page { display: none; animation: fadeIn 0.4s; }
  .page.active { display: block; }
  @keyframes fadeIn { from {opacity:0; transform:translateY(20px);} to {opacity:1; transform:none;} }

  .card {
    background: white; border-radius: 20px; padding: 25px;
    margin: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    text-align: center;
  }
  input, button {
    width: 100%; padding: 16px; margin: 12px 0; border-radius: 15px;
    border: none; font-size: 16px; outline: none;
  }
  input { border: 2px solid #eee; }
  button {
    background: var(--primary); color: white; font-weight: 600;
    cursor: pointer; transition: all 0.3s;
  }
  button:hover { transform: translateY(-3px); box-shadow: 0 10px 25px rgba(52,152,219,0.4); }
  .btn-wa { background: var(--wa); }
  .btn-call { background: var(--success); margin-bottom: 8px; }

  #searchBox {
    position: fixed; top: 70px; left: 15px; right: 15px; z-index: 997;
    background: white; padding: 12px; border-radius: 15px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.12);
  }

  .friend {
    background: white; border-radius: 18px; padding: 18px; margin: 15px;
    display: flex; align-items: center; box-shadow: 0 8px 25px rgba(0,0,0,0.08);
    transition: 0.3s;
  }
  .friend:hover { transform: translateY(-5px); box-shadow: 0 15px 35px rgba(0,0,0,0.12); }
  .friend img {
    width: 60px; height: 60px; border-radius: 50%; object-fit: cover;
    border: 4px solid var(--primary);
  }
  .info { flex: 1; margin-left: 15px; text-align: left; }
  .info b { font-size: 18px; color: #2c3e50; display: block; }
  .info small { color: #7f8c8d; font-size: 14px; }

  .bottom-nav {
    position: fixed; bottom: 0; left: 0; right: 0; background: white;
    display: flex; justify-content: space-around; padding: 10px 0 20px;
    box-shadow: 0 -5px 25px rgba(0,0,0,0.15); z-index: 999;
  }
  .nav-item {
    { text-align: center; padding: 10px; color: var(--gray); transition: 0.3s; }
  .nav-item i { font-size: 26px; display: block; margin-bottom: 4px; }
  .nav-item.active { color: var(--primary); transform: scale(1.15); }

  .profile-big {
    width: 130px; height: 130px; border-radius: 50%; object-fit: cover;
    border: 6px solid white; box-shadow: 0 10px 30px rgba(52,152,219,0.4);
    margin: 20px auto; display: block;
  }
</style>
</head>
<body>

<div id="loader">
  <div class="spinner"></div>
  <h2>নিঝুমদ্বীপ ফোরাম</h2>
  <p>লোড হচ্ছে...</p>
</div>

<div class="topbar" id="topTitle">নিঝুমদ্বীপ ফোরাম</div>

<!-- Login Page -->
<div id="loginPage" class="page active">
  <div class="card">
    <img src="https://img.icons8.com/fluency/96/school.png" style="width:90px;">
    <h2 style="margin:20px 0; color:var(--primary);">স্বাগতম</h2>
    <input type="text" id="userName" placeholder="আপনার পুরো নাম লিখুন">
    <input type="text" id="userPhone" placeholder="মোবাইল নাম্বার (017xxxxxxxx)">
    <input type="file" id="photoInput" accept="image/*" style="display:none;">
    <img id="photoPreview" src="https://via.placeholder.com/130/3498db/fff?text=আপলোড" class="profile-big">
    <button onclick="document.getElementById('photoInput').click()" style="background:var(--gray);">
      প্রোফাইল ছবি যোগ করুন
    </button>
    <button onclick="login()">লগইন করুন</button>
  </div>
</div>

<!-- Home Page -->
<div id="homePage" class="page">
  <div style="text-align:center; padding:20px 0;">
    <img id="myPhoto" class="profile-big" src="">
    <h2 style="color:var(--primary); margin:15px 0;">স্বাগতম, <span id="myName"></span>!</h2>
  </div>

  <div id="searchBox">
    <input type="text" id="search" placeholder="নাম, ব্যাচ, নাম্বার দিয়ে খুঁজুন..." onkeyup="searchFriends()">
  </div>

  <button onclick="go('addPage')" style="margin:20px 15px; background:var(--success);">
    নতুন বন্ধু যোগ করুন
  </button>

  <div id="friendList"></div>
</div>

<!-- Add Friend Page -->
<div id="addPage" class="page">
  <div class="card">
    <h3 style="color:var(--primary);">নতুন বন্ধু যোগ করুন</h3>
    <input type="text" id="fName" placeholder="পুরো নাম *">
    <input type="text" id="fSchool" placeholder="স্কুল / মাদ্রাসা (ঐচ্ছিক)">
    <input type="text" id="fYear" placeholder="ব্যাচ (যেমন: ২০১৫)">
    <input type="text" id="fPhone" placeholder="মোবাইল নাম্বার *">
    <button onclick="addFriend()" style="background:var(--success);">সেভ করুন</button>
    <button onclick="go('homePage')" style="background:var(--gray);">বাতিল করুন</button>
  </div>
</div>

<!-- Bottom Navigation -->
<div class="bottom-nav">
  <div class="nav-item active" onclick="go('homePage')"><i class="fas fa-home"></i><div>হোম</div></div>
  <div class="nav-item" onclick="loadFriends()"><i class="fas fa-users"></i><div>বন্ধু</div></div>
  <div class="nav-item" onclick="alert('চ্যাট ফিচার শীঘ্রই আসছে!')"><i class="fas fa-comments"></i><div>চ্যাট</div></div>
  <div class="nav-item" onclick="alert('প্রোফাইল শীঘ্রই আসছে')"><i class="fas fa-user"></i><div>প্রোফাইল</div></div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
  import { getDatabase, ref, push, set, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
  import { getStorage, ref as sRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-storage.js";

  const app = initializeApp({
    apiKey: "AIzaSyCy0ufC2TgNRYIYKHeKnjkRlElMFpdDkwI",
    authDomain: "nijhum-dwip-forum.firebaseapp.com",
    databaseURL: "https://nijhum-dwip-forum-default-rtdb.firebaseio.com",
    projectId: "nijhum-dwip-forum",
    storageBucket: "nijhum-dwip-forum.appspot.com",
    appId: "1:1084749156846:web:d45ad53a9b2f3616befeff"
  });

  const db = getDatabase(app);
  const storage = getStorage(app);
  let user = null;
  let allFriends = [];

  // Hide loader
  setTimeout(() => {
    document.getElementById("loader").style.opacity = "0";
    setTimeout(() => document.getElementById("loader").style.display = "none", 600);
  }, 800);

  window.go = function(page) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(page).classList.add('active');
    document.getElementById("topTitle").innerText = {
      homePage: "নিঝুমদ্বীপ ফোরাম",
      addPage: "নতুন বন্ধু যোগ করুন",
    }[page] || "নিঝুমদ্বীপ ফোরাম";

    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    if(page === 'homePage') {
      document.querySelectorAll('.navathi-item')[0].classList.add('active');
      document.querySelectorAll('.nav-item')[1].classList.add('active');
    }
  }

  // Photo preview
  document.getElementById("photoInput").onchange = e => {
    const file = e.target.files[0];
    if(file) {
      const reader = new FileReader();
      reader.onload = ev => document.getElementById("photoPreview").src = ev.target.result;
      reader.readAsDataURL(file);
    }
  }

  // Login
  window.login = async () => {
    const name = document.getElementById("userName").value.trim();
    const phone = document.getElementById("userPhone").value.trim();
    if(!name || !phone) return alert("নাম ও মোবাইল নাম্বার দিন");

    let photoURL = "https://img.icons8.com/fluency/96/user-male-circle.png";
    const file = document.getElementById("photoInput").files[0];
    if(file) {
      const storageRef = sRef(storage, 'profiles/' + Date.now() + '.jpg');
      await uploadBytes(storageRef, file);
      photoURL = await getDownloadURL(storageRef);
    }

    user = { name, phone, photo: photoURL };
    localStorage.setItem("ndUser", JSON.stringify(user));
    location.reload();
  }

  // Auto login if exists
  const saved = localStorage.getItem("ndUser");
  if(saved) {
    user = JSON.parse(saved);
    document.getElementById("myName").innerText = user.name;
    document.getElementById("myPhoto").src = user.photo;
    go('homePage');
    loadFriends();
  }

  // Add Friend
  window.addFriend = () => {
    const name = document.getElementById("fName").value.trim();
    const phone = document.getElementById("fPhone").value.trim();
    if(!name || !phone) return alert("নাম ও নাম্বার আবশ্যক!");

    push(ref(db, 'friends'), {
      name,
      school: document.getElementById("fSchool").value.trim() || "—",
      year: document.getElementById("fYear").value.trim() || "—",
      phone,
      addedBy: user.phone,
      time: new Date().toLocaleString('bn-BD')
    }).then(() => {
      alert("সফলভাবে যোগ হয়েছে!");
      document.getElementById("fName").value = "";
      document.getElementById("fPhone").value = "";
      document.getElementById("fSchool").value = "";
      document.getElementById("fYear").value = "";
      go('homePage');
    }).catch(err => alert("Error: " + err.message));
  }

  // Load & Render Friends
  window.loadFriends = () => {
    onValue(ref(db, 'friends'), snap => {
      allFriends = [];
      snap.forEach(child => allFriends.push(child.val()));
      allFriends.sort((a,b) => a.name.localeCompare(b.name, 'bn'));
      renderFriends(allFriends);
    }, { onlyOnce: false });
  }

  function renderFriends(list) {
    const container = document.getElementById("friendList");
    if(list.length === 0) {
      container.innerHTML = `<p style="text-align:center; color:#999; padding:40px;">কোনো বন্ধু যোগ করা হয়নি</p>`;
      return;
    }
    container.innerHTML = list.map(f => `
      <div class="friend">
        <img src="${f.photo || 'https://img.icons8.com/fluency/96/user-male-circle.png'}">
        <div class="info">
          <b>${f.name}</b>
          <small>${f.school} • ${f.year} ব্যাচ</small>
          <small>মোবাইল: ${f.phone}</small>
        </div>
        <div style="display:flex; flex-direction:column; gap:8px;">
          <button class="btn-call" onclick="location.href='tel:${f.phone}'">
            <i class="fas fa-phone"></i> কল
          </button>
          <button class="btn-wa" onclick="window.open('https://wa.me/88${f.phone.replace(/[^0-9]/g,'')}')">
            <i class="fab fa-whatsapp"></i> WhatsApp
          </button>
        </div>
      </div>
    `).join('');
  }

  // Search
  window.searchFriends = () => {
    const query = document.getElementById("search").value.trim();
    if(!query) return renderFriends(allFriends);
    const filtered = allFriends.filter(f =>
      f.name.toLowerCase().includes(query.toLowerCase()) ||
      f.phone.includes(query) ||
      f.year.includes(query) ||
      f.school.toLowerCase().includes(query.toLowerCase())
    );
    renderFriends(filtered);
  }

  // Start loading friends when home page opens
  if(saved) loadFriends();
</script>
</body>
</html>
