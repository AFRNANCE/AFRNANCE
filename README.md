<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AFRNANCE - Crypto to UGX Exchange</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            overflow-x: hidden;
        }
        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        .navbar {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 2rem;
        }
        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: white;
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
        }
        .nav-links {
            display: flex;
            gap: 2rem;
        }
        .nav-link {
            color: white;
            text-decoration: none;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .nav-link:hover {
            color: #ffd700;
            transform: translateY(-2px);
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 100px 2rem 2rem;
        }
        .hero {
            text-align: center;
            margin-bottom: 4rem;
            color: white;
        }
        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            text-shadow: 0 4px 8px rgba(0,0,0,0.3);
            animation: fadeInUp 1s ease;
        }
        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
            animation: fadeInUp 1s ease 0.2s both;
        }
        .cta-button {
            background: linear-gradient(45deg, #ffd700, #ffed4a);
            color: #333;
            border: none;
            padding: 1rem 2rem;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 215, 0, 0.4);
            animation: fadeInUp 1s ease 0.4s both;
        }
        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(255, 215, 0, 0.6);
        }
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 4rem;
        }
        .exchange-panel, .wallet-panel {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 2rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }
        .exchange-panel:hover, .wallet-panel:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.2);
        }
        .panel-title {
            color: white;
            font-size: 1.5rem;
            margin-bottom: 1.5rem;
            text-align: center;
        }
        .form-group {
            margin-bottom: 1.5rem;
        }
        .form-group label {
            display: block;
            color: white;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        .form-control {
            width: 100%;
            padding: 1rem;
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        .form-control:focus {
            outline: none;
            border-color: #ffd700;
            box-shadow: 0 0 20px rgba(255, 215, 0, 0.3);
        }
        .form-control::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }
        select.form-control {
            cursor: pointer;
        }
        .action-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 1rem;
            margin-top: 2rem;
        }
        .btn {
            padding: 1rem;
            border: none;
            border-radius: 15px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }
        .btn-success {
            background: linear-gradient(45deg, #56ab2f, #a8e6cf);
            color: white;
        }
        .btn-warning {
            background: linear-gradient(45deg, #f093fb, #f5576c);
            color: white;
        }
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.2);
        }
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
            margin-bottom: 4rem;
        }
        .stat-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 2rem;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
        }
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.2);
        }
        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            color: #ffd700;
            margin-bottom: 0.5rem;
        }
        .stat-label {
            color: white;
            font-size: 0.9rem;
            opacity: 0.8;
        }
        .impact-section {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 3rem;
            margin-bottom: 4rem;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .impact-title {
            color: white;
            font-size: 2rem;
            margin-bottom: 2rem;
        }
        .impact-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }
        .impact-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 2rem;
            transition: all 0.3s ease;
        }
        .impact-card:hover {
            transform: scale(1.05);
            background: rgba(255, 255, 255, 0.1);
        }
        .impact-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
        }
        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            backdrop-filter: blur(5px);
        }
        .modal-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 5% auto;
            padding: 2rem;
            border-radius: 20px;
            width: 90%;
            max-width: 500px;
            position: relative;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .close {
            color: white;
            float: right;
            font-size: 2rem;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s ease;
        }
        .close:hover {
            color: #ffd700;
        }
        .wallet-balance {
            background: linear-gradient(45deg, #1e3c72, #2a5298);
            border-radius: 15px;
            padding: 1.5rem;
            margin-bottom: 2rem;
            text-align: center;
        }
        .balance-amount {
            font-size: 2rem;
            color: #ffd700;
            font-weight: bold;
            margin-bottom: 0.5rem;
        }
        .balance-label {
            color: white;
            opacity: 0.8;
        }
        .supported-networks {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 1rem;
            margin: 2rem 0;
        }
        .network-chip {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 25px;
            padding: 0.5rem 1rem;
            text-align: center;
            color: white;
            font-size: 0.9rem;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
        }
        .network-chip:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: scale(1.05);
        }
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        .floating {
            animation: float 6s ease-in-out infinite;
        }
        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .action-buttons {
                grid-template-columns: 1fr;
            }
            
            .nav-links {
                display: none;
            }
        }
        .pulse {
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0% {
                box-shadow: 0 0 0 0 rgba(255, 215, 0, 0.7);
            }
            70% {
                box-shadow: 0 0 0 10px rgba(255, 215, 0, 0);
            }
            100% {
                box-shadow: 0 0 0 0 rgba(255, 215, 0, 0);
            }
        }
        .notification {
            position: fixed;
            top: 100px;
            right: 20px;
            background: linear-gradient(45deg, #56ab2f, #a8e6cf);
            color: white;
            padding: 1rem 2rem;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.2);
            transform: translateX(400px);
            transition: transform 0.3s ease;
            z-index: 3000;
        }
        .notification.show {
            transform: translateX(0);
        }
    </style>
