<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>abai個人作品集 </title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&display=swap" rel="stylesheet">
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0a0a0a;
            --text-main: #ffffff;
            --text-sub: #a0a0a0;
            --accent-gray: #333333;
            --hover-gray: #1a1a1a;
            --project-overlay: rgba(0, 0, 0, 0.7); /* 作品覆蓋層顏色 */
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        html {
            scroll-behavior: smooth; /* 平滑滾動 */
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* 導覽列 */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            padding: 2rem 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            background: rgba(10, 10, 10, 0.8);
            backdrop-filter: blur(10px);
            transition: background 0.3s ease-in-out; /* 滾動時背景變化 */
        }

        .logo { 
            font-weight: 700; 
            font-size: 1.5rem; 
            letter-spacing: 2px; 
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .logo:hover {
            transform: scale(1.05); /* Logo 懸停放大 */
        }

        .nav-links a {
            color: var(--text-main);
            text-decoration: none;
            margin-left: 2rem;
            font-size: 0.9rem;
            position: relative;
            transition: color 0.3s;
        }

        .nav-links a::after { /* 導覽列底部劃線動畫 */
            content: '';
            position: absolute;
            left: 0;
            bottom: -5px;
            width: 0;
            height: 1px;
            background-color: var(--text-main);
            transition: width 0.3s ease-out;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        /* 首頁區塊 */
        section {
            padding: 100px 10%;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            position: relative; /* 用於粒子背景定位 */
            z-index: 1; /* 確保內容在粒子上方 */
        }

        .hero { 
            text-align: center; 
            overflow: hidden; /* 確保粒子不會溢出 */
        }
        .hero h1 { 
            font-size: 5rem; 
            font-weight: 800; 
            margin-bottom: 1rem; 
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.3); /* 文字微光 */
        letter-spacing: .3rem;
        }
        .hero p { 
            color: var(--text-sub); 
            font-size: 1.2rem; 
            letter-spacing: 0.5px;
            color:#fff;
            letter-spacing: 0.3rem;
        }

        /* 粒子背景容器 */
        #particles-js {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), 
                url("bn2.jpg");
            background-size: cover;
            width:100%;
            z-index: -1; /* 確保在內容下方 */
            
        }
        .work h2{

        }

        /* 作品集網格 */
        .portfolio-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 50px;
            font-weight: 800;
        }
        

        .project-card {
            background: var(--accent-gray);
            height: 400px;
            position: relative;
            overflow: hidden;
            cursor: pointer;
            border-radius: 8px; /* 圓角 */
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2); /* 陰影 */
            transition: transform 0.5s cubic-bezier(0.165, 0.84, 0.44, 1), box-shadow 0.3s ease-in-out;
        }

        .project-card:hover {
            transform: translateY(-15px); /* 懸停上浮更多 */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4); /* 懸停陰影加深 */
        }

        .project-card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: grayscale(100%);
            transition: 0.6s ease-out; /* 變回彩色動畫更平滑 */
            opacity: 0.6;
        }
        /* 圖片佔位符 */
        .project-card .placeholder-bg {
            width: 100%;
            height: 100%;
            background-color: var(--accent-gray); /* 預設深灰色 */
            transition: background-color 0.6s ease-out;
        }


        .project-card:hover img {
            filter: grayscale(0%);
            opacity: 1;
            transform: scale(1.05); /* 圖片輕微放大 */
        }
        .project-card:hover .placeholder-bg {
             background-color: var(--hover-gray); /* 佔位符背景變深 */
        }


        .project-info {
            position: absolute;
            padding:10px;
            border-radius: 0 0 10px 10px;
            bottom: 20px;
            left: 20px;
            right: 20px;
            z-index: 2;
            opacity: 0; /* 預設隱藏 */
            transform: translateY(20px); /* 預設位移 */
            transition: opacity 0.4s ease-out, transform 0.4s ease-out;
            background: linear-gradient(to top, var(--project-overlay) 0%, transparent 100%); /* 漸層背景 */
            padding-top: 50px; /* 留出文字空間 */
        }
        
        .project-card::before { /* 覆蓋層，讓文字更突出 */
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            
            opacity: 1;
            transition: opacity 0.4s ease-out;
            z-index: 1;
        }

        .project-card:hover::before {
            opacity: 0; /* 懸停時覆蓋層消失 */
        }

        .project-card:hover .project-info {
            opacity: 1; /* 懸停時顯示 */
            transform: translateY(0); /* 歸位 */
        }
        
        .project-info h3 {
            font-size: 1.8rem;
            margin-bottom: 0.5rem;
            color: var(--text-main);
            text-shadow: 0 0 5px rgba(0, 0, 0, 0.7);
        }
        .project-info p {
            font-size: 1rem;
            color: #c0c0c0;
            letter-spacing: .2rem;
        }

        /* 關於我 */
        .about-content {
            max-width: 800px;
            font-size: 1.1rem;
            color: var(--text-sub);
            text-align: left;
        }

        .skill-list {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            margin-top: 2rem;
        }

        .skill-tag {
            padding: 8px 20px;
            border: 1px solid var(--accent-gray);
            border-radius: 50px;
            font-size: 0.8rem;
            transition: background-color 0.3s ease, border-color 0.3s ease, color 0.3s ease;
        }
        .skill-tag:hover {
            background-color: var(--accent-gray);
            border-color: var(--text-main);
            color: var(--text-main);
        }
