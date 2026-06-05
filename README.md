<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>LEGACY DATA HUB</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://js.paystack.co/v1/inline.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --yellow: #FFD700;
      --black: #000000;
      --dark-bg: #0a0a0a;
      --card-bg: rgba(20, 20, 20, 0.85);
      --glow-yellow: rgba(255, 215, 0, 0.2);
      --whatsapp-green: #25D366;
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Inter', sans-serif;
      background-color: var(--dark-bg);
      color: white;
      overflow-x: hidden;
    }
    #scene-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      pointer-events: none;
    }
    header {
      background: rgba(0, 0, 0, 0.85);
      backdrop-filter: blur(10px);
      padding: 1.2rem 2rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid var(--yellow);
      position: relative;
      z-index: 10;
    }
    .logo {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.6rem;
      font-weight: 700;
      color: var(--yellow);
      display: flex;
      align-items: center;
      gap: 0.6rem;
      text-shadow: 0 0 10px var(--glow-yellow);
    }
    .contact-info {
      font-size: 0.95rem;
      display: flex;
      gap: 1.5rem;
    }
    .container {
      max-width: 1200px;
      margin: 2.5rem auto;
      padding: 0 1.5rem;
      position: relative;
      z-index: 5;
    }
    .hero {
      text-align: center;
      margin-bottom: 2.5rem;
    }
    .hero h1 {
      font-family: 'Orbitron', sans-serif;
      font-size: 2.6rem;
      margin-bottom: 0.5rem;
      background: linear-gradient(to right, var(--yellow), #fff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 0 15px var(--glow-yellow);
    }
    .network-selector {
      display: flex;
      gap: 1rem;
      margin: 2rem 0;
      justify-content: center;
      flex-wrap: wrap;
    }
    .network-btn {
      background: transparent;
      color: white;
      border: 2px solid var(--yellow);
      padding: 0.7rem 1.4rem;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      border-radius: 6px;
      transition: all 0.3s ease;
    }
    .network-btn.active {
      background: var(--yellow);
      color: var(--black);
      box-shadow: 0 0 15px var(--glow-yellow);
    }
    .packages-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
      gap: 1.2rem;
      margin-bottom: 2.5rem;
    }
    .package-card {
      background: var(--card-bg);
      border: 1px solid rgba(255, 215, 0, 0.2);
      border-radius: 12px;
      padding: 1.4rem 1rem;
      text-align: center;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .package-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 6px 15px rgba(255, 215, 0, 0.3);
      border-color: var(--yellow);
    }
    .package-size {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.4rem;
      font-weight: 600;
      margin-bottom: 0.5rem;
      color: var(--yellow);
    }
    .package-price {
      font-size: 1.2rem;
      font-weight: 700;
      color: white;
    }
    .order-form {
      background: var(--card-bg);
      padding: 2rem;
      border-radius: 16px;
      margin-bottom: 2.5rem;
      border: 1px solid rgba(255, 215, 0, 0.2);
    }
    .form-group {
      margin-bottom: 1.2rem;
    }
    label {
      display: block;
      margin-bottom: 0.6rem;
      font-weight: 600;
      font-size: 1.05rem;
    }
    input {
      width: 100%;
      padding: 0.85rem;
      border-radius: 8px;
      border: 1px solid rgba(255, 215, 0, 0.4);
      background: rgba(10, 10, 10, 0.9);
      color: white;
      font-size: 1rem;
    }
    input:focus {
      outline: none;
      border-color: var(--yellow);
    }
    .btn {
      background: linear-gradient(to right, var(--yellow), #e6c200);
      color: var(--black);
      border: none;
      padding: 1rem;
      font-size: 1.1rem;
      font-weight: 700;
      border-radius: 8px;
      cursor: pointer;
      width: 100%;
      transition: transform 0.2s, box-shadow 0.2s;
      font-family: 'Orbitron', sans-serif;
      letter-spacing: 1px;
      text-transform: uppercase;
      box-shadow: 0 4px 15px rgba(255, 215, 0, 0.3);
    }
    .btn:hover {
      transform: scale(1.01);
      box-shadow: 0 6px 20px rgba(255, 215, 0, 0.5);
    }
    .track-btn {
      background: linear-gradient(to right, var(--whatsapp-green), #128C7E);
      margin-top: 1rem;
      color: white;
      box-shadow: 0 4px 15px rgba(37, 211, 102, 0.2);
    }
    .track-btn:hover {
      box-shadow: 0 6px 20px rgba(37, 211, 102, 0.4);
    }
    .divider {
      height: 1px;
      background: rgba(255, 215, 0, 0.2);
      margin: 2.5rem 0 1.5rem;
    }
    .summary {
      background: var(--card-bg);
      padding: 1.8rem;
      border-radius: 16px;
      border: 1px solid rgba(255, 215, 0, 0.15);
    }
    .summary h3 {
      font-family: 'Orbitron', sans-serif;
      margin-bottom: 1.2rem;
      color: var(--yellow);
      text-align: center;
    }
    .summary-item {
      display: flex;
      justify-content: space-between;
      margin-bottom: 0.8rem;
      font-size: 1.05rem;
    }
    .notice {
      background: rgba(15, 15, 15, 0.9);
      padding: 1.4rem;
      border-radius: 12px;
      margin-top: 2rem;
      font-size: 0.95rem;
      border-left: 3px solid var(--yellow);
    }
    footer {
      text-align: center;
      padding: 3rem 2rem 2rem;
      background: rgba(5, 5, 5, 0.95);
      margin-top: 4rem;
      position: relative;
      z-index: 5;
      border-top: 1px solid rgba(255, 215, 0, 0.1);
    }
    .footer-links-container {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      align-items: center;
      margin-bottom: 1.5rem;
    }
    .whatsapp-link {
      color: var(--whatsapp-green);
      text-decoration: none;
      font-weight: 600;
      font-size: 1.1rem;
      display: inline-flex;
      align-items: center;
      gap: 0.6rem;
      padding: 0.4rem 0.8rem;
      border-radius: 6px;
      background: rgba(37, 211, 102, 0.05);
      border: 1px solid rgba(37, 211, 102, 0.2);
      transition: all 0.3s ease;
    }
    .whatsapp-link:hover {
      background: rgba(37, 211, 102, 0.15);
      border-color: var(--whatsapp-green);
      box-shadow: 0 0 12px rgba(37, 211, 102, 0.3);
      transform: translateY(-2px);
    }
    .whatsapp-icon {
      width: 24px;
      height: 24px;
      fill: var(--whatsapp-green);
    }
    @media (max-width: 768px) {
      .hero h1 { font-size: 2rem; }
      .network-selector { flex-direction: column; align-items: center; }
      .packages-grid { grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); }
      .contact-info { flex-direction: column; gap: 0.4rem; align-items: flex-end; }
    }
  </style>
</head>
<body>
  <div id="scene-container"></div>

  <header>
    <div class="logo-container" style="display: flex; align-items: center; gap: 12px;">
  <svg width="45" height="45" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg" style="filter: drop-shadow(0px 0px 8px rgba(255, 215, 0, 0.4));">
    <defs>
      <linearGradient id="logo-grad" x1="0%" y1="100%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="#FFD700" />
        <stop offset="100%" stop-color="#00E5FF" />
      </linearGradient>
      <linearGradient id="border-grad" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#FFD700" stop-opacity="0.8"/>
        <stop offset="100%" stop-color="#101010" stop-opacity="0.2"/>
      </linearGradient>
    </defs>
    
    <polygon points="50,5 90,25 90,75 50,95 10,75 10,25" fill="#0A0A0A" stroke="url(#border-grad)" stroke-width="3"/>
    
    <rect x="28" y="68" width="44" height="8" rx="4" fill="url(#logo-grad)" />
    
    <rect x="28" y="24" width="8" height="38" rx="4" fill="url(#logo-grad)" />
    <rect x="40" y="36" width="8" height="26" rx="4" fill="url(#logo-grad)" opacity="0.85" />
    <rect x="52" y="46" width="8" height="16" rx="4" fill="url(#logo-grad)" opacity="0.7" />
    <rect x="64" y="54" width="8" height="8" rx="4" fill="url(#logo-grad)" opacity="0.5" />
    
    <path d="M 32 14 A 22 22 0 0 1 68 14" stroke="#00E5FF" stroke-width="3" stroke-linecap="round" opacity="0.9" />
  </svg>

  <div style="display: flex; flex-direction: column;">
    <span style="font-family: 'Orbitron', sans-serif; font-size: 1.4rem; font-weight: 700; color: #FFD700; letter-spacing: 1px; line-height: 1.1;">LEGACY</span>
    <span style="font-family: 'Inter', sans-serif; font-size: 0.75rem; font-weight: 600; color: #00E5FF; letter-spacing: 3.5px; text-transform: uppercase;">Data Hub</span>
  </div>
</div>
    <div class="contact-info">
      <span>📞 0599821047</span>
      <span>✉️ legacydatahub@gmail.com</span>
    </div>
  </header>

  <div class="container">
    <div class="hero">
      <h1>Your NO.1 data shop</h1>
      <p>Secure • Fast • Reliable</p>
    </div>

    <div class="network-selector">
      <button class="network-btn active" data-network="MTN">MTN</button>
      <button class="network-btn" data-network="TELECEL">TELECEL</button>
      <button class="network-btn" data-network="AIRTELTIGO">AIRTELTIGO</button>
    </div>

    <div class="packages-grid" id="packagesContainer"></div>

    <div class="order-form">
      <h3 style="text-align:center; margin-bottom:1.5rem; color:var(--yellow); font-family:'Orbitron', sans-serif;">Complete Your Order</h3>
      <div class="form-group">
        <label for="phoneNumber">Phone Number (Enter valid network number)</label>
        <input type="tel" id="phoneNumber" placeholder="e.g. 0241234567" max-length="10" required>
      </div>
      <div class="form-group">
        <label for="selectedPackage">Selected Package</label>
        <input type="text" id="selectedPackage" readonly placeholder="Select a card from above">
      </div>
      <div class="form-group">
        <label for="totalAmount">Total Amount (GHC)</label>
        <input type="text" id="totalAmount" readonly placeholder="₵0.00">
      </div>
      <button class="btn" id="payButton">Pay Now with Paystack</button>

      <div class="divider"></div>

      <h3 style="text-align:center; margin-bottom:1.2rem; color:var(--yellow); font-family:'Orbitron', sans-serif;">Order Tracking</h3>
      <div class="form-group">
        <label for="trackPhoneNumber">Enter Phone Number to Track Order</label>
        <input type="tel" id="trackPhoneNumber" placeholder="e.g. 0241234567">
      </div>
      <button class="btn track-btn" id="trackButton">Track My Order</button>
    </div>

    <div class="summary">
      <h3>Order Summary</h3>
      <div class="summary-item"><span>Network:</span><span id="summaryNetwork">MTN</span></div>
      <div class="summary-item"><span>Package:</span><span id="summaryPackage">-</span></div>
      <div class="summary-item"><span>Amount:</span><span id="summaryAmount">-</span></div>
      <div class="summary-item"><span>Phone:</span><span id="summaryPhone">-</span></div>
    </div>

    <div class="notice">
      <strong>Delivery Time:</strong> 4 to 30 minutes<br>
      <strong>Important:</strong> Enter a valid network number. Data sent to a wrong number cannot be refunded.
    </div>
  </div>

  <footer>
    <div class="footer-links-container">
      <a href="https://wa.me/message/DF4CE2EQV33QP1" target="_blank" class="whatsapp-link">
        <svg class="whatsapp-icon" viewBox="0 0 24 24"><path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946C.06 5.348 5.397.01 12.008.01c3.202.001 6.212 1.246 8.477 3.514 2.266 2.268 3.507 5.28 3.505 8.484-.004 6.657-5.34 11.997-11.953 11.997-2.005-.001-3.973-.502-5.713-1.455L0 24zm6.59-3.847c1.62.963 3.424 1.47 5.267 1.471h.005c5.445 0 9.876-4.43 9.88-9.878.002-2.64-1.019-5.123-2.877-6.983-1.857-1.86-4.339-2.883-6.98-2.884-5.448 0-9.88 4.43-9.884 9.88-.001 1.83.479 3.619 1.392 5.216l-.961 3.513 3.6-.945zm11.233-7.561c-.3-.149-1.772-.875-2.046-.975-.274-.1-.474-.149-.674.15-.2.299-.773.975-.947 1.174-.174.199-.349.224-.648.075-.3-.15-1.265-.466-2.41-1.485-.89-.794-1.49-1.775-1.665-2.074-.174-.299-.019-.461.13-.609.135-.133.3-.299.449-.449.149-.15.199-.249.299-.498.1-.2.05-.374-.025-.524-.075-.15-.674-1.62-.923-2.219-.242-.582-.487-.504-.674-.513-.174-.009-.374-.009-.573-.009-.2 0-.523.075-.797.374-.274.299-1.047 1.022-1.047 2.494 0 1.471 1.071 2.892 1.221 3.092.149.199 2.107 3.216 5.106 4.512.714.309 1.271.494 1.708.633.717.228 1.37.195 1.887.118.575-.085 1.772-.723 2.021-1.396.249-.673.249-1.246.174-1.396-.075-.149-.274-.249-.574-.398z"/></svg>
        Chat on WhatsApp
      </a>
      
      <a href="https://whatsapp.com/channel/0029VaCiikI23n3Wt1d5z402" target="_blank" class="whatsapp-link">
        <svg class="whatsapp-icon" viewBox="0 0 24 24"><path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946C.06 5.348 5.397.01 12.008.01c3.202.001 6.212 1.246 8.477 3.514 2.266 2.268 3.507 5.28 3.505 8.484-.004 6.657-5.34 11.997-11.953 11.997-2.005-.001-3.973-.502-5.713-1.455L0 24zm6.59-3.847c1.62.963 3.424 1.47 5.267 1.471h.005c5.445 0 9.876-4.43 9.88-9.878.002-2.64-1.019-5.123-2.877-6.983-1.857-1.86-4.339-2.883-6.98-2.884-5.448 0-9.88 4.43-9.884 9.88-.001 1.83.479 3.619 1.392 5.216l-.961 3.513 3.6-.945zm11.233-7.561c-.3-.149-1.772-.875-2.046-.975-.274-.1-.474-.149-.674.15-.2.299-.773.975-.947 1.174-.174.199-.349.224-.648.075-.3-.15-1.265-.466-2.41-1.485-.89-.794-1.49-1.775-1.665-2.074-.174-.299-.019-.461.13-.609.135-.133.3-.299.449-.449.149-.15.199-.249.299-.498.1-.2.05-.374-.025-.524-.075-.15-.674-1.62-.923-2.219-.242-.582-.487-.504-.674-.513-.174-.009-.374-.009-.573-.009-.2 0-.523.075-.797.374-.274.299-1.047 1.022-1.047 2.494 0 1.471 1.071 2.892 1.221 3.092.149.199 2.107 3.216 5.106 4.512.714.309 1.271.494 1.708.633.717.228 1.37.195 1.887.118.575-.085 1.772-.723 2.021-1.396.249-.673.249-1.246.174-1.396-.075-.149-.274-.249-.574-.398z"/></svg>
        Subscribe to Updates
      </a>
    </div>
    <p style="opacity: 0.5; font-size: 0.85rem;">&copy; 2026 LEGACY DATA HUB. All rights reserved.</p>
  </footer>

  <script>
    // Optimized Lightweight 3D Background Engine
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 500);
    
    const renderer = new THREE.WebGLRenderer({ antialias: false, alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)); 
    document.getElementById('scene-container').appendChild(renderer.domElement);

    const particlesGeometry = new THREE.BufferGeometry();
    const particlesCount = 600; 
    const posArray = new Float32Array(particlesCount * 3);
    for(let i = 0; i < particlesCount * 3; i++) {
      posArray[i] = (Math.random() - 0.5) * 120;
    }
    particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));

    const particlesMaterial = new THREE.PointsMaterial({
      size: 0.9,
      color: 0xFFD700,
      transparent: true,
      opacity: 0.5
    });

    const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
    scene.add(particlesMesh);

    const torusGeometry = new THREE.TorusGeometry(7, 1.5, 12, 40);
    const torusMaterial = new THREE.MeshBasicMaterial({ 
      color: 0xFFD700,
      wireframe: true,
      transparent: true,
      opacity: 0.35
    });
    const torus = new THREE.Mesh(torusGeometry, torusMaterial);
    torus.position.y = 2;
    scene.add(torus);

    camera.position.z = 25;

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    const animate = () => {
      requestAnimationFrame(animate);
      particlesMesh.rotation.x += 0.0003;
      particlesMesh.rotation.y += 0.0003;
      torus.rotation.x += 0.003;
      torus.rotation.y += 0.006;
      renderer.render(scene, camera);
    };
    animate();

    // Data Engine Configurations
    const PAYSTACK_PUBLIC_KEY = 'pk_live_8b9d5c666a57f0c2c1a5cb908083e50972b1e2aa';
    
    const packages = {
      MTN: [
        { size: '1GB', price: 4.80 }, { size: '2GB', price: 9.80 }, { size: '3GB', price: 14.30 },
        { size: '4GB', price: 22 }, { size: '5GB', price: 26 }, { size: '6GB', price: 29 },
        { size: '8GB', price: 37 }, { size: '10GB', price: 46 }, { size: '15GB', price: 64 },
        { size: '20GB', price: 84 }, { size: '25GB', price: 104 }, { size: '30GB', price: 126 },
        { size: '40GB', price: 163 }, { size: '50GB', price: 205 }
      ],
      TELECEL: [
        { size: '10GB', price: 41 }, { size: '15GB', price: 57.85 }, { size: '20GB', price: 76.80 },
        { size: '25GB', price: 93.75 }, { size: '40GB', price: 146.60 }, { size: '50GB', price: 181.50 }
      ],
      AIRTELTIGO: [
        { size: '1GB', price: 4.75 }, { size: '2GB', price: 9.25 }, { size: '3GB', price: 14.25 },
        { size: '4GB', price: 17.50 }, { size: '5GB', price: 20.50 }, { size: '6GB', price: 24.50 },
        { size: '8GB', price: 32 }, { size: '10GB', price: 40 }, { size: '12GB', price: 47 },
        { size: '15GB', price: 60.50 }
      ]
    };

    let currentNetwork = 'MTN';
    let selectedPackage = null;

    const forceNumeric = (e) => { e.target.value = e.target.value.replace(/[^0-9]/g, ''); };
    document.getElementById('phoneNumber').addEventListener('input', (e) => {
      forceNumeric(e);
      document.getElementById('summaryPhone').textContent = e.target.value || '-';
    });
    document.getElementById('trackPhoneNumber').addEventListener('input', forceNumeric);

    function renderPackages(network) {
      const container = document.getElementById('packagesContainer');
      container.innerHTML = '';
      
      packages[network].forEach(pkg => {
        const card = document.createElement('div');
        card.className = 'package-card';
        card.innerHTML = `
          <div class="package-size">${pkg.size}</div>
          <div class="package-price">₵${pkg.price.toFixed(2)}</div>
        `;
        card.addEventListener('click', () => {
          selectedPackage = pkg;
          document.getElementById('selectedPackage').value = `${pkg.size} (${network})`;
          document.getElementById('totalAmount').value = `₵${pkg.price.toFixed(2)}`;
          document.getElementById('summaryPackage').textContent = `${pkg.size} (${network})`;
          document.getElementById('summaryAmount').textContent = `₵${pkg.price.toFixed(2)}`;
          
          document.querySelectorAll('.package-card').forEach(c => c.style.border = '1px solid rgba(255, 215, 0, 0.2)');
          card.style.border = '2px solid var(--yellow)';
        });
        container.appendChild(card);
      });
    }

    document.querySelectorAll('.network-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.network-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        currentNetwork = btn.dataset.network;
        document.getElementById('summaryNetwork').textContent = currentNetwork;
        renderPackages(currentNetwork);
        selectedPackage = null;
        document.getElementById('selectedPackage').value = '';
        document.getElementById('totalAmount').value = '';
        document.getElementById('summaryPackage').textContent = '-';
        document.getElementById('summaryAmount').textContent = '-';
      });
    });

    document.getElementById('payButton').addEventListener('click', () => {
      const phone = document.getElementById('phoneNumber').value;
      if (!selectedPackage) {
        alert('Please choose a data bundle package card above first.');
        return;
      }
      if (!phone || phone.length < 10) {
        alert('Please enter a complete 10-digit valid phone number.');
        return;
      }
      
      const handler = PaystackPop.setup({
        key: PAYSTACK_PUBLIC_KEY,
        email: 'legacydatahub@gmail.com',
        amount: Math.round(selectedPackage.price * 100),
        currency: 'GHS',
        ref: 'LDH-' + Date.now() + '-' + Math.floor((Math.random() * 100000) + 1),
        metadata: {
          custom_fields: [
            { display_name: "Network", variable_name: "network", value: currentNetwork },
            { display_name: "Package Size", variable_name: "package_size", value: selectedPackage.size },
            { display_name: "Recipient Phone", variable_name: "recipient_phone", value: phone }
          ]
        },
        callback: function(response) {
          alert('Payment successful! Reference: ' + response.reference + '\nYour bundle will arrive within 4-30 minutes.');
        },
        onClose: function() {
          alert('Transaction window closed.');
        }
      });
      handler.openIframe();
    });

    document.getElementById('trackButton').addEventListener('click', () => {
      const trackPhone = document.getElementById('trackPhoneNumber').value;
      if (!trackPhone || trackPhone.length < 10) {
        alert('Please enter a complete 10-digit telephone order identity.');
        return;
      }
      const message = encodeURIComponent(`order tracking ${trackPhone}`);
      window.open(`https://wa.me/233599821047?text=${message}`, '_blank');
    });

    renderPackages(currentNetwork);
  </script>
</body>
</html>