</head>
<body>
    <canvas class="animated-bg"></canvas>
    
    <nav class="navbar">
        <div class="nav-container">
            <div class="logo">🌱 AFRNANCE</div>
            <div class="nav-links">
                <a href="#" class="nav-link" onclick="showKYC()">KYC Verification</a>
                <a href="#exchange" class="nav-link">Exchange</a>
                <a href="#impact" class="nav-link">Environmental Impact</a>
                <a href="#wallet" class="nav-link">Wallet</a>
            </div>
        </div>
    </nav>
    <div class="container">
        <section class="hero">
            <h1 class="floating">AFRNANCE Exchange</h1>
            <p>Seamlessly exchange cryptocurrency to Ugandan Shillings while funding environmental restoration and supporting rural communities.</p>
            <button class="cta-button pulse" onclick="showKYC()">Complete KYC & Start Trading</button>
        </section>
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-value" id="totalVolume">UGX 2.5B+</div>
                <div class="stat-label">Total Volume Traded</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="treesPlanted">15,000+</div>
                <div class="stat-label">Trees Planted</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="studentsHelped">500+</div>
                <div class="stat-label">Students Supported</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="plasticCollected">2.5T</div>
                <div class="stat-label">Plastic Collected</div>
            </div>
        </div>
        <div class="main-content" id="exchange">
            <div class="exchange-panel">
                <h2 class="panel-title">💱 Exchange</h2>
                
                <div class="form-group">
                    <label>From:</label>
                    <select class="form-control" id="fromCurrency">
                        <option value="ETH">ETH - Ethereum</option>
                        <option value="USDT">USDT - Tether</option>
                        <option value="USDC">USDC - USD Coin</option>
                        <option value="DAI">DAI - Dai Stablecoin</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Network:</label>
                    <select class="form-control" id="network">
                        <option value="ethereum">Ethereum</option>
                        <option value="polygon">Polygon</option>
                        <option value="celo">Celo</option>
                        <option value="base">Base</option>
                        <option value="arbitrum">Arbitrum</option>
                        <option value="optimism">Optimism</option>
                        <option value="solana">Solana</option>
                        <option value="metis">Metis</option>
                        <option value="divvi">Divvi</option>
                        <option value="hedera">Hedera</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Amount:</label>
                    <input type="number" class="form-control" id="amount" placeholder="Enter amount" step="0.0001">
                </div>
                <div class="form-group">
                    <label>To:</label>
                    <select class="form-control" id="toCurrency">
                        <option value="UGX">UGX - Ugandan Shillings</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Estimated Amount:</label>
                    <input type="text" class="form-control" id="estimatedAmount" readonly placeholder="UGX 0.00">
                </div>
                <div class="form-group">
                    <label>Mobile Money Number:</label>
                    <input type="tel" class="form-control" id="mobileNumber" placeholder="+256XXXXXXXXX">
                </div>
                <button class="btn btn-primary" onclick="initiateExchange()" style="width: 100%; margin-top: 1rem;">
                    🚀 Exchange Now
                </button>
            </div>
            <div class="wallet-panel" id="wallet">
                <h2 class="panel-title">💼 Your Wallet</h2>
                
                <div class="wallet-balance">
                    <div class="balance-amount" id="walletBalance">UGX 0.00</div>
                    <div class="balance-label">Available Balance</div>
                </div>
                <div class="form-group">
                    <label>Wallet Address:</label>
                    <input type="text" class="form-control" id="walletAddress" placeholder="Connect your wallet" readonly>
                </div>
                <div class="action-buttons">
                    <button class="btn btn-success" onclick="receiveModal()">
                        📥 Receive
                    </button>
                    <button class="btn btn-primary" onclick="sendModal()">
                        📤 Send
                    </button>
                    <button class="btn btn-warning" onclick="withdrawModal()">
                        💰 Withdraw
                    </button>
                </div>
                <div class="supported-networks">
                    <div class="network-chip">Ethereum</div>
                    <div class="network-chip">Polygon</div>
                    <div class="network-chip">Celo</div>
                    <div class="network-chip">Base</div>
                    <div class="network-chip">Arbitrum</div>
                    <div class="network-chip">Optimism</div>
                    <div class="network-chip">Solana</div>
                    <div class="network-chip">Metis</div>
                    <div class="network-chip">Divvi</div>
                    <div class="network-chip">Hedera</div>
                </div>
            </div>
        </div>
        <section class="impact-section" id="impact">
            <h2 class="impact-title">🌍 Environmental & Social Impact</h2>
            <p style="color: white; font-size: 1.1rem; margin-bottom: 2rem;">
                Every transaction on AFRNANCE contributes to environmental restoration and community development across Uganda.
            </p>
            
            <div class="impact-grid">
                <div class="impact-card">
                    <div class="impact-icon">🌳</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Tree Planting</h3>
                    <p style="color: rgba(255,255,255,0.8);">Reforestation programs across Uganda's degraded landscapes</p>
                </div>
                
                <div class="impact-card">
                    <div class="impact-icon">📚</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Education Support</h3>
                    <p style="color: rgba(255,255,255,0.8);">School supplies for vulnerable children in rural communities</p>
                </div>
                
                <div class="impact-card">
                    <div class="impact-icon">♻️</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Plastic Collection</h3>
                    <p style="color: rgba(255,255,255,0.8);">Community-driven plastic waste collection programs</p>
                </div>
                
                <div class="impact-card">
                    <div class="impact-icon">🌾</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Wetland Restoration</h3>
                    <p style="color: rgba(255,255,255,0.8);">Protecting and restoring critical wetland ecosystems</p>
                </div>
                
                <div class="impact-card">
                    <div class="impact-icon">🚜</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Regenerative Agriculture</h3>
                    <p style="color: rgba(255,255,255,0.8);">Supporting sustainable farming practices</p>
                </div>
                
                <div class="impact-card">
                    <div class="impact-icon">☀️</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Solar Power</h3>
                    <p style="color: rgba(255,255,255,0.8);">Bringing clean energy to rural households</p>
                </div>
                
                <div class="impact-card">
                    <div class="impact-icon">💰</div>
                    <h3 style="color: white; margin-bottom: 1rem;">Basic Income</h3>
                    <p style="color: rgba(255,255,255,0.8);">1% goes to GoodDollar UBI for farmers & women's groups</p>
                </div>
            </div>
        </section>
    </div>
    <!-- KYC Modal -->
    <div id="kycModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 style="color: white; margin-bottom: 2rem;">🆔 KYC Verification</h2>
            
            <div class="form-group">
                <label>Full Name:</label>
                <input type="text" class="form-control" id="fullName" placeholder="Enter your full name">
            </div>
            
            <div class="form-group">
                <label>National ID Number:</label>
                <input type="text" class="form-control" id="nationalId" placeholder="Enter National ID">
            </div>
            
            <div class="form-group">
                <label>Phone Number:</label>
                <input type="tel" class="form-control" id="phoneKyc" placeholder="+256XXXXXXXXX">
            </div>
            
            <div class="form-group">
                <label>Upload National ID (Front):</label>
                <input type="file" class="form-control" id="idFront" accept="image/*">
            </div>
            
            <div class="form-group">
                <label>Upload National ID (Back):</label>
                <input type="file" class="form-control" id="idBack" accept="image/*">
            </div>
            
            <button class="btn btn-success" onclick="submitKYC()" style="width: 100%; margin-top: 1rem;">
                ✅ Submit for Verification
            </button>
        </div>
    </div>
    <!-- Send Modal -->
    <div id="sendModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 style="color: white; margin-bottom: 2rem;">📤 Send Crypto</h2>
            
            <div class="form-group">
                <label>Recipient Address:</label>
                <input type="text" class="form-control" id="sendAddress" placeholder="Enter wallet address">
            </div>
            
            <div class="form-group">
                <label>Amount:</label>
                <input type="number" class="form-control" id="sendAmount" placeholder="Amount to send" step="0.0001">
            </div>
            
            <div class="form-group">
                <label>Currency:</label>
                <select class="form-control" id="sendCurrency">
                    <option value="ETH">ETH</option>
                    <option value="USDT">USDT</option>
                    <option value="USDC">USDC</option>
                    <option value="DAI">DAI</option>
                </select>
            </div>
            
            <button class="btn btn-primary" onclick="executeSend()" style="width: 100%; margin-top: 1rem;">
                🚀 Send Transaction
            </button>
        </div>
    </div>
    <!-- Receive Modal -->
    <div id="receiveModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 style="color: white; margin-bottom: 2rem;">📥 Receive Crypto</h2>
            
            <div style="text-align: center; margin: 2rem 0;">
                <div style="background: white; padding: 2rem; border-radius: 15px; display: inline-block;">
                    <div id="qrCode" style="width: 200px; height: 200px; background: #f0f0f0; display: flex; align-items: center; justify-content: center; border-radius: 10px;">
                        📱 QR Code
                    </div>
                </div>
            </div>
            
            <div class="form-group">
                <label>Your Wallet Address:</label>
                <input type="text" class="form-control" id="receiveAddress" value="0x742d35Cc6635C0532925a3b8D65C0b5b6f318D7" readonly>
            </div>
            
            <button class="btn btn-success" onclick="copyAddress()" style="width: 100%; margin-top: 1rem;">
                📋 Copy Address
            </button>
        </div>
    </div>
    <!-- Withdraw Modal -->
    <div id="withdrawModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 style="color: white; margin-bottom: 2rem;">💰 Withdraw Funds</h2>
            
            <div class="form-group">
                <label>Withdrawal Method:</label>
                <select class="form-control" id="withdrawMethod">
                    <option value="mobile">Mobile Money</option>
                    <option value="wallet">Crypto Wallet</option>
                </select>
            </div>
            
            <div class="form-group">
                <label>Amount (UGX):</label>
                <input type="number" class="form-control" id="withdrawAmount" placeholder="Amount to withdraw">
            </div>
            
            <div class="form-group" id="mobileWithdrawGroup">
                <label>Mobile Money Number:</label>
                <input type="tel" class="form-control" id="withdrawMobile" placeholder="+256XXXXXXXXX">
            </div>
            
            <div class="form-group" id="walletWithdrawGroup" style="display: none;">
                <label>Wallet Address:</label>
                <input type="text" class="form-control" id="withdrawWallet" placeholder="Destination wallet address">
            </div>
            
            <button class="btn btn-warning" onclick="executeWithdraw()" style="width: 100%; margin-top: 1rem;">
                💸 Process Withdrawal
            </button>
        </div>
    </div>
    <div id="notification" class="notification">
        <div id="notificationText">Transaction successful!</div>
    </div>
    <script>
        // Global state
        let exchangeRates = {
            ETH: 3800000,
            USDT: 3800,
            USDC: 3800,
            DAI: 3800
        };
        let userBalance = 0;
        let kycCompleted = false;
        // Three.js background animation
        function initBackground() {
            const canvas = document.querySelector('.animated-bg');
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            const renderer = new THREE.WebGLRenderer({ canvas, alpha: true });
            
            renderer.setSize(window.innerWidth, window.innerHeight);
            
            // Create floating particles
            const geometry = new THREE.SphereGeometry(0.5, 8, 8);
            const material = new THREE.MeshBasicMaterial({ color: 0xffffff, transparent: true, opacity: 0.6 });
            
            const particles = [];
            for (let i = 0; i < 50; i++) {
                const particle = new THREE.Mesh(geometry, material);
                particle.position.set(
                    (Math.random() - 0.5) * 100,
                    (Math.random() - 0.5) * 100,
                    (Math.random() - 0.5) * 100
                );
                particles.push(particle);
                scene.add(particle);
            }
            
            camera.position.z = 50;
            
            function animate() {
                requestAnimationFrame(animate);
                
                particles.forEach(particle => {
                    particle.rotation.x += 0.01;
                    particle.rotation.y += 0.01;
                    particle.