.video-section {
    background-color: #000; /* 影片載入前的底色 */
}

/* 影片本人 */
.bg-video {
    position: absolute;
    top: 50%;
    left: 50%;
    min-width: 100%;
    min-height: 100%;
    width: auto;
    height: auto;
    transform: translate(-50%, -50%);
    object-fit: cover; /* 確保影片不變形地填滿 */
    z-index: 0;
}

/* 深色遮罩層 */
.video-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5); /* 50% 黑透明，可根據影片明亮度調整 */
    z-index: 1;
}
        /* 聯絡區塊 */
        #Create {
            text-align: center;
            background: #000 ;
            background-size: cover;
            width:100%;
            padding: 100px 10%;
    min-height: 100vh;
        }

        #contact h2 {
            font-size: 3rem;
        }
        #contact p{
           
        }
        #contact a {
            color: var(--text-main);
            text-decoration: none;
            position: relative;
            padding-bottom: 5px;
            font-size: 1.2rem;
            transition: color 0.3s ease;
        }

        #contact a::after { /* 聯絡按鈕底部劃線動畫 */
            content: '';
            position: absolute;
            left: 0;
            bottom: 0;
            width: 0;
            height: 2px;
            background-color: var(--text-main);
            transition: width 0.3s ease-out;
        }

        #contact a:hover {
            color: var(--text-sub);
        }
        #contact a:hover::after {
            width: 100%;
        }

        /* 頁尾 */
        footer {
            padding: 20px 10%;
            border-top: 1px solid var(--accent-gray);
            text-align: center;
            color: var(--text-sub);
            font-size: 0.9rem;
        }
        footer p{
                margin-bottom: 0;
        }

        /* 響應式 */
        @media (max-width: 768px) {
            nav { padding: 1.5rem 5%; }
            .logo { font-size: 1.2rem; }
            .nav-links { display: none; } /* 手機版通常用漢堡選單，這裡先隱藏 */
            .hero h1 { font-size: 3rem; }
            .hero p { font-size: 1rem; }
            section { padding: 80px 5%; }
            .project-card { height: 300px; }
            .project-info h3 { font-size: 1.5rem; }
            #contact h2 { font-size: 2rem; }
        }
    </style>
</head>
<body>
    <!-- 選單欄 -->
    <nav>
        <div class="logo" onclick="scrollToSection('home')">Abai</div>
        <div class="nav-links">
            <!-- <a href="#home">自我介紹</a> -->
            <a href="#work">專案分享</a>
            <a href="#about">關於我</a>
            <a href="#contact">聯絡方式</a>
        </div>
    </nav>

    <section id="home" class="hero">
        <div id="particles-js"></div> <h1 data-aos="fade-up"><span id="typed"></span></h1>
        <p data-aos="fade-up" data-aos-delay="200">專注於數位體驗與極簡視覺設計</p>
    </section>
