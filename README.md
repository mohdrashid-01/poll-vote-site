<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <title>पहलगाम हमला पोल</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Arial', sans-serif;
      background: url('https://images.unsplash.com/photo-1568120507148-6e4b9d6dcb80?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80') no-repeat center center fixed;
      background-size: cover;
      text-align: center;
      color: white;
    }
    .poll-card {
      background: rgba(0, 0, 0, 0.7);
      margin: 50px auto;
      padding: 20px;
      border-radius: 15px;
      width: 90%;
      max-width: 400px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.5);
    }
    button {
      margin: 10px;
      padding: 12px 20px;
      font-size: 18px;
      cursor: pointer;
      border: none;
      border-radius: 8px;
      background-color: #4CAF50;
      color: white;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #45a049;
    }
    #result, #thankyou, #shareBtn {
      margin-top: 20px;
      display: none;
    }
    .bar {
      height: 20px;
      background: #4CAF50;
      margin: 10px 0;
      border-radius: 10px;
    }
    #shareBtn {
      background-color: #25D366;
    }
  </style>
</head>
<body>

<div class="poll-card">
  <h2>पहलगाम कश्मीर में हुए हमले का असली जिम्मेदार कौन?</h2>
  <p>🗓 वोटिंग अंतिम तारीख: 30 जून</p>

  <div id="voteButtons">
    <button onclick="vote('bjp')">🪀 बीजेपी</button>
    <button onclick="vote('congress')">🪀 कांग्रेस</button>
  </div>

  <div id="thankyou">
    <h3>🎉 धन्यवाद! आपने वोट डाला।</h3>
  </div>

  <div id="result">
    <h3>🔍 वोटिंग परिणाम:</h3>
    <p>बीजेपी: <span id="bjp-count">0</span>%</p>
    <div class="bar" id="bjp-bar" style="width: 0%"></div>

    <p>कांग्रेस: <span id="congress-count">0</span>%</p>
    <div class="bar" id="congress-bar" style="width: 0%"></div>
  </div>

  <button id="shareBtn" onclick="shareOnWhatsApp()">📤 व्हाट्सएप पर शेयर करें</button>
</div>

<script>
  let votes = {bjp: 0, congress: 0};
  let totalVotes = 0;

  function vote(party) {
    if (localStorage.getItem('voted')) {
      alert("⚠️ आपने पहले ही वोट डाल दिया है!");
      return;
    }

    votes[party]++;
    totalVotes++;

    let bjpPercent = Math.round((votes.bjp / totalVotes) * 100);
    let congressPercent = Math.round((votes.congress / totalVotes) * 100);

    document.getElementById('bjp-count').innerText = bjpPercent;
    document.getElementById('congress-count').innerText = congressPercent;
    document.getElementById('bjp-bar').style.width = bjpPercent + "%";
    document.getElementById('congress-bar').style.width = congressPercent + "%";

    document.getElementById('result').style.display = "block";
    document.getElementById('thankyou').style.display = "block";
    document.getElementById('voteButtons').style.display = "none";
    document.getElementById('shareBtn').style.display = "inline-block";

    localStorage.setItem('voted', 'true');
  }

  function shareOnWhatsApp() {
    let message = encodeURIComponent("मैंने पहलगाम हमले पर अपनी राय दी! आप भी वोट करें 👉 [अपना वेबसाइट लिंक यहाँ डालें]");
    let url = `https://wa.me/?text=${message}`;
    window.open(url, '_blank');
  }
</script>

</body>
</html>
