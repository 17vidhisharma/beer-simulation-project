<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Craft Beer Business Simulation</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@300;400;600;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
            color: white;
            overflow-x: hidden;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        .hero {
            position: relative;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            overflow: hidden;
        }
        
        .beer-bubbles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        
        .bubble {
            position: absolute;
            background: rgba(255, 193, 7, 0.3);
            border-radius: 50%;
            animation: float 6s infinite ease-in-out;
        }
        
        .bubble:nth-child(1) { width: 40px; height: 40px; left: 10%; animation-delay: 0s; }
        .bubble:nth-child(2) { width: 20px; height: 20px; left: 20%; animation-delay: 1s; }
        .bubble:nth-child(3) { width: 60px; height: 60px; left: 35%; animation-delay: 2s; }
        .bubble:nth-child(4) { width: 30px; height: 30px; left: 50%; animation-delay: 3s; }
        .bubble:nth-child(5) { width: 50px; height: 50px; left: 70%; animation-delay: 1.5s; }
        .bubble:nth-child(6) { width: 25px; height: 25px; left: 80%; animation-delay: 4s; }
        .bubble:nth-child(7) { width: 35px; height: 35px; left: 90%; animation-delay: 0.5s; }
        
        @keyframes float {
            0%, 100% {
                transform: translateY(100vh) scale(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) scale(1);
                opacity: 0;
            }
        }
        
        .hero-content {
            position: relative;
            z-index: 2;
            animation: slideInUp 1s ease-out;
        }
        
        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .beer-icon {
            font-size: 4rem;
            margin-bottom: 1rem;
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {
                transform: translateY(0);
            }
            40% {
                transform: translateY(-10px);
            }
            60% {
                transform: translateY(-5px);
            }
        }
        
        h1 {
            font-family: 'Bebas Neue', cursive;
            font-size: 4rem;
            margin-bottom: 1rem;
            background: linear-gradient(45deg, #ffc107, #ff9800, #ff5722);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: glow 2s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from {
                filter: drop-shadow(0 0 20px #ffc107);
            }
            to {
                filter: drop-shadow(0 0 30px #ff9800);
            }
        }
        
        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        
        .course-info {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 2rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .highlight {
            color: #ffc107;
            font-weight: 600;
        }
        
        .stats-section {
            padding: 100px 0;
            background: rgba(0, 0, 0, 0.2);
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin-top: 50px;
        }
        
        .stat-card {
            background: linear-gradient(135deg, rgba(255, 193, 7, 0.1) 0%, rgba(255, 152, 0, 0.1) 100%);
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            border: 1px solid rgba(255, 193, 7, 0.3);
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }
        
        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }
        
        .stat-card:hover::before {
            left: 100%;
        }
        
        .stat-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(255, 193, 7, 0.3);
        }
        
        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            color: #ffc107;
            margin-bottom: 10px;
            font-family: 'Bebas Neue', cursive;
        }
        
        .stat-label {
            font-size: 1.1rem;
            opacity: 0.8;
        }
        
        .highlights-section {
            padding: 100px 0;
        }
        
        .section-title {
            font-family: 'Bebas Neue', cursive;
            font-size: 3rem;
            text-align: center;
            margin-bottom: 50px;
            color: #ffc107;
        }
        
        .highlights-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }
        
        .highlight-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 30px;
            border-left: 5px solid #ffc107;
            transition: all 0.3s ease;
        }
        
        .highlight-card:hover {
            transform: translateX(10px);
            background: rgba(255, 193, 7, 0.1);
        }
        
        .highlight-title {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 15px;
            color: #ffc107;
        }
        
        .charts-section {
            padding: 100px 0;
            background: rgba(0, 0, 0, 0.2);
        }
        
        .charts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin-top: 50px;
        }
        
        .chart-placeholder {
            background: linear-gradient(135deg, rgba(255, 193, 7, 0.1) 0%, rgba(255, 152, 0, 0.1) 100%);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            border: 2px dashed rgba(255, 193, 7, 0.5);
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }
        
        .chart-placeholder:hover {
            border-color: #ffc107;
            transform: scale(1.02);
        }
        
        .chart-icon {
            font-size: 3rem;
            color: #ffc107;
            margin-bottom: 15px;
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.5;
            }
        }
        
        .scroll-indicator {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            animation: bounce 2s infinite;
        }
        
        .scroll-arrow {
            width: 30px;
            height: 30px;
            border: 2px solid #ffc107;
            border-top: none;
            border-left: none;
            transform: rotate(45deg);
        }
        
        .animate-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.6s ease;
        }
        
        .animate-in.visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .highlights-grid {
                grid-template-columns: 1fr;
            }
            
            .charts-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .floating-elements {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }
        
        .floating-beer {
            position: absolute;
            font-size: 2rem;
            color: rgba(255, 193, 7, 0.3);
            animation: floatAround 20s infinite linear;
        }
        
        @keyframes floatAround {
            0% {
                transform: translateX(-100px) rotate(0deg);
            }
            100% {
                transform: translateX(calc(100vw + 100px)) rotate(360deg);
            }
        }
    </style>