<!-- 作品展示 -->
    <section id="work">
        <h2 data-aos="fade-right" style="  font-size: 2.5rem; margin-bottom: 2rem; letter-spacing: .3rem;  "><span style="font-size: 24px; font-weight: 500;">專案分享</span><br>Selected Work</h2>
        <div class="portfolio-grid">
            
             <a href="https://www.behance.net/gallery/153436011/MSI-Venture-Series" class="project-card" data-aos="fade-up">
           
                       <img src="item1.jpg" class="img-responsive">        
                <div class="project-info" style="font-weight: 500;"><h3>MSI Venture Series</h3><p>微星電腦外型設計</p></div>
            </a>
            
            <a href="https://www.behance.net/gallery/145813157/CRUTCH" class="project-card" data-aos="fade-up" data-aos-delay="100">
                 <img src="item2.jpg" class="img-responsive"> 
                <div class="project-info" style="font-weight: 500;"><h3>CRUTCH</h3><p>行動輔具設計</p></div>
            </a>
            <a href="https://www.behance.net/gallery/141207715/ARCFOLD" class="project-card" data-aos="fade-up" data-aos-delay="200">
                 <img src="item3.jpg" class="img-responsive"> 
                <div class="project-info" style="font-weight: 500;"><h3>Arcfold</h3><p>折疊型腳踏車設計</p></div>
            </a>
            <a href="https://www.behance.net/gallery/145832487/PORTFOLIO-2026" class="project-card" data-aos="fade-up" data-aos-delay="200">
                 <img src="item4.jpg" class="img-responsive"> 
                <div class="project-info" style="font-weight: 500;"><h3>Portfolio</h3><p>個人作品集</p></div>
            </a>
            </div>
    </section>
<section id="about" class="video-section" style="   position: relative; overflow: hidden; min-height: 100vh; display: flex; align-items: center;">
    
    <video autoplay muted loop playsinline poster="item6.png" class="bg-video" style="opacity: 0.5;">
        <source src="BK2.mp4" type="video/mp4" style="width:100%; object-fit: cover; ">
    </video>
    
        <div class="container">
        <div class="row">
        <div class="col-md-6">
        <h2 data-aos="fade-right" style="  font-size: 2.5rem; margin-bottom: 2rem; letter-spacing: .3rem;  "><span style="font-size: 24px; font-weight: 500;">關於我</span><br>About me</h2>
        <div class="d-flex align-items-center"> <div class="about-content " data-aos="fade-up">
        <p style="margin-top: 1rem; letter-spacing:0.1rem; line-height: 1.1;">
            工業設計不只是造型的堆疊，更是對材料與細節的極致追求。我專注於將複雜的機能隱藏於簡潔的幾何之中，透過精確的建模與材質定義，讓每一件產品不僅是解決問題的工具，更是生活空間中的視覺藝術。
        </p>
        <div class="skill-list">
            <div class="skill-tag" data-aos="zoom-in" data-aos-delay="100">Rhinoceros 3D</div>
            <div class="skill-tag" data-aos="zoom-in" data-aos-delay="200">Luxion Keyshot</div>
            <div class="skill-tag" data-aos="zoom-in" data-aos-delay="300">Adobe Illustrator</div>
            <div class="skill-tag" data-aos="zoom-in" data-aos-delay="400">Adobe Photoshop</div>
            <div class="skill-tag" data-aos="zoom-in" data-aos-delay="500">Adobe Premiere</div>
            <div class="skill-tag" data-aos="zoom-in" data-aos-delay="600">Adobe After Effects</div>
        </div>
        </div>
    </div>
    </div>
    <div class="col-md-6">
   
       
        <img src="BK6.gif" style=" width: 100%; height: 100%; object-fit: cover; z-index: -1; opacity: 1;">
    
        
    
    </div>
    </div>
        </div>
        </div>
    </section>
</section>

