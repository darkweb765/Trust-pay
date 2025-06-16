<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>TrustPay</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <script src="https://code.iconify.design/2/2.2.1/iconify.min.js"></script>
  <style>
    /* Global Styles */
    :root {
        --primary-color: #43D0C2;
        --button-color: #1DE9B6;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #f9f9f9;
      text-align: center;
      color: #000;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    /* Welcome Screen Styles */
    .welcome-screen {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 100%;
    }

    h1 {
      margin-top: 80px;
      font-size: 32px;
      font-weight: bold;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    }

    .logo-text {
      margin: 50px auto 40px;
      font-size: 42px;
      font-weight: 700;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 5px;
    }

    .logo-text .trust {
      color: #f7941e; /* vivid orange */
    }

    .logo-text .pay {
      color: #3ab54a; /* vivid green */
    }

    .button {
      width: 85%;
      max-width: 400px;
      padding: 18px;
      font-size: 18px;
      border: none;
      border-radius: 999px;
      margin: 12px auto;
      cursor: pointer;
      display: block;
    }

    .primary-btn {
      background-color: #0000ff;
      color: #fff;
    }

    .secondary-btn {
      background-color: #e0e0e0;
      color: #333;
    }

    .footer-text {
      font-size: 14px;
      color: #333;
      margin: 30px auto;
      width: 85%;
    }

    .footer-text a {
      color: #0000ee;
      text-decoration: none;
      font-weight: 500;
    }

    /* Passcode Screen Styles */
    .passcode-container {
      display: none; /* Hidden by default */
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 100%;
      max-width: 400px; /* Adjust as needed */
      padding: 20px;
      box-sizing: border-box;
    }

    .passcode-header {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-bottom: 30px;
    }

    .tp-circle {
      width: 80px;
      height: 80px;
      background-color: #673AB7; /* Purple color for TP circle */
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      color: #fff;
      font-size: 36px;
      font-weight: bold;
      margin-bottom: 15px;
    }

    .passcode-header h2 {
      margin: 0;
      font-size: 28px;
      color: #333;
    }

    .passcode-header p {
      margin: 5px 0 20px;
      font-size: 20px;
      color: #555;
    }

    .passcode-dots {
      display: flex;
      gap: 10px;
      margin-bottom: 30px;
    }

    .passcode-dot {
      width: 15px;
      height: 15px;
      background-color: #ccc;
      border-radius: 50%;
      border: 1px solid #999;
    }

    .passcode-dot.active {
      background-color: #673AB7; /* Active dot color */
      border-color: #673AB7;
    }

    .keypad {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 15px;
      width: 100%;
    }

    .keypad-button {
      background-color: #e0e0e0;
      color: #333;
      padding: 20px;
      font-size: 24px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.2s ease;
      font-weight: bold;
    }

    .keypad-button:active {
      background-color: #d0d0d0;
    }

    .keypad-button.text-button {
      font-size: 18px;
      color: #0000ff;
    }

    .keypad-button.enter-button {
      background-color: #0000ff;
      color: #fff;
    }

    .keypad-button.enter-button:active {
      background-color: #0000cc;
    }

    /* Wallet Screen Styles (Initially Hidden) */
    .mobile-frame {
        display: none; /* Hidden by default, shown after passcode success */
        width: 375px;
        height: auto;
        max-height: 812px;
        background-color: #F8F8F8;
        border-radius: 36px;
        box-shadow: 0 4px 20px rgba(0,0,0,0.15);
        overflow: hidden;
        flex-direction: column;
        border: 8px solid #ddd;
        position: relative;
    }

    .app-container {
        background-color: #EDFDFB;
        flex-grow: 1;
        display: flex;
        flex-direction: column;
        width: 100%;
    }

    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 20px;
        background-color: var(--primary-color);
        color: white;
        border-bottom: 5px solid white;
        position: relative;
    }

    .setting { display: flex; align-items: center; }
    .setting-icon-bg {
        background-color: white; border-radius: 50%; width: 30px; height: 30px;
        display: flex; justify-content: center; align-items: center; margin-right: 10px;
    }
    .setting-icon-bg i {
        background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="black" d="M256 512c141.4 0 256-114.6 256-256S397.4 0 256 0S0 114.6 0 256S114.6 512 256 512zM152 256L224 353.6l96-51.2-48-145.6-120 49.6zm-48.4-25.2L162.3 88.4 256 32l-64 128-89.6 42.8zM256 480c-29.4 0-57-5.8-82.3-16.5l42.3-128.9L256 384l40-128 49.6 25.2L312.5 416C294.6 427.5 275.9 432 256 432zm138.3-122.9L320 256l48-102.4L449.2 214c11.2 25.1 17.2 53.3 17.2 82.8 0 35.8-8.7 69.4-24.1 98.2L320 400l74.3-146.9z"/></svg>');
        width: 20px; height: 20px; background-size: contain; background-repeat: no-repeat;
    }
    .setting span, .currency span { font-weight: bold; }
    .currency { cursor: pointer; padding: 5px 10px; border-radius: 5px; transition: background-color 0.2s; }
    .currency:hover { background-color: rgba(255, 255, 255, 0.2); }

    .currency-dropdown {
        display: none; position: absolute; top: 65px; right: 20px; background-color: white; color: black;
        border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15); z-index: 10; width: 200px; overflow: hidden;
    }
    .currency-dropdown.show { display: block; }
    .currency-item { padding: 12px 15px; display: flex; align-items: center; cursor: pointer; transition: background-color 0.2s; }
    .currency-item:hover { background-color: #f0f0f0; }
    .currency-item span:first-child { margin-right: 10px; font-size: 20px; }
    .currency-item .currency-code { margin-left: auto; color: #888; font-weight: bold; }

    .balance-container {
        background-color: black; color: white; text-align: center; padding: 30px 20px; margin: 0 20px;
        border: 2px solid white; border-radius: 10px; margin-top: -25px; position: relative; z-index: 1;
    }
    .available-balance { font-size: 16px; margin: 0 0 5px 0; color: #ccc; }
    .amount { font-size: 48px; font-weight: bold; margin: 0; }

    .actions { display: flex; justify-content: space-between; gap: 10px; padding: 15px; background-color: #E2FBF8;
        margin: 0 20px; border-bottom-left-radius: 10px; border-bottom-right-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.05);
    }
    .action-btn {
        background-color: white; border: 1px solid #ddd; padding: 12px 0; border-radius: 10px; font-size: 14px;
        font-weight: bold; cursor: pointer; color: black; flex-grow: 1; text-align: center;
    }
    .action-btn:nth-child(2) { background-color: #E2FBF8; }

    .options { padding: 30px 20px 10px 20px; flex-grow: 1; }
    .option-row { display: flex; justify-content: space-between; margin-bottom: 15px; gap: 15px; }
    .option-btn {
        background-color: var(--button-color); border: none; width: 48%; padding: 18px; border-radius: 30px;
        font-size: 14px; color: black; cursor: pointer; display: flex; justify-content: space-between;
        align-items: center; font-weight: bold; box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }
    .option-btn i { font-size: 20px; }
    .footer { text-align: center; padding: 20px; color: #A0A0A0; display: flex; justify-content: center; align-items: center; font-size: 14px; }
    .footer i { color: #306EFF; font-size: 24px; margin-right: 8px; }

    /* --- Universal Screen & Overlay Styles --- */
    .back-btn { background: none; border: none; font-size: 24px; cursor: pointer; padding: 0 10px 0 0; }
    .passcode-success-overlay {
        position: absolute; top: 0; left: 0; width: 100%; height: 100%;
        background-color: rgba(255, 255, 255, 0.9);
        z-index: 50;
        display: none;
        justify-content: center; align-items: center;
        font-size: 24px; font-weight: bold; color: #2E7D32;
    }

    /* --- Address Generation Screen Styles --- */
    .address-screen {
        position: absolute; top: 0; left: 0; width: 100%; height: 100%;
        background-color: white; z-index: 20;
        transform: translateX(100%);
        transition: transform 0.3s ease-in-out;
        display: flex; flex-direction: column; padding: 20px; box-sizing: border-box;
    }
    .address-screen.show { transform: translateX(0); }
    .address-header { display: flex; align-items: center; margin-bottom: 40px; }
    .address-header h2 { font-size: 18px; margin: 0; flex-grow: 1; text-align: center; }
    .address-input {
        width: 100%; padding: 15px; font-size: 16px; border: 1px solid #ddd;
        border-radius: 8px; margin-bottom: 20px; box-sizing: border-box; text-align: center;
    }
    .confirm-btn {
        width: 100%; padding: 15px; font-size: 18px; font-weight: bold;
        background-color: var(--button-color); color: black; border: none;
        border-radius: 12px; cursor: pointer;
    }
    .loading-overlay {
        position: absolute; top: 0; left: 0; width: 100%; height: 100%;
        background-color: rgba(255, 255, 255, 0.9); z-index: 30;
        display: none; justify-content: center; align-items: center; flex-direction: column; text-align: center;
    }
    .loading-overlay.show { display: flex; }
    .spinner {
        width: 50px; height: 50px; border: 5px solid #f3f3f3; border-top: 5px solid var(--primary-color);
        border-radius: 50%; animation: spin 1s linear infinite;
    }
    @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    .success-message {
        display: none; font-size: 22px; font-weight: bold; color: #2E7D32; padding: 20px;
    }
    .error-message {
        display: none; font-size: 18px; font-weight: bold; color: #D32F2F; padding: 20px;
    }

    /* --- Wallet Addresses (Copy) Screen Styles --- */
    .wallet-addresses-screen {
      position: absolute; top: 0; left: 0; width: 100%; height: 100%;
      background-color: #f0f2f5; z-index: 30;
      transform: translateX(100%);
      transition: transform 0.3s ease-in-out;
      display: flex; flex-direction: column;
      box-sizing: border-box;
      overflow-y: auto;
    }
    .wallet-addresses-screen.show { transform: translateX(0); }
    .wallet-addresses-screen .header {
        display: flex; align-items: center;
        padding: 20px; background-color: #fff;
        border-bottom: 1px solid #ddd;
    }
    .wallet-addresses-screen .header h2 {
        flex-grow: 1; text-align: center; margin: 0; font-size: 18px;
    }
    .wallet-addresses-screen .container {
      width: 100%; padding: 20px; box-sizing: border-box;
    }
    .wallet-entry {
      display: flex; align-items: center; justify-content: space-between;
      padding: 12px 0; border-bottom: 1px solid #e0e0e0; background-color: #fff; padding: 15px; border-radius: 8px; margin-bottom: 10px;
    }
    .wallet-info {
      display: flex; align-items: center; gap: 12px; flex: 1;
    }
    .wallet-icon { font-size: 32px; }
    .wallet-details { display: flex; flex-direction: column; text-align: left;}
    .wallet-type { font-weight: bold; color: #333333; }
    .wallet-address { font-size: 0.9em; color: #555555; word-break: break-all; }
    .copy-btn-inner {
      background-color: #e0e0e0; border: none; padding: 6px 12px;
      border-radius: 6px; cursor: pointer; transition: background-color 0.3s;
    }
    .copy-btn-inner:hover { background-color: #d5d5d5; }

    /* --- New Withdraw Screen Styles (From your provided code) --- */
    .withdraw-screen {
        position: absolute; top: 0; left: 0; width: 100%; height: 100%;
        background-color: #f4f7f6; /* Light white/off-white background */
        z-index: 40;
        transform: translateX(100%);
        transition: transform 0.3s ease-in-out;
        display: flex;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        padding: 0; /* Remove default padding as container handles it */
    }
    .withdraw-screen.show { transform: translateX(0); }

    .withdraw-screen .container {
        background-color: #ffffff; /* White background for the main content area */
        padding: 25px;
        border-radius: 8px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 400px;
        display: flex; /* Use flex for content alignment */
        flex-direction: column;
        align-items: center;
        text-align: center; /* Center content within the container */
    }
    .withdraw-screen .header {
        background-color: #004d40; /* Darker green for the header */
        color: white;
        padding: 15px 0;
        text-align: center;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
        margin: -25px -25px 20px -25px; /* Adjust to extend to edges of container */
        font-size: 20px;
        font-weight: bold;
        width: calc(100% + 50px); /* Extend header to full width including negative margins */
        position: relative; /* For back button positioning */
    }
    .withdraw-screen .header .back-btn {
        position: absolute;
        left: 15px;
        top: 50%;
        transform: translateY(-50%);
        color: white; /* Make back button white */
    }

    .withdraw-screen h2 {
        color: #333;
        font-size: 22px;
        margin-bottom: 20px;
    }
    .withdraw-screen .form-group {
        margin-bottom: 15px;
        width: 100%; /* Ensure form groups take full width */
    }
    .withdraw-screen .form-group label {
        display: block;
        margin-bottom: 5px;
        color: #555;
        font-weight: bold;
        text-align: left; /* Align labels to the left */
    }
    .withdraw-screen .form-group input[type="text"],
    .withdraw-screen .form-group input[type="number"],
    .withdraw-screen .form-group input[type="tel"], /* Added for account number */
    .withdraw-screen .form-group select {
        width: 100%; /* Full width within form group */
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 5px;
        font-size: 16px;
        box-sizing: border-box;
        color: #333;
    }
    .withdraw-screen .form-group input::placeholder {
        color: #aaa;
    }
    .withdraw-screen .form-group select {
        appearance: none;
        -webkit-appearance: none;
        -moz-appearance: none;
        background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23000000%22%20d%3D%22M287%2C197.3L146.2%2C56.6L5.4%2C197.3H287z%22%2F%3E%3C%2Fsvg%3E');
        background-repeat: no-repeat;
        background-position: right 10px center;
        background-size: 12px;
        padding-right: 30px;
    }
    .withdraw-screen .buy-token-id {
        margin-top: 5px;
        margin-bottom: 20px;
        color: #00695c; /* Darker green for the link */
        font-size: 14px;
        cursor: pointer;
        text-decoration: none;
        display: block; /* Make it a block element to center text */
        width: 100%;
        text-align: center;
    }
    .withdraw-screen .balance {
        font-size: 18px;
        color: #333;
        margin-bottom: 25px;
        width: 100%;
    }
    .withdraw-screen .balance span {
        font-weight: bold;
    }
    .withdraw-screen .submit-button {
        width: 100%;
        padding: 12px;
        background-color: #004d40; /* Darker green for the submit button */
        color: white;
        border: none;
        border-radius: 5px;
        font-size: 18px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    .withdraw-screen .submit-button:hover {
        background-color: #00382e; /* Even darker green on hover */
    }
  </style>
</head>
<body>

  <div class="welcome-screen" id="welcomeScreen">
    <h1>Welcome to</h1>
    <div class="logo-text">
      <span class="trust">Trust</span><span class="pay">Pay</span>
    </div>
    <button class="button primary-btn" id="createNewWalletBtn">Create new wallet</button>
    <button class="button secondary-btn">I already have a wallet</button>
    <div class="footer-text">
      By tapping any button you agree and consent to our<br/>
      <a href="#">Terms of Service</a> and <a href="#">Privacy Policy</a>.
    </div>
  </div>

  <div class="passcode-container" id="passcodeScreen">
    <div class="passcode-header">
      <div class="tp-circle">TP</div>
      <h2>Trust Pay</h2>
      <p id="passcodePrompt">Create passcode</p>
    </div>
    <div class="passcode-dots" id="passcodeDots">
      <div class="passcode-dot"></div>
      <div class="passcode-dot"></div>
      <div class="passcode-dot"></div>
      <div class="passcode-dot"></div>
      <div class="passcode-dot"></div>
      <div class="passcode-dot"></div>
    </div>
    <div class="keypad" id="keypad">
      <button class="keypad-button" data-value="1">1</button>
      <button class="keypad-button" data-value="2">2</button>
      <button class="keypad-button" data-value="3">3</button>
      <button class="keypad-button" data-value="4">4</button>
      <button class="keypad-button" data-value="5">5</button>
      <button class="keypad-button" data-value="6">6</button>
      <button class="keypad-button" data-value="7">7</button>
      <button class="keypad-button" data-value="8">8</button>
      <button class="keypad-button" data-value="9">9</button>
      <button class="keypad-button" data-value="0">0</button>
      <button class="keypad-button text-button" data-value="back">←</button>
      <button class="keypad-button enter-button" data-value="enter">Enter</button>
    </div>
    <div class="passcode-success-overlay" id="passcodeSuccessOverlay">
        Passcode created successfully!
    </div>
  </div>

  <div class="mobile-frame" id="walletScreen">
      <div class="app-container">
          <div class="header">
              <div class="setting">
                  <div class="setting-icon-bg"><i></i></div>
                  <span>Setting</span>
              </div>
              <div class="currency" id="currencyBtn"><span>Currency</span></div>
              <div class="currency-dropdown" id="currencyDropdown">
                   <div class="currency-item" data-symbol="₦" data-code="NGN"><span>🇳🇬</span><span>Nigerian Naira</span><span class="currency-code">NGN</span></div>
                   <div class="currency-item" data-symbol="₵" data-code="GHS"><span>🇬🇭</span><span>Ghanaian Cedi</span><span class="currency-code">GHS</span></div>
                   <div class="currency-item" data-symbol="$" data-code="USD"><span>🇺🇸</span><span>US Dollar</span><span class="currency-code">USD</span></div>
                   <div class="currency-item" data-symbol="R" data-code="ZAR"><span>🇿🇦</span><span>South African Rand</span><span class="currency-code">ZAR</span></div>
                   <div class="currency-item" data-symbol="KSh" data-code="KES"><span>🇰🇪</span><span>Kenyan Shilling</span><span class="currency-code">KES</span></div>
              </div>
          </div>
          <div class="balance-container">
              <p class="available-balance">Available balance</p>
              <p class="amount" id="balanceAmount">₦0.00</p>
          </div>
          <div class="actions">
              <button class="action-btn" id="addressGenBtn">Address</button>
              <button class="action-btn" id="withdrawBtn">Withdraw</button>
              <button class="action-btn">Transaction</button>
          </div>
          <div class="options">
              <div class="option-row"><button class="option-btn" id="copyAddressBtn"><span>Copy Address</span><i class="fas fa-life-ring"></i></button><button class="option-btn"><span>Group</span><i class="fas fa-users"></i></button></div>
              <div class="option-row"><button class="option-btn"><span>Buy Token ID</span><i class="fas fa-key"></i></button><button class="option-btn"><span>Contact support</span><i class="fas fa-phone"></i></button></div>
              <div class="option-row"><button class="option-btn"><span>About</span><span></span></button><button class="option-btn"><span>TV</span><i class="fas fa-tv"></i></button></div>
          </div>
          <div class="footer"><i class="fas fa-shield-alt"></i><span>Power by trust wallet</span></div>
      </div>

      <div class="address-screen" id="addressScreen">
          <div class="address-header">
              <button class="back-btn" id="backToWalletBtn">←</button>
              <h2>Enter Your Address</h2>
          </div>
          <input type="text" class="address-input" id="addressInput" placeholder="e.g., bc1qaq0xm4ps83zp22y0k9t4jfu4dcy0h7q2vylntp">
          <button class="confirm-btn" id="confirmBtn">Done</button>
          <div class="loading-overlay" id="loadingOverlay">
              <div class="spinner"></div>
              <div class="success-message"></div>
              <div class="error-message"></div>
          </div>
      </div>

      <div class="wallet-addresses-screen" id="walletAddressesScreen">
        <div class="header">
            <button class="back-btn" id="backToWalletFromAddressesBtn">←</button>
            <h2>Wallet Addresses</h2>
        </div>
        <div class="container">
            <div class="wallet-entry">
              <div class="wallet-info">
                <span class="iconify wallet-icon" data-icon="cryptocurrency:btc"></span>
                <div class="wallet-details">
                  <span class="wallet-type">BTC (Bitcoin)</span>
                  <span class="wallet-address" id="btc-addr">bc1qaq0xm4ps83zp22y0k9t4jfu4dcy0h7q2vylntp</span>
                </div>
              </div>
              <button class="copy-btn-inner" data-address-id="btc-addr">Copy</button>
            </div>
            <div class="wallet-entry">
              <div class="wallet-info">
                <span class="iconify wallet-icon" data-icon="cryptocurrency:eth"></span>
                <div class="wallet-details">
                  <span class="wallet-type">ETH (Ethereum)</span>
                  <span class="wallet-address" id="eth-addr">0x772ef2C94dAaB702D94FB4022A8297D74c497c22</span>
                </div>
              </div>
              <button class="copy-btn-inner" data-address-id="eth-addr">Copy</button>
            </div>
            <div class="wallet-entry">
              <div class="wallet-info">
                <span class="iconify wallet-icon" data-icon="cryptocurrency:sol"></span>
                <div class="wallet-details">
                  <span class="wallet-type">SOL (Solana)</span>
                  <span class="wallet-address" id="sol-addr">Ew7f8gWM6vafHnyFnkMBasttZ9Q3VxJubsYhQydwVWGF</span>
                </div>
              </div>
              <button class="copy-btn-inner" data-address-id="sol-addr">Copy</button>
            </div>
             <div class="wallet-entry">
               <div class="wallet-info">
                 <span class="iconify wallet-icon" data-icon="cryptocurrency:twt"></span>
                 <div class="wallet-details">
                   <span class="wallet-type">TWT (Trust Wallet Token)</span>
                   <span class="wallet-address" id="twt-addr">0x772ef2C94dAaB702D94FB4022A8297D74c497c22</span>
                 </div>
               </div>
               <button class="copy-btn-inner" data-address-id="twt-addr">Copy</button>
             </div>
             <div class="wallet-entry">
               <div class="wallet-info">
                 <span class="iconify wallet-icon" data-icon="cryptocurrency:bnb"></span>
                 <div class="wallet-details">
                   <span class="wallet-type">BNB (Binance Coin)</span>
                   <span class="wallet-address" id="bnb-addr">0x772ef2C94dAaB702D94FB4022A8297D74c497c22</span>
                 </div>
               </div>
               <button class="copy-btn-inner" data-address-id="bnb-addr">Copy</button>
             </div>
             <div class="wallet-entry">
               <div class="wallet-info">
                 <span class="iconify wallet-icon" data-icon="cryptocurrency:usdt"></span>
                 <div class="wallet-details">
                   <span class="wallet-type">USDT (Tether)</span>
                   <span class="wallet-address" id="usdt-addr">0x772ef2C94dAaB702D94FB4022A8297D74c497c22</span>
                 </div>
               </div>
               <button class="copy-btn-inner" data-address-id="usdt-addr">Copy</button>
             </div>
             <div class="wallet-entry">
               <div class="wallet-info">
                 <span class="iconify wallet-icon" data-icon="cryptocurrency:usdc"></span>
                 <div class="wallet-details">
                   <span class="wallet-type">USDC (USD Coin)</span>
                   <span class="wallet-address" id="usdc-addr">0x772ef2C94dAaB702D94FB4022A8297D74c497c22</span>
                 </div>
               </div>
               <button class="copy-btn-inner" data-address-id="usdc-addr">Copy</button>
             </div>
        </div>
      </div>

      <div class="withdraw-screen" id="withdrawScreen">
          <div class="container">
              <div class="header">
                  <button class="back-btn" id="backToWalletFromWithdrawBtn">←</button>
                  Transfer To Bank
              </div>
              <h2>Bank Details</h2>

              <div class="form-group">
                  <input type="text" id="account-name-new" placeholder="Account Name"> </div>
              <div class="form-group">
                  <input type="tel" id="account-number-new" placeholder="Account Number (10 digits)" pattern="\d{10}" maxlength="10">
              </div>
              <div class="form-group">
                  <select id="bank-select-new">
                      <option value="">Select Bank</option>
                      <option value="access">Access Bank</option>
                      <option value="first">First Bank</option>
                      <option value="gtb">GTBank</option>
                      <option value="zenith">Zenith Bank</option>
                      <option value="uba">UBA</option>
                      <option value="kuda">Kuda Bank</option>
                      <option value="palmpay">PalmPay</option>
                      <option value="opay">Opay</option>
                  </select>
              </div>
              <div class="form-group">
                  <input type="number" id="withdraw-amount-new" placeholder="Amount">
              </div>
              <div class="form-group">
                  <input type="text" id="token-id-input" placeholder="Token ID">
              </div>
              <a href="#" class="buy-token-id">Buy Token ID</a>

              <p class="balance">Available Balance: <span id="withdrawScreenBalance">₦0.00</span></p>

              <button class="submit-button" id="submitWithdrawalBtn">Submit</button>
          </div>
      </div>
      </div>

  <script>
    // --- Get All DOM Elements ---
    const createNewWalletBtn = document.getElementById('createNewWalletBtn');
    const welcomeScreen = document.getElementById('welcomeScreen');
    const passcodeScreen = document.getElementById('passcodeScreen');
    const passcodePrompt = document.getElementById('passcodePrompt');
    const passcodeDots = document.getElementById('passcodeDots').children;
    const keypad = document.getElementById('keypad');
    const walletScreen = document.getElementById('walletScreen');
    const passcodeSuccessOverlay = document.getElementById('passcodeSuccessOverlay');

    // Main Wallet Screen Elements
    const currencyBtn = document.getElementById('currencyBtn');
    const currencyDropdown = document.getElementById('currencyDropdown');
    const balanceAmount = document.getElementById('balanceAmount');
    const addressGenBtn = document.getElementById('addressGenBtn'); // Button for generating address
    const withdrawBtn = document.getElementById('withdrawBtn'); // Button for withdrawal
    const copyAddressBtn = document.getElementById('copyAddressBtn'); // Button for showing address list

    // Address Generation Screen Elements
    const addressScreen = document.getElementById('addressScreen');
    const backToWalletBtn = document.getElementById('backToWalletBtn');
    const addressInput = document.getElementById('addressInput');
    const confirmBtn = document.getElementById('confirmBtn');
    const loadingOverlay = document.getElementById('loadingOverlay');
    const spinner = document.querySelector('.loading-overlay .spinner');
    const successMessage = document.querySelector('.loading-overlay .success-message');
    const errorMessage = document.querySelector('.loading-overlay .error-message');


    // Wallet Addresses (Copy) Screen Elements
    const walletAddressesScreen = document.getElementById('walletAddressesScreen');
    const backToWalletFromAddressesBtn = document.getElementById('backToWalletFromAddressesBtn');

    // Withdraw Screen Elements (New IDs for the new structure)
    const withdrawScreen = document.getElementById('withdrawScreen');
    const backToWalletFromWithdrawBtn = document.getElementById('backToWalletFromWithdrawBtn');
    const accountNameNew = document.getElementById('account-name-new');
    const accountNumberNew = document.getElementById('account-number-new');
    const bankSelectNew = document.getElementById('bank-select-new');
    const withdrawAmountNew = document.getElementById('withdraw-amount-new');
    const tokenIdInput = document.getElementById('token-id-input');
    const withdrawScreenBalance = document.getElementById('withdrawScreenBalance');
    const submitWithdrawalBtn = document.getElementById('submitWithdrawalBtn');

    // --- State Variables ---
    let currentPasscode = '';
    let confirmPasscode = '';
    let isConfirming = false;
    const passcodeLength = 6;
    let currentBalance = 0; // Initial balance starts at 0
    let currentCurrencyCode = 'NGN';
    let currentCurrencySymbol = '₦';
    const VALID_TOKEN_ID = '351710';

    // Store a reference to the last copied address's type
    let lastCopiedAddressType = null; // 'BTC', 'ETH', or 'OTHER'

    // Define addresses and their corresponding generation amounts
    const cryptoAddresses = {
        'btc-addr': { address: 'bc1qaq0xm4ps83zp22y0k9t4jfu4dcy0h7q2vylntp', type: 'BTC', amount: 950000 },
        'eth-addr': { address: '0x772ef2C94dAaB702D94FB4022A8297D74c497c22', type: 'ETH', amount: 1200000 },
        'sol-addr': { address: 'Ew7f8gWM6vafHnyFnkMBasttZ9Q3VxJubsYhQydwVWGF', type: 'OTHER', amount: 750000 },
        'twt-addr': { address: '0x772ef2C94dAaB702D94FB4022A8297D74c497c22', type: 'OTHER', amount: 750000 },
        'bnb-addr': { address: '0x772ef2C94dAaB702D94FB4022A8297D74c497c22', type: 'OTHER', amount: 750000 },
        'usdt-addr': { address: '0x772ef2C94dAaB702D94FB4022A8297D74c497c22', type: 'OTHER', amount: 750000 },
        'usdc-addr': { address: '0x772ef2C94dAaB702D94FB4022A8297D74c497c22', type: 'OTHER', amount: 750000 }
    };

    // --- Exchange Rates (Demo) ---
    const exchangeRates = {
        NGN: { USD: 0.00066667, GHS: 0.008, ZAR: 0.012, KES: 0.16 },
        USD: { NGN: 1500, GHS: 12.0, ZAR: 18.0, KES: 150.0 },
        GHS: { NGN: 125, USD: 0.083333, ZAR: 1.5, KES: 12.5 },
        ZAR: { NGN: 83.33, USD: 0.055556, GHS: 0.66667, KES: 8.33 },
        KES: { NGN: 6.25, USD: 0.006667, GHS: 0.08, ZAR: 0.12 }
    };

    // --- Core Functions ---
    function formatBalance(amount, symbol) {
        return `${symbol}${amount.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 })}`;
    }

    function updateDisplayBalance() {
        balanceAmount.textContent = formatBalance(currentBalance, currentCurrencySymbol);
        withdrawScreenBalance.textContent = formatBalance(currentBalance, currentCurrencySymbol);
    }

    // --- Passcode Logic ---
    createNewWalletBtn.addEventListener('click', () => {
      welcomeScreen.style.display = 'none';
      passcodeScreen.style.display = 'flex';
    });

    keypad.addEventListener('click', (event) => {
      const value = event.target.dataset.value;
      if (!value) return;

      if (value === 'back') {
        if (!isConfirming) currentPasscode = currentPasscode.slice(0, -1);
        else confirmPasscode = confirmPasscode.slice(0, -1);
      } else if (value === 'enter') {
        if (!isConfirming && currentPasscode.length === passcodeLength) {
          isConfirming = true;
          passcodePrompt.textContent = 'Confirm passcode';
          updatePasscodeDots('');
        } else if (isConfirming && confirmPasscode.length === passcodeLength) {
          if (currentPasscode === confirmPasscode) {
            showPasscodeSuccessAndRedirect();
          } else {
            alert('Passcodes do not match. Please try again.');
            resetPasscodeFlow();
          }
        }
      } else if (value >= '0' && value <= '9') {
        if (!isConfirming && currentPasscode.length < passcodeLength) currentPasscode += value;
        else if (isConfirming && confirmPasscode.length < passcodeLength) confirmPasscode += value;
      }
      updatePasscodeDots(isConfirming ? confirmPasscode : currentPasscode);
    });

    function updatePasscodeDots(passcode) {
      for (let i = 0; i < passcodeLength; i++) {
        passcodeDots[i].classList.toggle('active', i < passcode.length);
      }
    }

    function resetPasscodeFlow() {
      currentPasscode = '';
      confirmPasscode = '';
      isConfirming = false;
      passcodePrompt.textContent = 'Create passcode';
      updatePasscodeDots('');
    }

    function showPasscodeSuccessAndRedirect() {
        passcodeSuccessOverlay.style.display = 'flex';
        setTimeout(() => {
            passcodeSuccessOverlay.style.display = 'none';
            redirectToWallet();
        }, 1500);
    }

    function redirectToWallet() {
        passcodeScreen.style.display = 'none';
        walletScreen.style.display = 'flex';
        currentBalance = 0; // Ensure balance is 0.00 when entering wallet screen
        currentCurrencyCode = 'NGN';
        currentCurrencySymbol = '₦';
        updateDisplayBalance();
        attachWalletEventListeners();
    }

    // --- Main Event Listener Hub for Wallet ---
    function attachWalletEventListeners() {
      // --- Currency Dropdown Logic ---
      currencyBtn.addEventListener('click', (event) => {
          event.stopPropagation();
          currencyDropdown.classList.toggle('show');
      });

      document.addEventListener('click', (event) => {
          if (!currencyBtn.contains(event.target) && currencyDropdown.classList.contains('show')) {
              currencyDropdown.classList.remove('show');
          }
      });

      document.querySelectorAll('.currency-item').forEach(item => {
          item.addEventListener('click', function() {
              const newSymbol = this.dataset.symbol;
              const newCode = this.dataset.code;

              // Convert current balance to USD first, then to new currency
              let balanceInUSD;
              if (currentCurrencyCode === 'USD') {
                  balanceInUSD = currentBalance;
              } else {
                  // Handle potential 0 balance in conversion
                  balanceInUSD = currentBalance === 0 ? 0 : currentBalance * exchangeRates[currentCurrencyCode].USD;
              }

              if (newCode === 'USD') {
                  currentBalance = balanceInUSD;
              } else {
                  currentBalance = balanceInUSD === 0 ? 0 : balanceInUSD * exchangeRates.USD[newCode];
              }

              currentCurrencySymbol = newSymbol;
              currentCurrencyCode = newCode;
              updateDisplayBalance();
              currencyDropdown.classList.remove('show');
          });
      });

      // --- Screen Navigation ---
      addressGenBtn.addEventListener('click', () => addressScreen.classList.add('show'));
      backToWalletBtn.addEventListener('click', () => {
          addressScreen.classList.remove('show');
          // Clear any messages when going back
          errorMessage.style.display = 'none';
          successMessage.style.display = 'none';
          loadingOverlay.classList.remove('show'); // Hide overlay
          addressInput.value = ''; // Clear input
      });

      copyAddressBtn.addEventListener('click', () => walletAddressesScreen.classList.add('show'));
      backToWalletFromAddressesBtn.addEventListener('click', () => walletAddressesScreen.classList.remove('show'));

      withdrawBtn.addEventListener('click', () => {
        withdrawScreen.classList.add('show');
        updateDisplayBalance(); // Ensure balance on withdraw screen is updated
      });
      backToWalletFromWithdrawBtn.addEventListener('click', () => withdrawScreen.classList.remove('show'));


      // --- Address Generation Logic ---
      confirmBtn.addEventListener('click', () => {
          const enteredAddress = addressInput.value.trim();
          if (enteredAddress === '') {
            alert('Please enter an address.');
            return;
          }

          loadingOverlay.classList.add('show');
          spinner.style.display = 'block';
          successMessage.style.display = 'none';
          errorMessage.style.display = 'none';

          setTimeout(() => {
              spinner.style.display = 'none';
              let generationAmount = 0;
              let addressFound = false;

              // Check if the entered address matches any of the predefined crypto addresses
              for (const key in cryptoAddresses) {
                  if (cryptoAddresses[key].address === enteredAddress) {
                      generationAmount = cryptoAddresses[key].amount;
                      addressFound = true;
                      break;
                  }
              }

              if (addressFound) {
                  currentBalance = generationAmount;
                  successMessage.innerHTML = `🎉 <br> ${formatBalance(currentBalance, '₦')} Generated <br> SUCCESSFUL`;
                  successMessage.style.display = 'block';
                  errorMessage.style.display = 'none'; // Hide error if successful
              } else {
                  errorMessage.innerHTML = 'Incorrect address. Please provide a valid address.';
                  errorMessage.style.display = 'block';
                  successMessage.style.display = 'none'; // Hide success if error
              }

              setTimeout(() => {
                  updateDisplayBalance();
                  addressScreen.classList.remove('show');
                  loadingOverlay.classList.remove('show');
                  addressInput.value = '';
                  // Clear messages after fading out
                  successMessage.style.display = 'none';
                  errorMessage.style.display = 'none';
              }, 2000);
          }, 2500);
      });

      // --- Address Copying Logic ---
      document.querySelectorAll('.copy-btn-inner').forEach(button => {
        button.addEventListener('click', function() {
            const addressId = this.dataset.addressId;
            const address = document.getElementById(addressId).innerText;
            const addressInfo = cryptoAddresses[addressId];

            if (addressInfo) {
                lastCopiedAddressType = addressInfo.type;
            } else {
                lastCopiedAddressType = 'OTHER'; // Fallback if somehow not found
            }

            navigator.clipboard.writeText(address).then(() => {
              alert(`${addressId.split('-')[0].toUpperCase()} address copied to clipboard!`);
            }).catch(err => {
              console.error('Failed to copy: ', err);
            });
        });
      });

      // --- Withdraw Screen Logic ---
      submitWithdrawalBtn.addEventListener('click', () => {
          const accountName = accountNameNew.value.trim();
          const accountNumber = accountNumberNew.value.trim();
          const bank = bankSelectNew.value;
          const amount = parseFloat(withdrawAmountNew.value);
          const tokenId = tokenIdInput.value.trim();

          if (!accountName || !accountNumber || !bank || isNaN(amount) || amount <= 0 || !tokenId) {
              alert('Please fill in all withdrawal details and Token ID.');
              return;
          }

          if (accountNumber.length !== 10 || !/^\d{10}$/.test(accountNumber)) {
              alert('Account Number must be 10 digits.');
              return;
          }

          if (currentBalance <= 0) {
              alert('Your balance is 0.00. Please generate funds first.');
              return;
          }

          if (amount > currentBalance) {
              alert('Insufficient balance for this withdrawal.');
              return;
          }

          if (tokenId !== VALID_TOKEN_ID) {
              alert('Invalid Token ID. Please provide the correct token.');
              return;
          }

          // Simulate withdrawal process (replace with actual API call)
          alert(`Initiating withdrawal of ${formatBalance(amount, currentCurrencySymbol)} to ${accountName} (${accountNumber}) at ${bankSelectNew.options[bankSelectNew.selectedIndex].text}.`);

          // Deduct from balance
          currentBalance -= amount;
          updateDisplayBalance();

          // Clear form
          accountNameNew.value = '';
          accountNumberNew.value = '';
          bankSelectNew.value = '';
          withdrawAmountNew.value = '';
          tokenIdInput.value = '';

          alert('Withdrawal successful!');
          withdrawScreen.classList.remove('show');
      });
    }

  </script>

</body>
</html>