</head>
<body>
    <div class="floating-elements">
        <div class="floating-beer" style="top: 20%; animation-delay: 0s;">🍺</div>
        <div class="floating-beer" style="top: 60%; animation-delay: 5s;">🍻</div>
        <div class="floating-beer" style="top: 80%; animation-delay: 10s;">🍺</div>
    </div>
    
    <section class="hero">
        <div class="beer-bubbles">
            <div class="bubble"></div>
            <div class="bubble"></div>
            <div class="bubble"></div>
            <div class="bubble"></div>
            <div class="bubble"></div>
            <div class="bubble"></div>
            <div class="bubble"></div>
        </div>
        
        <div class="container">
            <div class="hero-content">
                <div class="beer-icon">🍺</div>
                <h1>Craft Beer Business Simulation</h1>
                <p class="subtitle">A data-driven business simulation project that transforms Austin's craft beer scene</p>
                
                <div class="course-info">
                    <p>Completed for <span class="highlight">AD715: Quantitative & Qualitative Decision-Making</span> at <span class="highlight">Boston University</span> (Spring 2025)</p>
                    <p>Our team designed a <span class="highlight">craft beer bar and microbrewery in Austin, Texas</span>, running multiple simulation cycles to optimize operations, finance, HR, and innovation strategies.</p>
                </div>
                
                <p style="font-size: 1.3rem; margin-top: 20px;">
                    The result? A microbrewery concept that <span class="highlight">breaks even in just 9 months</span> and pours <span class="highlight">$4.3M median profit</span> over 36 months.
                </p>
            </div>
        </div>
        
        <div class="scroll-indicator">
            <div class="scroll-arrow"></div>
        </div>
    </section>
    
    <section class="stats-section">
        <div class="container">
            <h2 class="section-title animate-in">Key Performance Metrics</h2>
            <div class="stats-grid">
                <div class="stat-card animate-in">
                    <div class="stat-number">$4.32M</div>
                    <div class="stat-label">Median Net Profit</div>
                </div>
                <div class="stat-card animate-in">
                    <div class="stat-number">9.08</div>
                    <div class="stat-label">Months to Break-even</div>
                </div>
                <div class="stat-card animate-in">
                    <div class="stat-number">$5.6M</div>
                    <div class="stat-label">Contribution Margin</div>
                </div>
                <div class="stat-card animate-in">
                    <div class="stat-number">36</div>
                    <div class="stat-label">Months Simulated</div>
                </div>
            </div>
        </div>
    </section>
    
    <section class="highlights-section">
        <div class="container">
            <h2 class="section-title animate-in">📊 Project Highlights</h2>
            <div class="highlights-grid">
                <div class="highlight-card animate-in">
                    <div class="highlight-title">🎯 Strategic Simulation</div>
                    <p>Simulated comprehensive business decisions for production, innovation, HR, and financial strategy using advanced modeling techniques.</p>
                </div>
                <div class="highlight-card animate-in">
                    <div class="highlight-title">📈 Analytical Framework</div>
                    <p>Conducted thorough PESTLE, SWOT, and break-even analyses to understand market dynamics and competitive positioning.</p>
                </div>
                <div class="highlight-card animate-in">
                    <div class="highlight-title">🔮 Predictive Modeling</div>
                    <p>Used what-if analysis, forecasting, and optimization techniques to drive data-informed decision-making processes.</p>
                </div>
                <div class="highlight-card animate-in">
                    <div class="highlight-title">🏆 Outstanding Results</div>
                    <p>Best-performing simulation cycle achieved exceptional financial performance with rapid break-even and strong profitability.</p>
                </div>
                <div class="highlight-card animate-in">
                    <div class="highlight-title">🍺 Austin Market Focus</div>
                    <p>Specifically designed for Austin's thriving craft beer scene, leveraging local market insights and consumer preferences.</p>
                </div>
                <div class="highlight-card animate-in">
                    <div class="highlight-title">⚡ Rapid Growth Model</div>
                    <p>Developed a scalable business model that demonstrates sustainable growth and market penetration strategies.</p>
                </div>
            </div>
        </div>
    </section>
    
    <section class="charts-section">
        <div class="container">
            <h2 class="section-title animate-in">🖼️ Simulation Visualizations</h2>
            <div class="charts-grid">
                <div class="chart-placeholder animate-in">
                    <div class="chart-icon">📊</div>
                    <h3>Revenue Projections</h3>
                    <p>Interactive charts showing revenue growth over 36 months with seasonal variations and market trends.</p>
                </div>
                <div class="chart-placeholder animate-in">
                    <div class="chart-icon">💰</div>
                    <h3>Profit Analysis</h3>
                    <p>Detailed profit margins and break-even analysis demonstrating path to profitability.</p>
                </div>
                <div class="chart-placeholder animate-in">
                    <div class="chart-icon">📈</div>
                    <h3>Market Penetration</h3>
                    <p>Market share growth and customer acquisition metrics over the simulation period.</p>
                </div>
                <div class="chart-placeholder animate-in">
                    <div class="chart-icon">🎯</div>
                    <h3>Strategic Metrics</h3>
                    <p>Key performance indicators tracking operational efficiency and strategic goal achievement.</p>
                </div>
                <div class="chart-placeholder animate-in">
                    <div class="chart-icon">🔄</div>
                    <h3>Scenario Analysis</h3>
                    <p>Comparative analysis of different strategic scenarios and their financial implications.</p>
                </div>
                <div class="chart-placeholder animate-in">
                    <div class="chart-icon">📉</div>
                    <h3>Risk Assessment</h3>
                    <p>Risk analysis and sensitivity testing for various market conditions and operational parameters.</p>
                </div>
            </div>
        </div>
    </section>
    
    <script>
        // Intersection Observer for animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -100px 0px'
        };
        
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, observerOptions);
        
        // Observe all elements with animate-in class
        document.querySelectorAll('.animate-in').forEach(el => {
            observer.observe(el);
        });
        
        // Add click interactions to stat cards
        document.querySelectorAll('.stat-card').forEach(card => {
            card.addEventListener('click', () => {
                card.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    card.style.transform = 'translateY(-10px)';
                }, 100);
            });
        });
        
        // Add hover effects to chart placeholders
        document.querySelectorAll('.chart-placeholder').forEach(chart => {
            chart.addEventListener('mouseenter', () => {
                const icon = chart.querySelector('.chart-icon');
                icon.style.transform = 'scale(1.2) rotate(5deg)';
            });
            
            chart.addEventListener('mouseleave', () => {
                const icon = chart.querySelector('.chart-icon');
                icon.style.transform = 'scale(1) rotate(0deg)';
            });
        });
        
        // Smooth scrolling for scroll indicator
        document.querySelector('.scroll-indicator').addEventListener('click', () => {
            document.querySelector('.stats-section').scrollIntoView({
                behavior: 'smooth'
            });
        });
        
        // Dynamic bubble generation
        function createBubble() {
            const bubble = document.createElement('div');
            bubble.className = 'bubble';
            bubble.style.left = Math.random() * 100 + '%';
            bubble.style.width = bubble.style.height = (20 + Math.random() * 40) + 'px';
            bubble.style.animationDuration = (4 + Math.random() * 4) + 's';
            bubble.style.animationDelay = Math.random() * 2 + 's';
            
            document.querySelector('.beer-bubbles').appendChild(bubble);
            
            setTimeout(() => {
                bubble.remove();
            }, 8000);
        }
        
        // Generate bubbles periodically
        setInterval(createBubble, 1000);
    </script>
</body>
</html>