<section id="Create" class="video-section" style="position: relative; overflow: hidden; min-height: 100vh; display: flex; align-items: center; padding: 0 10%;">
    
    <video autoplay muted loop playsinline poster="item6.png" class="bg-video" style="opacity: 0.5;">
        <source src="BK3.mp4" type="video/mp4" style="width:100%; object-fit: cover; ">
    </video>
    <section id="contact">
        <h2 data-aos="zoom-in">Let's Create Together</h2>
        <p style="margin: 30px 0; font-size: 1.1rem;  color:#fff;" data-aos="fade-up">無論是新專案合作、技術交流，還是單純的問候，我都期待與你交流！</p>
        <a href="mailto:abaiabai0689@gmail.com" data-aos="zoom-in" data-aos-delay="200">Say Hello</a>
    </section>
</section>
    <footer>
        <p>&copy; 2026 Abai Portfolio. All Rights Reserved.</p>
    </footer>

    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script src="https://unpkg.com/typed.js@2.0.16/dist/typed.umd.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>
</script>
    <script>
        // 初始化 AOS 滾動動畫
        AOS.init({
            duration: 1000,
            once: true,
            easing: 'ease-out-quart',
            offset: 100 // 提前100px觸發動畫
        });

        // 初始化 打字效果
        var typed = new Typed('#typed', {
            strings: ['I am Abai, a Product Designer.', 'Defined by aesthetics.', 'Elegance meets function.'], // 將 YOUR NAME 放在首位
            typeSpeed: 60,
            backSpeed: 40,
            loop: true,
            showCursor: true, // 顯示打字游標
            cursorChar: '|',
            autoInsertCss: true,
        });

        // 初始化 particles.js
        particlesJS('particles-js', {
            "particles": {
                "number": {
                    "value": 80,
                    "density": {
                        "enable": true,
                        "value_area": 800
                    }
                },
                "color": {
                    "value": "#ffffff" /* 粒子顏色 */
                },
                "shape": {
                    "type": "circle",
                    "stroke": {
                        "width": 0,
                        "color": "#000000"
                    },
                    "polygon": {
                        "nb_sides": 5
                    }
                },
                "opacity": {
                    "value": 0.5,
                    "random": false,
                    "anim": {
                        "enable": false,
                        "speed": 1,
                        "opacity_min": 0.1,
                        "sync": false
                    }
                },
                "size": {
                    "value": 3,
                    "random": true,
                    "anim": {
                        "enable": false,
                        "speed": 40,
                        "size_min": 0.1,
                        "sync": false
                    }
                },
                "line_linked": {
                    "enable": true,
                    "distance": 150,
                    "color": "#ffffff", /* 連線顏色 */
                    "opacity": 0.4,
                    "width": 1
                },
                "move": {
                    "enable": true,
                    "speed": 3, /* 粒子移動速度 */
                    "direction": "none",
                    "random": false,
                    "straight": false,
                    "out_mode": "out",
                    "bounce": false,
                    "attract": {
                        "enable": false,
                        "rotateX": 600,
                        "rotateY": 1200
                    }
                }
            },
            "interactivity": {
                "detect_on": "canvas",
                "events": {
                    "onhover": {
                        "enable": true,
                        "mode": "grab" /* 滑鼠懸停時粒子互動模式: grab 抓取連線 */
                    },
                    "onclick": {
                        "enable": true,
                        "mode": "push" /* 滑鼠點擊時粒子互動模式: push 產生粒子 */
                    },
                    "resize": true
                },
                "modes": {
                    "grab": {
                        "distance": 140,
                        "line_linked": {
                            "opacity": 1
                        }
                    },
                    "bubble": {
                        "distance": 400,
                        "size": 40,
                        "duration": 2,
                        "opacity": 8,
                        "speed": 3
                    },
                    "repulse": {
                        "distance": 200,
                        "duration": 0.4
                    },
                    "push": {
                        "particles_nb": 4
                    },
                    "remove": {
                        "particles_nb": 2
                    }
                }
            },
            "retina_detect": true
        });

        // 導覽列平滑滾動與 Logo 點擊回首頁
        document.querySelectorAll('nav .nav-links a').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });

        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({
                behavior: 'smooth'
            });
        }
    </script>
</body>
</html>
