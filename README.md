<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DailyPay - Live Claim App</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
  <style>
    /* --- General Styles --- */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body,
    html {
      font-family: 'Segoe UI', Arial, sans-serif;
      width: 100%;
      height: 100%;
      overflow-x: hidden;
      /* Prevent horizontal scroll */
      background-color: white;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .screen {
      display: none;
      /* All screens initially hidden */
      width: 100%;
      max-width: 400px; /* Set a max-width for a more app-like feel on desktop */
      min-height: 100vh;
      /* Use min-height for content flexibility */
      justify-content: flex-start; /* Align content to the top */
      align-items: center;
      flex-direction: column;
      /* Ensure content stacks vertically */
      padding-bottom: 20px;
      /* Add some padding at the bottom */
      border: 1px solid #ccc; /* Optional: adds a border to visualize the app frame */
      box-shadow: 0 4px 8px rgba(0,0,0,0.1); /* Optional: adds a subtle shadow */
    }

    /* --- Welcome Screen Styles --- */
    .welcome-screen {
      display: flex;
      /* Initially show welcome screen */
      background-color: #A8D5A2;
      justify-content: center;
    }

    .container-welcome {
      /* Renamed to avoid conflict with withdraw container */
      background-color: #A8D5A2;
      width: 100%;
      height: 100%;
      border-radius: 40px 40px 0 0;
      position: relative;
      overflow: hidden;
      padding: 40px 20px 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .top-logo {
        text-align: center;
    }

    .top-logo h1 {
      color: #00844D;
      font-weight: bold;
      font-size: 28px;
    }

    .cash-logo {
      font-size: 28px;
      margin-right: 5px;
    }

    .cash-text {
      font-weight: 700;
    }

    .dailypay {
      font-size: 48px;
      font-weight: bold;
      margin-top: 10px;
    }

    .daily {
      color: #151d38;
    }

    .check {
      color: #5f9969;
    }

    .pay {
      color: #5f9969;
      margin-left: 5px;
    }

    .description {
      margin-top: 30px;
      font-size: 16px;
      color: #222;
      line-height: 1.6;
      text-align: center;
    }

    .money-animation {
        position: relative;
        width: 100px;
        height: 60px;
        margin: 40px 0 50px;
    }

    .money-animation .bill {
      width: 30px;
      height: 15px;
      background-color: #00844D;
      border-radius: 3px;
      position: absolute;
      opacity: 0.7;
    }

    .bill:nth-child(1) { top: 0; left: 10%; transform: rotate(15deg); }
    .bill:nth-child(2) { top: 15%; left: 60%; transform: rotate(-10deg); }
    .bill:nth-child(3) { top: 30%; left: 35%; transform: rotate(25deg); }
    .bill:nth-child(4) { top: 45%; left: 80%; transform: rotate(-20deg); }

    .buttons {
      display: flex;
      justify-content: space-around;
      width: 100%;
      gap: 20px;
    }

    button {
      padding: 15px 0;
      width: 45%;
      border-radius: 25px;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
      border: 2px solid #006b2c;
      transition: 0.3s;
    }

    .register {
      background-color: #006b2c;
      color: #fff;
    }

    .login {
      background-color: transparent;
      color: #006b2c;
    }

    /* --- Form Screen Styles (Register/Login) --- */
    .form-screen {
      background-color: white;
      padding: 40px 20px;
      justify-content: center;
    }

    .form-box {
      max-width: 400px;
      width: 100%;
    }

    .form-box h2 {
      text-align: center;
      margin-bottom: 20px;
      color: green;
    }

    .form-box label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
    }

    .form-box input {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #aaa;
      border-radius: 8px;
    }

    .form-box .submit-button {
      /* General style for form submit buttons */
      margin-top: 20px;
      width: 100%;
      padding: 15px;
      background-color: green;
      color: white;
      border: none;
      border-radius: 25px;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
    }

    .form-box .submit-button:hover {
      background-color: darkgreen;
    }

    /* --- Dashboard Styles (Claim App) --- */
    .dashboard-screen {
      background-color: #f3f3f3;
      padding: 0;
      /* Remove initial padding, sections have their own */
    }

    .dashboard-screen header {
      background-color: #00423e;
      color: white;
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      /* Align items vertically in the center */
      width: 100%;
      /* Full width header */
    }

    .header-left {
      display: flex;
      align-items: center;
      gap: 10px;
      /* Space between profile image and username */
    }


    .balance-section {
      background-color: #00423e;
      color: white;
      margin: 20px;
      border-radius: 20px;
      padding: 20px;
      text-align: center;
      width: calc(100% - 40px);
      /* Adjust width for margin */
      max-width: 400px;
      /* Limit width */
    }

    .badges {
      display: flex;
      gap: 6px;
      justify-content: center;
      margin-bottom: 10px;
    }

    .badge {
      background-color: orange;
      color: white;
      border-radius: 10px;
      padding: 2px 8px;
      font-size: 10px;
    }

    .badge-top {
      background-color: #4e6cef;
    }

    .withdraw-dashboard-btn {
      background-color: orange;
      color: white;
      border: none;
      padding: 10px 30px;
      border-radius: 25px;
      font-size: 16px;
      margin-top: 10px;
      cursor: pointer;
    }

    .claim-section {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      /* Responsive grid */
      gap: 20px;
      padding: 20px;
      justify-items: center;
      width: 100%;
      max-width: 800px;
      /* Limit overall width */
    }

    .claim-card {
      background-color: white;
      border-radius: 15px;
      padding: 15px;
      width: 140px;
      /* Fixed width for cards */
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
      text-align: center;
    }

    .claim-card p {
      margin: 5px 0;
      font-weight: bold;
    }

    .claim-card button {
      background-color: #00423e;
      color: white;
      border: none;
      border-radius: 20px;
      padding: 10px;
      width: 100%;
      margin-top: 10px;
      cursor: pointer;
    }

    .claim-card button:disabled {
      background-color: grey;
      cursor: not-allowed;
    }

    #notification {
      background-color: yellow;
      padding: 10px;
      display: none;
      margin: 10px auto;
      width: 80%;
      border-radius: 10px;
      text-align: center;
      max-width: 400px;
      /* Limit width */
    }

    #profileImage {
      border-radius: 50%;
      width: 30px;
      height: 30px;
      object-fit: cover;
    }

    #notificationCount {
      position: absolute;
      top: -5px;
      right: -5px;
      background-color: red;
      color: white;
      font-size: 10px;
      border-radius: 50%;
      padding: 2px 6px;
      display: none;
    }

    /* --- Withdrawal Page Styles --- */
    .withdraw-screen {
        justify-content: flex-start;
    }

    .withdraw-container {
      /* For the form part */
      width: 100%;
      max-width: 400px;
      background-color: #ffffff;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      border-radius: 8px;
      overflow: hidden;
      margin-top: 20px;
    }

    .withdraw-screen .header {
      /* Specific to header within withdraw flow */
      background-color: #4CAF50;
      color: white;
      padding: 15px 20px;
      font-size: 20px;
      text-align: center;
      display: flex;
      /* Make it a flex container */
      justify-content: space-between;
      /* Space out items */
      align-items: center;
      /* Vertically align items */
    }

    .withdraw-screen .header .back-arrow,
    .withdraw-screen .header .cancel-icon {
      /* Apply styles to both back and cancel icons */
      cursor: pointer;
      /* Adjust size and color for the back arrow */
    }

    .withdraw-screen .header .back-arrow img,
    .withdraw-screen .header .cancel-icon img {
      /* Apply styles to images within both icons */
      width: 24px;
      /* Adjust size as needed */
      height: 24px;
      filter: invert(1);
      /* Makes the black icon white */
    }

    .withdraw-screen .header .header-title {
      flex-grow: 1;
      /* Allows title to take available space */
      text-align: center;
      /* Center the title within its space */
      margin-left: -24px;
      /* Offset the space taken by the back arrow on the left for true centering */
    }


    .withdraw-screen .form-section {
      /* Specific to form section within withdraw flow */
      padding: 20px;
    }

    .withdraw-screen .form-group {
      margin-bottom: 15px;
    }

    .withdraw-screen .form-group input,
    .withdraw-screen .form-group select {
      width: 100%;
      padding: 12px 10px;
      border: 1px solid #ddd;
      border-radius: 8px;
      font-size: 16px;
      box-sizing: border-box;
      background-color: #fff;
    }

    .withdraw-screen .withdrawal-button {
      width: 100%;
      padding: 15px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 18px;
      cursor: pointer;
    }

    .withdraw-screen .buy-coupon-code {
      text-align: center;
      font-weight: 500;
      /* Choose your desired color here: blue or red */
      color: blue;
      /* Changed to blue */
      /* color: red; */
      /* Uncomment this line and comment the above for red */
      cursor: pointer;
      margin-top: 15px;
      /* Add some space above the link */
    }

    .withdraw-screen .message-screen,
    .withdraw-screen .success-screen {
      /* For success/error messages within withdraw flow */
      background: white;
      padding: 20px;
      text-align: center;
      max-width: 400px;
      width: 100%;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      margin-top: 20px;
      /* Give some space if shown standalone after form */
      /* display: none; /* Initially hidden, controlled by JS */
    }

    /* Ensure only one part of withdraw screen is shown at a time by JS */
    #mainForm {
      display: block;
    }

    /* Default visible part of withdraw screen */
    #successScreenWithdraw {
      display: none;
    }

    #errorScreenWithdraw {
      display: none;
    }


    .withdraw-screen .summary-title {
      font-size: 22px;
      font-weight: bold;
      margin-bottom: 15px;
    }

    .withdraw-screen .summary-icon {
      margin: 10px 0;
    }

    .withdraw-screen .summary-name {
      font-size: 16px;
      margin-top: 10px;
    }

    .withdraw-screen .summary-amount {
      font-size: 26px;
      font-weight: bold;
      margin-bottom: 20px;
    }

    .withdraw-screen .summary-row {
      display: flex;
      justify-content: space-between;
      font-size: 16px;
      padding: 8px 0;
      border-bottom: 1px solid #eee;
    }

    .withdraw-screen .summary-label {
      font-weight: 500;
    }

    .withdraw-screen .done-btn {
      background: green;
      color: white;
      padding: 15px;
      border-radius: 50px;
      border: none;
      font-size: 18px;
      width: 100%;
      margin-top: 20px;
      cursor: pointer;
    }

    .withdraw-screen .error-message {
      font-size: 18px;
      color: red;
      margin: 20px 0;
    }

    .withdraw-screen .green-btn {
      background-color: #4CAF50;
      color: white;
      padding: 12px;
      margin-top: 10px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      width: 100%;
      cursor: pointer;
    }

    .withdraw-screen .support-btn {
      background-color: #007BFF;
      color: white;
      padding: 12px;
      margin-top: 10px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      width: 100%;
      cursor: pointer;
    }

    .withdraw-screen .care-btn {
      background-color: #ff5722;
      color: white;
      padding: 12px;
      margin-top: 10px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      width: 100%;
      cursor: pointer;
    }
  </style>
