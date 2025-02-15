<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>College Basketball Trading Simulator - Level Up Edition</title>
  <style>
    /* New Clean Color Theme: Dark navy with gold accents */
    body {
      background: #0a0a23;
      color: #f0f0f0;
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 0;
      overflow-x: hidden;
    }
    /* Ticker Styles */
    #ticker-top, #ticker-bottom {
      background: #000;
      border: 2px solid #ffd700;
      box-shadow: 0 0 15px #ffd700;
      overflow: hidden;
      padding: 5px 0;
    }
    .ticker-content {
      white-space: nowrap;
      display: inline-block;
      padding-left: 100%;
      animation: tickerAnimation 12s linear infinite;
      font-size: 1.3em;
      text-transform: uppercase;
      color: #ffd700;
    }
    .ticker-content span {
      margin-right: 30px;
      padding: 0 10px;
    }
    @keyframes tickerAnimation {
      0% { transform: translateX(0); }
      100% { transform: translateX(-100%); }
    }
    /* Section Container */
    .section {
      background: #1a1a2e;
      border: 1px solid #ffd700;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.5);
      margin: 20px 15px;
      padding: 20px;
    }
    h1, h2, h3 {
      text-align: center;
      color: #ffd700;
      margin-bottom: 10px;
      text-transform: uppercase;
    }
    p {
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 10px 0;
    }
    table, th, td {
      border: 1px solid #444;
    }
    th, td {
      padding: 8px;
      text-align: center;
    }
    form {
      margin: 10px 0;
    }
    label {
      display: block;
      margin-top: 10px;
      font-weight: bold;
      color: #ddd;
    }
    select, input[type="number"] {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
      border: 1px solid #444;
      border-radius: 4px;
      background: #222;
      color: #f0f0f0;
    }
    button {
      width: 100%;
      padding: 10px;
      background: #ffd700;
      color: #000;
      border: none;
      border-radius: 4px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 10px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    button:hover {
      background: #e6c200;
    }
    .log, .explanation {
      background: #222;
      border: 1px solid #444;
      border-radius: 6px;
      padding: 10px;
      max-height: 200px;
      overflow-y: auto;
      font-size: 14px;
      margin-top: 10px;
    }
    /* Responsive design */
    @media (max-width: 768px) {
      .section { margin: 10px; }
    }
  </style>
</head>
<body>
  <!-- Top Ticker -->
  <div id="ticker-top">
    <div class="ticker-content" id="tickerTopContent">Loading ticker...</div>
  </div>
  
  <!-- Account Summary Section -->
  <div class="section" id="accountSummary">
    <h2>Account Summary</h2>
    <p>Bank Balance: $<span id="bankBalance">1000000.00</span></p>
    <p>Portfolio Value: $<span id="portfolioValue">0.00</span></p>
    <p>Total Account Value: $<span id="totalValue">1000000.00</span></p>
    <p>Profit/Loss: $<span id="profitLoss">0.00</span></p>
    <p>Level: <span id="playerLevel">1</span> (<span id="playerXP">0</span> XP / <span id="xpThreshold">100</span> XP)</p>
  </div>
  
  <!-- Athlete News Section -->
  <div class="section" id="athleteNews">
    <h2>College Athlete News</h2>
    <div id="newsTicker">Loading news...</div>
  </div>
  
  <!-- Live Market Section -->
  <div class="section" id="liveMarket">
    <h2>Live Market</h2>
    <table id="liveMarketTable">
      <thead>
        <tr>
          <th>Ticker</th>
          <th>Team</th>
          <th>Price ($)</th>
          <th>Change</th>
          <th>% Change</th>
        </tr>
      </thead>
      <tbody>
        <!-- Live market data will be inserted here -->
      </tbody>
    </table>
  </div>
  
  <!-- Team Trading Section -->
  <div class="section" id="teamTrading">
    <h2>Team Trading</h2>
    <form id="teamForm">
      <label for="teamAction">Action:</label>
      <select id="teamAction">
        <option value="buy">Buy Team Shares</option>
        <option value="sell">Sell Team Shares</option>
      </select>
      <label for="teamSelect">Select Team:</label>
      <select id="teamSelect">
        <!-- Options populated via JS -->
      </select>
      <label for="teamShares">Number of Shares:</label>
      <input type="number" id="teamShares" min="1" value="1" />
      <button type="button" id="teamTradeButton">Execute Trade</button>
    </form>
    <h3>Your Portfolio</h3>
    <table id="portfolioTable">
      <thead>
        <tr>
          <th>Team</th>
          <th>Shares Owned</th>
          <th>Current Price</th>
          <th>Total Value</th>
        </tr>
      </thead>
      <tbody>
        <!-- Portfolio data will be inserted here -->
      </tbody>
    </table>
    <div class="log" id="teamLog">
      <p>Team trade log will appear here.</p>
    </div>
  </div>
  
  <!-- Spacing -->
  <div style="height: 30px;"></div>
  
  <!-- Options Trading Section -->
  <div class="section" id="optionsTrading">
    <h2>Options Trading</h2>
    <form id="optionsForm">
      <label for="optionAction">Action:</label>
      <select id="optionAction">
        <option value="buy_call">Buy Call Option</option>
        <option value="buy_put">Buy Put Option</option>
        <option value="sell_call">Sell Call Option</option>
        <option value="sell_put">Sell Put Option</option>
      </select>
      <label for="optionTeamSelect">Select Team:</label>
      <select id="optionTeamSelect">
        <!-- Options populated via JS -->
      </select>
      <label for="optionContracts">Number of Contracts (1 contract = 100 shares):</label>
      <input type="number" id="optionContracts" min="1" value="1" />
      <button type="button" id="optionTradeButton">Execute Options Trade</button>
    </form>
    <div class="log" id="optionsLog">
      <p>Options trade log will appear here.</p>
    </div>
  </div>
  
  <!-- Trade Explanation Section -->
  <div class="section" id="tradeExplanation">
    <h2>Trade Explanation</h2>
    <div class="explanation" id="explanation">
      <p>Detailed explanations of your trades will appear here.</p>
    </div>
  </div>
  
  <!-- Bottom Ticker -->
  <div id="ticker-bottom">
    <div class="ticker-content" id="tickerBottomContent">Loading ticker...</div>
  </div>
  
  <script>
    // ============================================
    // Global Data & Variables
    // ============================================
    let bank = 1000000;
    const startingBank = 1000000;
    const premiumRate = 0.05; // Options premium: 5% per share

    // Leveling system
    let playerLevel = 1;
    let playerXP = 0;
    function addXP(amount) {
      playerXP += amount;
      let xpThreshold = playerLevel * 100;
      if (playerXP >= xpThreshold) {
        playerXP -= xpThreshold;
        playerLevel++;
        alert("Congratulations! You've leveled up to Level " + playerLevel + "!");
      }
      updateAccountSummary();
    }
    
    // 25 College Basketball Teams
    const teams = {
      "DUKE":  { name: "Duke Blue Devils",         price: 120.00, prevPrice: 120.00 },
      "UNC":   { name: "North Carolina Tar Heels",   price: 150.00, prevPrice: 150.00 },
      "KENT":  { name: "Kentucky Wildcats",         price: 100.00, prevPrice: 100.00 },
      "KANS":  { name: "Kansas Jayhawks",           price: 130.00, prevPrice: 130.00 },
      "UCLA":  { name: "UCLA Bruins",               price: 110.00, prevPrice: 110.00 },
      "MSUS":  { name: "Michigan State Spartans",   price: 140.00, prevPrice: 140.00 },
      "VILL":  { name: "Villanova Wildcats",        price: 115.00, prevPrice: 115.00 },
      "SYR":   { name: "Syracuse Orange",           price: 90.00,  prevPrice: 90.00 },
      "ARIZ":  { name: "Arizona Wildcats",          price: 125.00, prevPrice: 125.00 },
      "LOUI":  { name: "Louisville Cardinals",      price: 95.00,  prevPrice: 95.00 },
      "FLOR":  { name: "Florida Gators",            price: 105.00, prevPrice: 105.00 },
      "INDI":  { name: "Indiana Hoosiers",          price: 110.00, prevPrice: 110.00 },
      "TEX":   { name: "Texas Longhorns",           price: 115.00, prevPrice: 115.00 },
      "OSU":   { name: "Ohio State Buckeyes",       price: 125.00, prevPrice: 125.00 },
      "GONZ":  { name: "Gonzaga Bulldogs",          price: 135.00, prevPrice: 135.00 },
      "VIRG":  { name: "Virginia Cavaliers",        price: 120.00, prevPrice: 120.00 },
      "OKLA":  { name: "Oklahoma Sooners",          price: 100.00, prevPrice: 100.00 },
      "TTECH": { name: "Texas Tech Red Raiders",    price: 105.00, prevPrice: 105.00 },
      "BYU":   { name: "BYU Cougars",               price: 95.00,  prevPrice: 95.00 },
      "MARY":  { name: "Maryland Terrapins",        price: 90.00,  prevPrice: 90.00 },
      "WISC":  { name: "Wisconsin Badgers",         price: 115.00, prevPrice: 115.00 },
      "NDIR":  { name: "Notre Dame Fighting Irish", price: 130.00, prevPrice: 130.00 },
      "IOWA":  { name: "Iowa Hawkeyes",             price: 100.00, prevPrice: 100.00 },
      "PURD":  { name: "Purdue Boilermakers",       price: 125.00, prevPrice: 125.00 },
      "CINC":  { name: "Cincinnati Bearcats",       price: 110.00, prevPrice: 110.00 }
    };

    // Portfolio: track shares owned for each team (initially 0)
    let portfolio = {};
    for (const ticker in teams) {
      portfolio[ticker] = 0;
    }

    // ============================================
    // Random College Athlete News Headlines
    // ============================================
    const headlines = [
      "Trey Johnson fined for dribbling in the hallway.",
      "Marcus Williams declares free throws his new ringtone.",
      "Jamal Davis spotted bench-warming at his own practice.",
      "Darius Brown arrested for excessive air dribbling.",
      "Elijah Carter mistakenly dunked a water bottle.",
      "Tyrone Smith traded his sneakers for a pizza.",
      "Andre Lewis benched himself to avoid homework.",
      "Corey Martin claims he invented the crossover move.",
      "Malik Robinson banned for scoring memes with three-pointers.",
      "Devon Clark fined for a layup dance-off.",
      "Xavier Jenkins caught wearing mismatched shoes at practice.",
      "Quentin Harris accidentally scored on his own team.",
      "Jamal Jefferson blames power outages for missed free throws.",
      "Calvin Bryant sets record for halftime selfies.",
      "Leonard Parker orders pizza during every timeout.",
      "Rashad Allen shocks fans playing defense in a game of tag.",
      "Eugene Carter trains with secret coach—his grandma.",
      "Victor Howard spikes a soda can instead of the ball.",
      "Dante Mitchell’s jump shot shatters a gym window.",
      "Trevor King turns the locker room into a dance floor.",
      "Ricky Adams raps his free throw routine.",
      "Jordan Foster practices with a karaoke machine.",
      "Antonio Reed’s crossover confuses even his coach.",
      "Brett Collins challenges a ref to a three-point contest.",
      "Isaiah Powell’s game-winning shot delayed by rogue mascot.",
      "Nolan Bailey’s pregame hype includes a drum solo.",
      "Zachary Mitchell benches his phone for focus.",
      "Marlon Edwards uses a beach ball in scrimmage.",
      "Cody Barnes caught slam dunking in his dorm.",
      "Damien Scott’s hair ruins his free throws—again!"
    ];
    function updateNewsTicker() {
      const newsTicker = document.getElementById("newsTicker");
      const randomHeadline = headlines[Math.floor(Math.random() * headlines.length)];
      newsTicker.innerHTML = `<span>${randomHeadline}</span>`;
    }
    setInterval(updateNewsTicker, 3000);

    // ============================================
    // Ticker & Display Updates
    // ============================================
    function updateTicker() {
      let tickerHTML = "";
      for (const ticker in teams) {
        const team = teams[ticker];
        const change = team.price - team.prevPrice;
        let color = change > 0 ? "lime" : change < 0 ? "red" : "#ffd700";
        tickerHTML += `<span>${ticker} (${team.name}): $${team.price.toFixed(2)}</span>`;
      }
      document.getElementById("tickerTopContent").innerHTML = tickerHTML;
      document.getElementById("tickerBottomContent").innerHTML = tickerHTML;
    }
    
    function animateValue(element, start, end, duration) {
      let startTime = null;
      function animate(currentTime) {
        if (!startTime) startTime = currentTime;
        const progress = currentTime - startTime;
        const value = start + (end - start) * (progress / duration);
        element.innerText = value.toFixed(2);
        if (progress < duration) {
          requestAnimationFrame(animate);
        } else {
          element.innerText = end.toFixed(2);
        }
      }
      requestAnimationFrame(animate);
    }
    function updateBankDisplay(oldBank, newBank) {
      const bankElement = document.getElementById("bankBalance");
      animateValue(bankElement, oldBank, newBank, 500);
      updateAccountSummary();
    }
    
    function updateAccountSummary() {
      let portfolioValue = 0;
      for (const ticker in portfolio) {
        portfolioValue += portfolio[ticker] * teams[ticker].price;
      }
      const totalValue = bank + portfolioValue;
      const profitLoss = totalValue - startingBank;
      document.getElementById("portfolioValue").innerText = portfolioValue.toFixed(2);
      document.getElementById("totalValue").innerText = totalValue.toFixed(2);
      document.getElementById("profitLoss").innerText = profitLoss.toFixed(2);
      document.getElementById("playerLevel").innerText = playerLevel;
      document.getElementById("playerXP").innerText = playerXP;
      document.getElementById("xpThreshold").innerText = playerLevel * 100;
    }
    
    function updateLiveMarket() {
      const tbody = document.querySelector("#liveMarketTable tbody");
      tbody.innerHTML = "";
      for (const ticker in teams) {
        const team = teams[ticker];
        const change = team.price - team.prevPrice;
        const percentChange = (change / team.prevPrice) * 100;
        let changeColor = change >= 0 ? "green" : "red";
        const row = document.createElement("tr");
        row.innerHTML = `<td>${ticker}</td>
                         <td>${team.name}</td>
                         <td>$${team.price.toFixed(2)}</td>
                         <td style="color: ${changeColor};">${change >= 0 ? "+" : ""}${change.toFixed(2)}</td>
                         <td style="color: ${changeColor};">${change >= 0 ? "+" : ""}${percentChange.toFixed(2)}%</td>`;
        tbody.appendChild(row);
      }
    }
    
    function updatePortfolioDisplay() {
      const tbody = document.querySelector("#portfolioTable tbody");
      tbody.innerHTML = "";
      for (const ticker in portfolio) {
        const shares = portfolio[ticker];
        const price = teams[ticker].price;
        const totalValue = shares * price;
        if (shares > 0) {
          const row = document.createElement("tr");
          row.innerHTML = `<td>${teams[ticker].name} (${ticker})</td>
                           <td>${shares}</td>
                           <td>$${price.toFixed(2)}</td>
                           <td>$${totalValue.toFixed(2)}</td>`;
          tbody.appendChild(row);
        }
      }
      if (tbody.innerHTML === "") {
        tbody.innerHTML = "<tr><td colspan='4'>No team shares owned yet.</td></tr>";
      }
    }
    
    function logTeamMessage(message) {
      const logDiv = document.getElementById("teamLog");
      const p = document.createElement("p");
      p.innerHTML = message;
      logDiv.appendChild(p);
      logDiv.scrollTop = logDiv.scrollHeight;
    }
    
    function logOptionsMessage(message) {
      const logDiv = document.getElementById("optionsLog");
      const p = document.createElement("p");
      p.innerHTML = message;
      logDiv.appendChild(p);
      logDiv.scrollTop = logDiv.scrollHeight;
    }
    
    function updateExplanation(text) {
      const explanationDiv = document.getElementById("explanation");
      explanationDiv.innerHTML = `<p>${text}</p>`;
    }
    
    // ============================================
    // Simulate Market Price Movements
    // ============================================
    function simulatePriceMovement(price) {
      const pctChange = (Math.random() * 0.02) - 0.01;
      const newPrice = price * (1 + pctChange);
      return parseFloat(newPrice.toFixed(2));
    }
    
    function updateMarketPrices() {
      for (const ticker in teams) {
        teams[ticker].prevPrice = teams[ticker].price;
        teams[ticker].price = simulatePriceMovement(teams[ticker].price);
      }
      updateTicker();
      updateLiveMarket();
      updatePortfolioDisplay();
      updateAccountSummary();
    }
    
    // ============================================
    // Populate Dropdown Options
    // ============================================
    function populateTeamOptions() {
      const teamSelect = document.getElementById("teamSelect");
      const optionTeamSelect = document.getElementById("optionTeamSelect");
      teamSelect.innerHTML = "";
      optionTeamSelect.innerHTML = "";
      for (const ticker in teams) {
        const option1 = document.createElement("option");
        option1.value = ticker;
        option1.innerText = `${teams[ticker].name} (${ticker})`;
        teamSelect.appendChild(option1);
        const option2 = document.createElement("option");
        option2.value = ticker;
        option2.innerText = `${teams[ticker].name} (${ticker})`;
        optionTeamSelect.appendChild(option2);
      }
    }
    
    // ============================================
    // TEAM TRADING HANDLER
    // ============================================
    document.getElementById("teamTradeButton").addEventListener("click", function() {
      const action = document.getElementById("teamAction").value;
      const ticker = document.getElementById("teamSelect").value;
      const shares = parseInt(document.getElementById("teamShares").value);
      if (shares <= 0) { alert("Enter a valid number of shares."); return; }
      const price = teams[ticker].price;
      const totalCost = price * shares;
      let explanation = "";
      const oldBank = bank;
      
      if (action === "buy") {
        if (bank < totalCost) { alert("Not enough funds to buy."); return; }
        bank -= totalCost;
        portfolio[ticker] += shares;
        explanation = `You bought ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each for $${totalCost.toFixed(2)}.`;
        logTeamMessage(`Bought ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each. Total cost: $${totalCost.toFixed(2)}.`);
      } else if (action === "sell") {
        if (portfolio[ticker] < shares) { alert("You don't own that many shares to sell."); return; }
        bank += totalCost;
        portfolio[ticker] -= shares;
        explanation = `You sold ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each for $${totalCost.toFixed(2)}.`;
        logTeamMessage(`Sold ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each. Total gain: $${totalCost.toFixed(2)}.`);
      }
      
      const newPrice = simulatePriceMovement(price);
      teams[ticker].prevPrice = teams[ticker].price;
      teams[ticker].price = newPrice;
      explanation += ` After your trade, the price changed from $${price.toFixed(2)} to $${newPrice.toFixed(2)}.`;
      
      updateBankDisplay(oldBank, bank);
      updatePortfolioDisplay();
      updateExplanation(explanation);
      updateTicker();
      
      // Add XP for every trade (e.g., 10 XP per trade)
      addXP(10);
    });
    
    // ============================================
    // OPTIONS TRADING HANDLER
    // ============================================
    document.getElementById("optionTradeButton").addEventListener("click", function() {
      const action = document.getElementById("optionAction").value;
      const ticker = document.getElementById("optionTeamSelect").value;
      const contracts = parseInt(document.getElementById("optionContracts").value);
      if (contracts <= 0) { alert("Enter a valid number of contracts."); return; }
      
      const currentPrice = teams[ticker].price;
      const strike = currentPrice;
      const premiumPerContract = premiumRate * strike * 100;
      const totalPremium = premiumPerContract * contracts;
      let explanation = "";
      let logMsg = `<strong>Options Trade:</strong> ${action.replace('_', ' ')} on ${teams[ticker].name} (${ticker}) for ${contracts} contract(s).<br>`;
      logMsg += `<em>Strike:</em> $${strike.toFixed(2)} | <em>Premium/Contract:</em> $${premiumPerContract.toFixed(2)} | <em>Total Premium:</em> $${totalPremium.toFixed(2)}<br>`;
      const oldBank = bank;
      
      if (action.startsWith("buy")) {
        if (bank < totalPremium) { alert("Not enough funds for this options trade."); return; }
        bank -= totalPremium;
        logMsg += `Premium paid: -$${totalPremium.toFixed(2)}<br>`;
      } else if (action.startsWith("sell")) {
        bank += totalPremium;
        logMsg += `Premium collected: +$${totalPremium.toFixed(2)}<br>`;
      }
      
      const prevPrice = teams[ticker].price;
      const newPrice = simulatePriceMovement(prevPrice);
      teams[ticker].prevPrice = prevPrice;
      teams[ticker].price = newPrice;
      const pctChange = ((newPrice - prevPrice) / prevPrice) * 100;
      logMsg += `<em>Market Movement:</em> Price moved from $${prevPrice.toFixed(2)} to $${newPrice.toFixed(2)} (${pctChange.toFixed(2)}%)<br>`;
      
      let payoff = 0, cost = 0, profit = 0;
      if (action === "buy_call") {
        const intrinsicValue = Math.max(newPrice - strike, 0);
        payoff = intrinsicValue * 100 * contracts;
        profit = payoff - totalPremium;
        logMsg += `Call Option Payoff: $${payoff.toFixed(2)}<br>`;
        explanation = `You bought a call option on ${teams[ticker].name} (${ticker}) giving you the right to buy at $${strike.toFixed(2)}. With the price at $${newPrice.toFixed(2)}, the option’s value is $${(intrinsicValue * 100 * contracts).toFixed(2)}. Your net result: $${profit.toFixed(2)}.`;
      } else if (action === "buy_put") {
        const intrinsicValue = Math.max(strike - newPrice, 0);
        payoff = intrinsicValue * 100 * contracts;
        profit = payoff - totalPremium;
        logMsg += `Put Option Payoff: $${payoff.toFixed(2)}<br>`;
        explanation = `You bought a put option on ${teams[ticker].name} (${ticker}) giving you the right to sell at $${strike.toFixed(2)}. With the price at $${newPrice.toFixed(2)}, the option’s value is $${(intrinsicValue * 100 * contracts).toFixed(2)}. Your net result: $${profit.toFixed(2)}.`;
      } else if (action === "sell_call") {
        const intrinsicValue = Math.max(newPrice - strike, 0);
        cost = intrinsicValue * 100 * contracts;
        profit = totalPremium - cost;
        logMsg += `Call Option Obligation: $${cost.toFixed(2)}<br>`;
        explanation = `You sold a call option on ${teams[ticker].name} (${ticker}) and received $${totalPremium.toFixed(2)} in premium. With the price at $${newPrice.toFixed(2)}, your cost is $${cost.toFixed(2)}. Net result: $${profit.toFixed(2)}.`;
      } else if (action === "sell_put") {
        const intrinsicValue = Math.max(strike - newPrice, 0);
        cost = intrinsicValue * 100 * contracts;
        profit = totalPremium - cost;
        logMsg += `Put Option Obligation: $${cost.toFixed(2)}<br>`;
        explanation = `You sold a put option on ${teams[ticker].name} (${ticker}) and received $${totalPremium.toFixed(2)} in premium. With the price at $${newPrice.toFixed(2)}, your cost is $${cost.toFixed(2)}. Net result: $${profit.toFixed(2)}.`;
      }
      
      logMsg += `<strong>Net P/L:</strong> $${profit.toFixed(2)}<br>`;
      
      if (action.startsWith("buy")) {
        bank += payoff;
      } else if (action.startsWith("sell")) {
        bank -= cost;
      }
      
      updateBankDisplay(oldBank, bank);
      logOptionsMessage(logMsg);
      updateExplanation(explanation);
      updateTicker();
      updatePortfolioDisplay();
      
      // Add XP for the options trade as well
      addXP(15);
    });
    
    // ============================================
    // Periodic Market Updates
    // ============================================
    setInterval(updateMarketPrices, 5000);
    
    // ============================================
    // Initial Setup on Page Load
    // ============================================
    window.onload = function() {
      updateTicker();
      populateTeamOptions();
      updateLiveMarket();
      updatePortfolioDisplay();
      updateAccountSummary();
      updateBankDisplay(bank, bank);
    }
  </script>
</body>
</html>
