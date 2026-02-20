# Tracking-

html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Global Number Lookup</title>
    <style>
        body { font-family: sans-serif; text-align: center; padding-top: 50px; background: #f4f4f9; }
        input { padding: 10px; width: 250px; border: 1px solid #ccc; border-radius: 4px; }
        button { padding: 10px 20px; background: #28a745; color: white; border: none; cursor: pointer; }
        #results { margin-top: 20px; font-weight: bold; color: #333; }
    </style>
</head>
<body>
    <h1>Phone Number Info Tracker</h1>
    <p>Enter number with +country code (e.g., +91... or +1...)</p>
    <input type="text" id="phone" placeholder="+1234567890">
    <button onclick="lookup()">Track Info</button>
    <div id="results"></div>

    <script>
        async function lookup() {
            const num = document.getElementById('phone').value;
            const resDiv = document.getElementById('results');
            resDiv.innerHTML = "Searching...";
            
            // Using numverify API (Free tier requires sign-up for your own key)
            const apiKey = 'YOUR_NUMVERIFY_API_KEY'; 
            try {
                const response = await fetch(`http://apilayer.net{apiKey}&number=${num.replace('+','')}`);
                const data = await response.json();
                if(data.valid) {
                    resDiv.innerHTML = `Location: ${data.location}, ${data.country_name}<br>Carrier: ${data.carrier}<br>Line Type: ${data.line_type}`;
                } else {
                    resDiv.innerHTML = "Invalid number format.";
                }
            } catch (e) {
                resDiv.innerHTML = "Error connecting to lookup service.";
            }
        }
    </script>
</body>
</html>
