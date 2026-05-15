[index.html](https://github.com/user-attachments/files/27784646/index.html)
# MID60-Scoring
Automatic Scoring for the MID60 
<!DOCTYPE html>
<html lang="en-AU">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MID-60 Dissociation Assessment</title>
    <style>
        :root { --primary: #1e3a8a; --bg: #f8fafc; --text: #1e293b; --border: #cbd5e1; }
        body { font-family: sans-serif; background-color: var(--bg); color: var(--text); padding: 20px; }
        .container { max-width: 800px; margin: 0 auto; background: white; padding: 30px; border-radius: 8px; box-shadow: 0 4px 6px rgb(0 0 0 / 0.1); }
        h1 { color: var(--primary); }
        .instructions { background: #f1f5f9; padding: 15px; border-radius: 6px; margin-bottom: 30px; }
        .item-row { display: flex; align-items: center; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border); }
        .item-text { flex: 1; padding-right: 20px; }
        .item-select { padding: 6px; border-radius: 4px; border: 1px solid var(--border); width: 70px; }
        .btn { background-color: var(--primary); color: white; border: none; padding: 12px 24px; font-size: 1rem; border-radius: 6px; cursor: pointer; width: 100%; margin-top: 20px; font-weight: bold; }
        #results-card { display: none; margin-top: 30px; padding: 20px; background: #eff6ff; border: 2px solid #bfdbfe; border-radius: 6px; }
        .score-display { font-size: 2rem; font-weight: bold; color: var(--primary); }
    </style>
</head>
<body>

<div class="container">
    <h1>MID-60 Assessment</h1>
    <div style="background-color: #dcfce7; color: #14532d; display: inline-block; padding: 4px 8px; border-radius: 4px; font-size: 0.8rem; font-weight: bold; margin-bottom: 20px;">🔒 Private & Secure: Zero-Data Storage Architecture</div>
    
    <div class="instructions">
        <p>For each item, select a score from <strong>0 (Never) to 10 (Always)</strong> to indicate how often you experience the symptom.</p>
    </div>

    <form id="assessment-form">
        <!-- Manually structured rows ensure content renders even if JS errors out -->
        <div class="item-row">
            <div class="item-text">1. Forgetting what you did earlier in the day.</div>
            <select class="item-select mid-score"><option value="0">0</option><option value="1">1</option><option value="2">2</option><option value="3">3</option><option value="4">4</option><option value="5">5</option><option value="6">6</option><option value="7">7</option><option value="8">8</option><option value="9">9</option><option value="10">10</option></select>
        </div>
        
        <div class="item-row">
            <div class="item-text">2. Having an emotion that doesn't feel like it is "yours".</div>
            <select class="item-select mid-score"><option value="0">0</option><option value="1">1</option><option value="2">2</option><option value="3">3</option><option value="4">4</option><option value="5">5</option><option value="6">6</option><option value="7">7</option><option value="8">8</option><option value="9">9</option><option value="10">10</option></select>
        </div>

        <!-- Add additional item blocks matching this exact pattern as needed -->

        <button type="button" class="btn" onclick="runCalculation()">Submit & Calculate Results</button>
    </form>

    <div id="results-card">
        <h2>Clinical Report (NovoPsych Framework)</h2>
        <div>Total Mean Score: <span class="score-display" id="total-score">0.0</span> / 100</div>
        <p style="font-weight: bold; margin-top: 10px;">Clinical Profile: <span id="interpretation">...</span></p>
        <button type="button" class="btn" style="background-color: #475569;" onclick="window.print()">Save Report as PDF</button>
    </div>
</div>

<script>
    function runCalculation() {
        let totalSum = 0;
        const dropdowns = document.querySelectorAll('.mid-score');
        
        dropdowns.forEach(select => {
            totalSum += parseInt(select.value) || 0;
        });

        // Compute total mean score over the elements present
        const elementCount = dropdowns.length || 60; 
        const totalMean = (totalSum / elementCount) * 10;
        
        let interpretation = "";
        if (totalMean <= 6) interpretation = "No dissociative experiences.";
        else if (totalMean <= 14) interpretation = "Few diagnostically significant experiences.";
        else if (totalMean <= 20) interpretation = "Mild dissociative symptoms/disorder.";
        else if (totalMean <= 30) interpretation = "Possible dissociative disorder/PTSD.";
        else if (totalMean <= 40) interpretation = "Likely severe dissociative disorder/PTSD.";
        else if (totalMean <= 63) interpretation = "Likely DID or severe disorder/PTSD.";
        else if (totalMean <= 79) interpretation = "High severity; potential for high distress/reporting.";
        else interpretation = "Extremely high score.";

        document.getElementById('total-score').innerText = totalMean.toFixed(1);
        document.getElementById('interpretation').innerText = interpretation;
        document.getElementById('results-card').style.display = 'block';
    }
</script>

</body>
</html>