</head>

<body>

  <div class="screen welcome-screen" id="welcomeScreen">
    <div class="container-welcome">
      <div class="top-logo">
        <h1><span class="cash-logo">💳</span><span class="cash-text">CASH</span></h1>
        <h2 class="dailypay"><span class="daily">dai<span class="check">✓</span>ly</span><span class="pay">pay</span></h2>
      </div>

      <div class="description">
        <p>Transfer to other Bank.</p>
      </div>

      <div class="money-animation">
        <div class="bill"></div>
        <div class="bill"></div>
        <div class="bill"></div>
        <div class="bill"></div>
      </div>

      <div class="buttons">
        <button class="register" onclick="showScreen('registerScreen')">Register</button>
        <button class="login" onclick="showScreen('loginScreen')">Login</button>
      </div>
    </div>
  </div>

  <div class="screen form-screen" id="registerScreen">
    <form class="form-box" id="registerForm">
      <h2>Register</h2>
      <label for="regUsername">Username</label>
      <input type="text" id="regUsername" required placeholder="Enter username" />

      <label for="regEmail">Email</label>
      <input type="email" id="regEmail" required placeholder="Enter email" />

      <label for="regPassword">Password</label>
      <input type="password" id="regPassword" required placeholder="Enter password" />

      <button type="submit" class="submit-button">Register</button>
      <div id="registerMessage" style="display: none; text-align: center; margin-top: 15px; color: green;">
        Registering...
      </div>
    </form>
  </div>

  <div class="screen form-screen" id="loginScreen">
    <form class="form-box" id="loginForm">
      <h2>Login</h2>
      <label for="email">Email</label>
      <input type="email" id="email" required placeholder="Enter email" />

      <label for="password">Password</label>
      <input type="password" id="password" required placeholder="Enter password" />

      <button type="submit" class="submit-button">Login</button>
      <div id="loadingMessage" style="display: none; text-align: center; margin-top: 15px; color: green;">
        Logging in, please wait...
      </div>
    </form>
  </div>

  <div class="screen dashboard-screen" id="dashboardScreen">
    <header>
      <div class="header-left">
        <div style="position: relative;">
          <label for="profileUpload">
            <img id="profileImage" src="https://img.icons8.com/ios-glyphs/30/ffffff/user--v1.png" style="cursor: pointer;" />
          </label>
          <input type="file" id="profileUpload" accept="image/*" style="display: none;" />
        </div>
        <span id="usernameDisplay" style="color: white; font-weight: bold;"></span>
      </div>

      <div style="position: relative;">
        <img src="https://img.icons8.com/ios-filled/30/000000/appointment-reminders--v1.png" style="filter: invert(1);" />
        <span id="notificationCount">0</span>
      </div>
    </header>

    <audio id="successSound" src="https://assets.mixkit.co/sfx/preview/mixkit-achievement-bell-600.mp3" preload="auto"></audio>
    <audio id="errorSound" src="https://assets.mixkit.co/sfx/preview/mixkit-wrong-answer-fail-notification-946.mp3" preload="auto"></audio>
    <audio id="errorSound_general" src="https://assets.mixkit.co/sfx/preview/mixkit-wrong-answer-fail-notification-946.mp3" preload="auto"></audio>


    <div id="notification">Claimed successfully</div>

    <section class="balance-section">
      <div class="badges">
        <div class="badge badge-top">Top-Rated</div>
        <div class="badge">New</div>
      </div>
      <h2><span id="balance">₦0.00</span></h2>
      <p>Live Balance</p>
      <button class="withdraw-dashboard-btn" onclick="showScreen('withdrawScreen')">Withdrawal</button>
    </section>

    <section class="claim-section" id="claimSection"></section>
  </div>

  <div class="screen withdraw-screen" id="withdrawScreen">
    <div style="width: 100%; max-width: 400px; display: flex; flex-direction: column; align-items: center;">
      <div class="withdraw-container" id="mainForm">
        <div class="header">
          <div class="back-arrow" onclick="showScreen('dashboardScreen')">
            <img src="https://img.icons8.com/ios-glyphs/30/ffffff/back--v1.png" alt="Back" />
          </div>
          <div class="header-title">Transfer To Bank</div>
          <div></div>
        </div>
        <div class="form-section">
          <div class="form-group">
            <input type="text" id="accountNumber" placeholder="Account Number">
          </div>
          <div class="form-group">
            <select id="selectedBank">
              <option value="">Select bank</option>
              <option>Access Bank</option>
              <option>Carbon Bank</option>
              <option>FairMoney Bank</option>
              <option>GTBank</option>
              <option>Kuda Bank</option>
              <option>Moniepoint Bank</option>
              <option>OPay Bank</option>
              <option>PalmPay Bank</option>
              <option>Rubies Bank</option>
              <option>UBA Bank</option>
              <option>Vbank Bank</option>
              <option>Wema Bank</option>
              <option>Zenith Bank</option>
            </select>
          </div>
          <div class="form-group">
            <input type="text" id="accountName" placeholder="Account Name">
          </div>
          <div class="form-group">
            <input type="text" id="amount" placeholder="Amount">
          </div>
          <div class="form-group">
            <input type="text" id="couponCode" placeholder="Coupon Code">
          </div>
          <button class="withdrawal-button" id="initiateWithdrawal">Withdraw</button>
          <div class="buy-coupon-code" onclick="alert('Contact support to buy a coupon code.')">Buy coupon code</div>
        </div>
      </div>

      <div class="success-screen" id="successScreenWithdraw">
        <div class="summary-title">Transaction Summary</div>
        <div class="summary-icon"><img src="https://img.icons8.com/emoji/96/000000/check-mark-emoji.png" width="80" /></div>
        <div class="summary-name" id="summaryName"></div>
        <div class="summary-amount" id="summaryAmount"></div>

        <div class="summary-row">
          <div class="summary-label">Reference No</div>
          <div id="summaryRef"></div>
        </div>
        <div class="summary-row">
          <div class="summary-label">Wallet Number</div>
          <div id="summaryWalletNumber"></div>
        </div>
        <div class="summary-row">
          <div class="summary-label">Wallet Name</div>
          <div id="summaryBank"></div>
        </div>
        <div class="summary-row">
          <div class="summary-label">Fees</div>
          <div>₦0.00</div>
        </div>
        <button class="done-btn" onclick="returnToWithdrawForm()">Done</button>
      </div>

      <div class="message-screen" id="errorScreenWithdraw">
        <div class="header" style="background-color: #f44336;">
          <div class="cancel-icon" onclick="backToWithdrawFormFromError()"> <img src="https://img.icons8.com/ios-glyphs/30/ffffff/multiply.png" alt="Cancel" />
          </div>
          <div class="header-title">Error</div>
          <div></div>
        </div>
        <div class="error-message">Incorrect coupon code</div>
        <button class="green-btn" onclick="alert('Redirecting to coupon purchase...')">Buy Coupon</button>
        <button class="support-btn" id="joinGroupBtn">Join WhatsApp Group</button>
        <button class="care-btn" id="contactCustomerCareBtn">Contact Customer Care</button>
      </div>
    </div>
  </div>


  <script>
    // --- Screen Management ---
    function showScreen(screenId) {
      document.querySelectorAll('.screen').forEach(screen => {
        screen.style.display = 'none';
      });

      const targetScreen = document.getElementById(screenId);
      if (targetScreen) {
        targetScreen.style.display = "flex"; // Show the target screen
      }


      if (screenId === "dashboardScreen") {
        updateUsernameDisplay();
        updateBalanceDisplay();
        renderClaimCards();
        updateNotificationDisplay();
        startClaimTimer();
      } else {
        clearInterval(claimIntervalId); // Stop dashboard timer if not on dashboard
      }

      // If showing withdrawScreen, ensure its main form is visible by default
      // and its internal success/error messages are hidden.
      if (screenId === "withdrawScreen") {
        document.getElementById("mainForm").style.display = "block"; // or "flex" if your .withdraw-container uses flex
        document.getElementById("successScreenWithdraw").style.display = "none";
        document.getElementById("errorScreenWithdraw").style.display = "none";
      }
    }

    // New function to return to and reset the withdrawal form
    function returnToWithdrawForm() {
      // Hide success and error screens within the withdrawScreen
      document.getElementById("successScreenWithdraw").style.display = "none";
      document.getElementById("errorScreenWithdraw").style.display = "none";

      // Show the main withdrawal form
      document.getElementById("mainForm").style.display = "block"; // or "flex"

      // Clear the input fields for a new withdrawal
      document.getElementById("accountNumber").value = "";
      document.getElementById("selectedBank").value = "";
      document.getElementById("accountName").value = "";
      document.getElementById("amount").value = "";
      document.getElementById("couponCode").value = "";

      // Ensure the withdrawScreen itself is the active one.
      // Calling showScreen also handles clearing dashboard timers if necessary.
      showScreen('withdrawScreen');
    }

    // New function to go back to the withdraw form from the error screen
    function backToWithdrawFormFromError() {
      document.getElementById("errorScreenWithdraw").style.display = "none";
      document.getElementById("mainForm").style.display = "block";
      // Optionally clear the coupon code field when returning from an error
      document.getElementById("couponCode").value = "";
    }


    // Show welcome screen on initial load
    window.onload = function() {
      showScreen("welcomeScreen");
    }

    // --- User Data Storage (for demonstration purposes only - NOT SECURE for production) ---
    const USERS_KEY = 'registeredUsers';

    function getRegisteredUsers() {
      try {
        return JSON.parse(localStorage.getItem(USERS_KEY)) || {};
      } catch (e) {
        console.error("Error parsing registered users from localStorage:", e);
        return {};
      }
    }

    function saveRegisteredUsers(users) {
      localStorage.setItem(USERS_KEY, JSON.stringify(users));
    }

    // --- Registration Logic ---
    document.getElementById("registerForm").addEventListener("submit", function(e) {
      e.preventDefault();

      const username = document.getElementById("regUsername").value.trim();
      const email = document.getElementById("regEmail").value.trim();
      const password = document.getElementById("regPassword").value;
      const registerMessage = document.getElementById("registerMessage");
      const errorSoundGeneral = document.getElementById("errorSound_general");

      if (!username || !email || !password) {
        alert("Please fill in all registration fields.");
        errorSoundGeneral.play();
        return;
      }

      let users = getRegisteredUsers();

      if (users[email]) {
        alert("This email is already registered. Please login or use a different email.");
        errorSoundGeneral.play();
        return;
      }

      registerMessage.style.display = "block";
      registerMessage.textContent = "Registering...";

      setTimeout(() => {
        users[email] = {
          username: username,
          password: password
        };
        saveRegisteredUsers(users);

        registerMessage.textContent = "Registration successful! Redirecting to app...";
        localStorage.setItem('loggedInUserEmail', email); // Store for dashboard to know who is logged in

        document.getElementById("successSound").play();

        setTimeout(() => {
          registerMessage.style.display = "none";
          showScreen("dashboardScreen");
        }, 1000);
      }, 2000);
    });


    // --- Login Logic ---
    document.getElementById("loginForm").addEventListener("submit", function(e) {
      e.preventDefault();

      const emailInput = document.getElementById("email").value.trim(); // Renamed to avoid conflict
      const passwordInput = document.getElementById("password").value; // Renamed to avoid conflict
      const loadingMsg = document.getElementById("loadingMessage");
      const errorSoundGeneral = document.getElementById("errorSound_general");

      let users = getRegisteredUsers();
      const user = users[emailInput];

      if (user && user.password === passwordInput) {
        loadingMsg.style.display = "block";
        loadingMsg.textContent = "Logging in, please wait...";

        setTimeout(function() {
          loadingMsg.style.display = "none";
          localStorage.setItem('loggedInUserEmail', emailInput); // Store for dashboard
          showScreen("dashboardScreen");
          document.getElementById("successSound").play();
        }, 2000);
      } else {
        alert("Invalid email or password.");
        errorSoundGeneral.play();
      }
    });

    // --- Dashboard Logic (Claim App) ---
    let balance = parseInt(localStorage.getItem('userBalance') || '0', 10);
    const claimCooldown = 8 * 60 * 60 * 1000; // 8 hours
    const claimStartKey = 'claimStart';
    const maxDuration = 4 * 24 * 60 * 60 * 1000; // 4 days
    let claimIntervalId;


    const claimData = [{
      amount: 65000,
      minutes: 20
    }, {
      amount: 65000,
      minutes: 15
    }, {
      amount: 65000,
      minutes: 16
    }, {
      amount: 65000,
      minutes: 14
    }];

    function updateBalanceDisplay() {
      const balanceEl = document.getElementById("balance");
      if (balanceEl) {
        balanceEl.textContent =
          "₦" + balance.toLocaleString("en-NG", {
            minimumFractionDigits: 2,
            maximumFractionDigits: 2
          });
      }
    }

    function showNotification(message) {
      const notification = document.getElementById("notification");
      if (notification) {
        notification.textContent = message;
        notification.style.display = "block";
        setTimeout(() => {
          notification.style.display = "none";
        }, 3000);
      }
    }

    function incrementNotification() {
      let count = parseInt(localStorage.getItem('notificationCount') || '0', 10);
      count += 1;
      localStorage.setItem('notificationCount', count.toString());
      updateNotificationDisplay();
    }

    function updateNotificationDisplay() {
      const count = parseInt(localStorage.getItem('notificationCount') || '0', 10);
      const badge = document.getElementById('notificationCount');
      if (badge) {
        if (count > 0) {
          badge.style.display = 'inline';
          badge.textContent = count;
        } else {
          badge.style.display = 'none';
        }
      }
    }

    function updateUsernameDisplay() {
      const loggedInUserEmail = localStorage.getItem('loggedInUserEmail');
      const usernameDisplayEl = document.getElementById('usernameDisplay');

      if (loggedInUserEmail && usernameDisplayEl) {
        const users = getRegisteredUsers();
        const currentUser = users[loggedInUserEmail];
        if (currentUser && currentUser.username) {
          usernameDisplayEl.textContent = currentUser.username;
        } else {
          usernameDisplayEl.textContent = '';
        }
      }
    }

    function claimAmount(index, button) {
      const now = Date.now();
      const successSound = document.getElementById("successSound");
      const errorSound = document.getElementById("errorSound");

      if (!localStorage.getItem(claimStartKey)) {
        localStorage.setItem(claimStartKey, now);
      }

      const start = parseInt(localStorage.getItem(claimStartKey), 10);
      if (now - start > maxDuration) {
        showNotification("⛔ Claiming period (4 days) is over.");
        if (errorSound) errorSound.play();
        return;
      }

      const lastClaim = localStorage.getItem(`claim_${index}`);
      if (lastClaim && now - parseInt(lastClaim, 10) < claimCooldown) {
        const remainingTime = claimCooldown - (now - parseInt(lastClaim, 10));
        const hoursLeft = Math.floor(remainingTime / (60 * 60 * 1000));
        const minutesLeft = Math.floor((remainingTime % (60 * 60 * 1000)) / (60 * 1000));
        showNotification(`⏳ Come back in ${hoursLeft}h ${minutesLeft}m to claim again.`);
        if (errorSound) errorSound.play();
        return;
      }

      balance += claimData[index].amount;
      localStorage.setItem('userBalance', balance.toString());
      updateBalanceDisplay();
      localStorage.setItem(`claim_${index}`, now.toString());

      showNotification("🎉 You received ₦65,000!");
      if (successSound) successSound.play();
      incrementNotification();
      renderClaimCards();
    }


    function getTimeRemainingFormatted(ms) {
      if (ms <= 0) return "00:00:00";
      const totalSec = Math.floor(ms / 1000);
      const hrs = Math.floor(totalSec / 3600);
      const mins = Math.floor((totalSec % 3600) / 60);
      const secs = totalSec % 60;
      return `${String(hrs).padStart(2, '0')}:${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
    }

    function renderClaimCards() {
      const container = document.getElementById("claimSection");
      if (!container) return;
      container.innerHTML = "";
      const now = Date.now();
      claimData.forEach((data, index) => {
        const lastClaim = localStorage.getItem(`claim_${index}`);
        let remaining = 0;
        let claimReady = true;
        if (lastClaim) {
          const elapsed = now - parseInt(lastClaim, 10);
          remaining = claimCooldown - elapsed;
          if (remaining > 0) claimReady = false;
        }
        let timeDisplay = claimReady ? `<span style="color:green">Ready to Claim</span>` : `<span id="timer_${index}" style="color:red">${getTimeRemainingFormatted(remaining)}</span>`;
        const card = document.createElement("div");
        card.className = "claim-card";
        card.innerHTML = `
         <div class="badge">New</div>
         <p>₦${data.amount.toLocaleString("en-NG", { minimumFractionDigits: 2 })}</p>
         <p>${timeDisplay}</p>
         <button onclick="claimAmount(${index}, this)" ${claimReady ? "" : "disabled"}>
           ${claimReady ? "Claim" : "Wait"}
         </button>`
        container.appendChild(card);
      });
    }

    function startClaimTimer() {
        clearInterval(claimIntervalId); // Clear any existing timer
        claimIntervalId = setInterval(() => {
            const now = Date.now();
            claimData.forEach((data, index) => {
                const timerEl = document.getElementById(`timer_${index}`);
                if (timerEl) {
                    const lastClaim = localStorage.getItem(`claim_${index}`);
                    if (lastClaim) {
                        const remaining = claimCooldown - (now - parseInt(lastClaim, 10));
                        if(remaining > 0) {
                            timerEl.textContent = getTimeRemainingFormatted(remaining);
                        } else {
                            // Timer finished, re-render this card to show "Ready to Claim"
                            renderClaimCards();
                        }
                    }
                }
            });
        }, 1000);
    }
    
    // --- Withdrawal Logic ---
    document.getElementById("initiateWithdrawal").addEventListener("click", function() {
        const accountNumber = document.getElementById("accountNumber").value;
        const selectedBank = document.getElementById("selectedBank").value;
        const accountName = document.getElementById("accountName").value;
        const amount = document.getElementById("amount").value;
        const couponCode = document.getElementById("couponCode").value;
        
        // Basic validation
        if (!accountNumber || !selectedBank || !accountName || !amount || !couponCode) {
            alert("Please fill all withdrawal fields.");
            return;
        }
        
        // --- THIS IS A MOCK LOGIC ---
        // In a real app, you would verify the coupon code with a server.
        // For this demo, we'll use a hardcoded coupon code.
        const VALID_COUPON = "LIVEPAY2024";
        
        if (couponCode.toUpperCase() === VALID_COUPON) {
            // Success
            document.getElementById("mainForm").style.display = "none";
            document.getElementById("errorScreenWithdraw").style.display = "none";
            const successScreen = document.getElementById("successScreenWithdraw");
            successScreen.style.display = "block";
            
            // Populate summary
            document.getElementById("summaryName").textContent = accountName;
            document.getElementById("summaryAmount").textContent = "₦" + parseFloat(amount).toLocaleString('en-NG', {minimumFractionDigits: 2});
            document.getElementById("summaryRef").textContent = "DP" + Date.now(); // Dummy reference
            document.getElementById("summaryWalletNumber").textContent = accountNumber;
            document.getElementById("summaryBank").textContent = selectedBank;

        } else {
            // Error
            document.getElementById("mainForm").style.display = "none";
            document.getElementById("successScreenWithdraw").style.display = "none";
            document.getElementById("errorScreenWithdraw").style.display = "block";
        }
    });
    
    // --- Event Listeners for Profile Image ---
    document.getElementById("profileUpload").addEventListener("change", function(event) {
        if (event.target.files && event.target.files[0]) {
            const reader = new FileReader();
            reader.onload = function(e) {
                document.getElementById("profileImage").src = e.target.result;
            }
            reader.readAsDataURL(event.target.files[0]);
        }
    });

  </script>
</body>

</html>
