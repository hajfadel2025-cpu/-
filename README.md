
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>Display - Haj Fadel</title>
    <style>
        :root {
            --main-bg: radial-gradient(circle, #1a4f8a 0%, #001d3d 100%);
            --panel-bg: rgba(0, 31, 63, 0.9);
            --accent-yellow: #ffd60a;
            --text-white: #ffffff;
        }

        body { margin: 0; padding: 0; background: var(--main-bg); color: var(--text-white); height: 100vh; display: flex; flex-direction: column; overflow: hidden; font-family: Arial, sans-serif; direction: rtl; }

        .top-header { display: flex; justify-content: space-between; align-items: center; padding: 10px 40px; background: rgba(0,0,0,0.2); border-bottom: 2px solid var(--accent-yellow); }
        .office-title { font-size: 2.2vw; font-weight: bold; color: var(--accent-yellow); }
        .logo-circle { width: 50px; height: 50px; background: #fff; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 30px; font-weight: bold; color: #001d3d; }

        .date-time { text-align: left; }
        #clock-time { font-size: 2vw; font-weight: bold; line-height: 1; }
        #clock-date { font-size: 0.9vw; color: #a0c4ff; text-transform: uppercase; margin-top: 5px; font-weight: bold; }

        .main-grid { flex: 1; padding: 2vh 3vw; display: flex; flex-direction: column; gap: 1vh; }
        .grid-header { display: flex; gap: 15px; }
        .h-cell { flex: 1; background: #fff; color: #001d3d; text-align: center; padding: 8px; border-radius: 5px; font-size: 1.2vw; font-weight: bold; }

        .grid-row { display: flex; gap: 15px; margin-bottom: 5px; }
        .cell { flex: 1; background: var(--panel-bg); border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; height: 11vh; display: flex; align-items: center; justify-content: center; font-size: 2.8vw; font-weight: bold; }
        .cell-info { justify-content: space-between; padding: 0 30px; font-size: 1.6vw; color: var(--accent-yellow); }
        .cell-info img { width: 3.5vw; border-radius: 4px; }

        .marquee-footer { background: #000c1a; height: 35px; display: flex; align-items: center; border-top: 2px solid var(--accent-yellow); overflow: hidden; }
        .marquee-inner { white-space: nowrap; font-size: 1.1vw; font-weight: bold; animation: moveLeft 30s linear infinite; padding-right: 100%; }
        @keyframes moveLeft { 0% { transform: translateX(-100%); } 100% { transform: translateX(100%); } }
    </style>
</head>
<body>

    <div class="top-header">
        <div class="date-time">
            <div id="clock-time">00:00:00</div>
            <div id="clock-date">LOADING...</div>
        </div>
        <div style="display:flex; align-items:center; gap:15px;">
            <div class="office-title">&#1605;&#1603;&#1578;&#1576; &#1581;&#1580; &#1601;&#1575;&#1590;&#1604; &#1604;&#1604;&#1589;&#1585;&#1575;&#1601;&#1577;</div>
            <div class="logo-circle">H</div>
        </div>
    </div>

    <div class="main-grid">
        <div class="grid-header">
            <div class="h-cell">&#1576;&#1610;&#1593;</div>
            <div class="h-cell">&#1588;&#1585;&#1575;&#1569;</div>
            <div class="h-cell">&#1575;&#1604;&#1593;&#1605;&#1604;&#1577;</div>
        </div>
        <div id="dynamicRows"></div>
    </div>

    <div class="marquee-footer">
        <div class="marquee-inner">
            &#1605;&#1603;&#1578;&#1576; &#1581;&#1580; &#1601;&#1575;&#1590;&#1604; - &#1571;&#1585;&#1576;&#1610;&#1604; - &#1588;&#1575;&#1585;&#1593; 30 &#1605;&#1578;&#1585;&#1610; - &#1607;&#1575;&#1578;&#1601;: 07501983870 whatsapp Summer Hours: 9:30 AM – 6:30 PM

Winter Hours: 9:30 AM – 5:00 PM 
        </div>
    </div>

<script>
    // ??? ?????? ???? ???????? ????? ??? ??????
    function updateDisplay() {
        const data = localStorage.getItem("office_rates");
        const rates = data ? JSON.parse(data) : [];
        const container = document.getElementById("dynamicRows");
        
        let htmlContent = "";
        const flagMap = { "USD": "us", "EUR": "eu", "TRY": "tr", "GBP": "gb", "IQD": "iq", "SAR": "sa" };

        rates.forEach(item => {
            const flag = flagMap[item.code] || "un";
            htmlContent += `
                <div class="grid-row">
                    <div class="cell">${item.sale}</div>
                    <div class="cell">${item.buy}</div>
                    <div class="cell cell-info"><span>${item.code}</span><img src="https://flagcdn.com/w160/${flag}.png"></div>
                </div>
            `;
        });
        container.innerHTML = htmlContent;
    }

    function updateClock() {
        const now = new Date();
        document.getElementById('clock-time').innerText = now.toLocaleTimeString('en-US', { hour12: true });
        document.getElementById('clock-date').innerText = now.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
    }

    // ??? ????????? ?? 500 ???? ????? (??? ?????) ????? ??????? ??????
    setInterval(updateDisplay, 500);
    setInterval(updateClock, 1000);
    
    updateDisplay();
    updateClock();
</script>
</body>
</html>
