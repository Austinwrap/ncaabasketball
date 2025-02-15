<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>College Basketball Trading Simulator - CHAOS Edition</title>
  <style>
    /* Base Styles – Dark, edgy, and chaotic */
    body {
      background: linear-gradient(135deg, #1a1a1a, #333);
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 0;
      color: #eee;
      overflow-x: hidden;
    }
    /* Neon Ticker Styles for top, bottom, and news */
    #ticker-top, #ticker-bottom {
      background: #000;
      border: 2px solid #ff0000;
      box-shadow: 0 0 15px #ff0000;
      overflow: hidden;
      padding: 5px 0;
      position: relative;
      z-index: 10;
    }
    .ticker-content {
      white-space: nowrap;
      display: inline-block;
      padding-left: 100%;
      animation: tickerAnimation 15s linear infinite;
      font-size: 1.3em;
    }
    .ticker-content span {
      margin-right: 30px;
      padding: 0 10px;
      animation: neonFlicker 1.5s infinite alternate;
    }
    @keyframes tickerAnimation {
      from { transform: translateX(0); }
      to { transform: translateX(-100%); }
    }
    @keyframes neonFlicker {
      from { text-shadow: 0 0 5px currentColor; }
      to { text-shadow: 0 0 20px currentColor; }
    }
    /* Section Container – common styling for each section */
    .section {
      background: #222;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.6);
      margin: 20px 15px;
      padding: 20px;
    }
    h1, h2, h3 {
      text-align: center;
      color: #ff0000;
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
      border: 1px solid #555;
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
      color: #ccc;
    }
    select, input[type="number"] {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
      border: 1px solid #555;
      border-radius: 4px;
      background: #444;
      color: #eee;
    }
    button {
      width: 100%;
      padding: 10px;
      background: #ff0000;
      color: #fff;
      border: none;
      border-radius: 4px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 10px;
    }
    button:hover {
      background: #cc0000;
    }
    .log, .explanation {
      background: #333;
      border: 1px solid #555;
      border-radius: 6px;
      padding: 10px;
      max-height: 200px;
      overflow-y: auto;
      font-size: 14px;
      margin-top: 10px;
    }
    /* Athlete News Section Styles */
    #athleteNews {
      background: #111;
      border-radius: 10px;
      box-shadow: 0 0 20px #ff0000;
      margin: 20px 15px;
      padding: 15px;
      position: relative;
      overflow: hidden;
    }
    #newsTicker {
      white-space: nowrap;
      display: inline-block;
      padding-left: 100%;
      animation: tickerAnimation 10s linear infinite;
      font-size: 1.2em;
      color: #ffff00;
      font-weight: bold;
    }
    /* Responsive design */
    @media (max-width: 768px) {
      .section { margin: 10px; }
    }
  </style>
</head>
<body>
  <!-- Neon Ticker at Top -->
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
        <!-- Options will be inserted here -->
      </select>
      <label for="teamShares">Number of Shares:</label>
      <input type="number" id="teamShares" min="1" value="1">
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
        <!-- Portfolio rows will be inserted here -->
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
        <!-- Options will be inserted here -->
      </select>
      <label for="optionContracts">Number of Contracts (1 contract = 100 shares):</label>
      <input type="number" id="optionContracts" min="1" value="1">
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
  
  <!-- Neon Ticker at Bottom -->
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

    // 25 College Basketball Teams (Ticker: { name, price, prevPrice })
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

    // Function to update the athlete news ticker every 3 seconds
    function updateNewsTicker() {
      const newsTicker = document.getElementById("newsTicker");
      const randomHeadline = headlines[Math.floor(Math.random() * headlines.length)];
      newsTicker.innerHTML = `<span>${randomHeadline}</span>`;
    }
    setInterval(updateNewsTicker, 3000);

    // ============================================
    // Ticker & Display Updates
    // ============================================
    // Update the neon ticker with team prices and flash colors based on movement.
    function updateTicker() {
      let tickerHTML = "";
      for (const ticker in teams) {
        const team = teams[ticker];
        const change = team.price - team.prevPrice;
        let color;
        if (change > 0) {
          color = "lime";
        } else if (change < 0) {
          color = "red";
        } else {
          color = "#ff0000";
        }
        tickerHTML += `<span style="color:${color};">${ticker} (${team.name}): $${team.price.toFixed(2)}</span>`;
      }
      document.getElementById("tickerTopContent").innerHTML = tickerHTML;
      document.getElementById("tickerBottomContent").innerHTML = tickerHTML;
    }
    
    // Animate bank balance changes (rolling effect)
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
    
    // Update Account Summary: portfolio value, total account value, profit/loss
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
    }
    
    // Update the Live Market table with current prices, change, and percent change.
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
    
    // Update Portfolio Table
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
    
    // Log messages for team trading
    function logTeamMessage(message) {
      const logDiv = document.getElementById("teamLog");
      const p = document.createElement("p");
      p.innerHTML = message;
      logDiv.appendChild(p);
      logDiv.scrollTop = logDiv.scrollHeight;
    }
    
    // Log messages for options trading
    function logOptionsMessage(message) {
      const logDiv = document.getElementById("optionsLog");
      const p = document.createElement("p");
      p.innerHTML = message;
      logDiv.appendChild(p);
      logDiv.scrollTop = logDiv.scrollHeight;
    }
    
    // Update the Trade Explanation sidebar
    function updateExplanation(text) {
      const explanationDiv = document.getElementById("explanation");
      explanationDiv.innerHTML = `<p>${text}</p>`;
    }
    
    // ============================================
    // Simulate Market Price Movements
    // ============================================
    // For the live market, we use smaller fluctuations (±1%)
    function simulatePriceMovement(price) {
      const pctChange = (Math.random() * 0.02) - 0.01;
      const newPrice = price * (1 + pctChange);
      return parseFloat(newPrice.toFixed(2));
    }
    
    // Periodically update market prices every 5 seconds
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
      if (shares <= 0) {
        alert("Enter a valid number of shares.");
        return;
      }
      const price = teams[ticker].price;
      const totalCost = price * shares;
      let explanation = "";
      let oldBank = bank;
      
      if (action === "buy") {
        if (bank < totalCost) {
          alert("Not enough funds to buy.");
          return;
        }
        bank -= totalCost;
        portfolio[ticker] += shares;
        explanation = `You <strong>bought</strong> ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each for $${totalCost.toFixed(2)}. This team is a powerhouse on the court!`;
        logTeamMessage(`Bought ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each. Total cost: $${totalCost.toFixed(2)}.`);
      } else if (action === "sell") {
        if (portfolio[ticker] < shares) {
          alert("You don't own that many shares to sell.");
          return;
        }
        bank += totalCost;
        portfolio[ticker] -= shares;
        explanation = `You <strong>sold</strong> ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each for $${totalCost.toFixed(2)}. Great play!`;
        logTeamMessage(`Sold ${shares} shares of ${teams[ticker].name} (${ticker}) at $${price.toFixed(2)} each. Total gain: $${totalCost.toFixed(2)}.`);
      }
      
      // Simulate a post-trade price movement for the traded team
      const newPrice = simulatePriceMovement(price);
      teams[ticker].prevPrice = teams[ticker].price;
      teams[ticker].price = newPrice;
      explanation += ` After your trade, ${teams[ticker].name} moved from $${price.toFixed(2)} to $${newPrice.toFixed(2)}.`;
      
      updateBankDisplay(oldBank, bank);
      updatePortfolioDisplay();
      updateExplanation(explanation);
      updateTicker();
    });
    
    // ============================================
    // OPTIONS TRADING HANDLER
    // ============================================
    document.getElementById("optionTradeButton").addEventListener("click", function() {
      const action = document.getElementById("optionAction").value;
      const ticker = document.getElementById("optionTeamSelect").value;
      const contracts = parseInt(document.getElementById("optionContracts").value);
      if (contracts <= 0) {
        alert("Enter a valid number of contracts.");
        return;
      }
      
      const currentPrice = teams[ticker].price;
      const strike = currentPrice; // Using current price as the strike
      const premiumPerContract = premiumRate * strike * 100;
      const totalPremium = premiumPerContract * contracts;
      let explanation = "";
      let logMsg = `<strong>Options Trade:</strong> ${action.replace('_', ' ')} on ${teams[ticker].name} (${ticker}) for ${contracts} contract(s).<br>`;
      logMsg += `<em>Strike Price:</em> $${strike.toFixed(2)} | <em>Premium/Contract:</em> $${premiumPerContract.toFixed(2)} | <em>Total Premium:</em> $${totalPremium.toFixed(2)}<br>`;
      let oldBank = bank;
      
      // Process funds for options: buying costs premium; selling collects premium.
      if (action.startsWith("buy")) {
        if (bank < totalPremium) {
          alert("Not enough funds for this options trade.");
          return;
        }
        bank -= totalPremium;
        logMsg += `Premium paid: -$${totalPremium.toFixed(2)}<br>`;
      } else if (action.startsWith("sell")) {
        bank += totalPremium;
        logMsg += `Premium collected: +$${totalPremium.toFixed(2)}<br>`;
      }
      
      // Simulate market movement for the underlying team
      const prevPrice = teams[ticker].price;
      const newPrice = simulatePriceMovement(prevPrice);
      teams[ticker].prevPrice = prevPrice;
      teams[ticker].price = newPrice;
      const pctChange = ((newPrice - prevPrice) / prevPrice) * 100;
      logMsg += `<em>Market Movement:</em> Price moved from $${prevPrice.toFixed(2)} to $${newPrice.toFixed(2)} (${pctChange.toFixed(2)}%)<br>`;
      
      // Calculate options outcome
      let payoff = 0, cost = 0, profit = 0;
      if (action === "buy_call") {
        const intrinsicValue = Math.max(newPrice - strike, 0);
        payoff = intrinsicValue * 100 * contracts;
        profit = payoff - totalPremium;
        logMsg += `Call Option Payoff: $${payoff.toFixed(2)}<br>`;
        explanation = `You <strong>bought a call option</strong> on ${teams[ticker].name} (${ticker}). This gives you the right to buy at $${strike.toFixed(2)}. With the team’s price moving to $${newPrice.toFixed(2)}, the intrinsic value is $${(intrinsicValue * 100 * contracts).toFixed(2)}. After a $${totalPremium.toFixed(2)} premium, your net result is $${profit.toFixed(2)}.`;
      } else if (action === "buy_put") {
        const intrinsicValue = Math.max(strike - newPrice, 0);
        payoff = intrinsicValue * 100 * contracts;
        profit = payoff - totalPremium;
        logMsg += `Put Option Payoff: $${payoff.toFixed(2)}<br>`;
        explanation = `You <strong>bought a put option</strong> on ${teams[ticker].name} (${ticker}). This gives you the right to sell at $${strike.toFixed(2)}. With the price dropping to $${newPrice.toFixed(2)}, the intrinsic value is $${(intrinsicValue * 100 * contracts).toFixed(2)}. After a $${totalPremium.toFixed(2)} premium, your net result is $${profit.toFixed(2)}.`;
      } else if (action === "sell_call") {
        const intrinsicValue = Math.max(newPrice - strike, 0);
        cost = intrinsicValue * 100 * contracts;
        profit = totalPremium - cost;
        logMsg += `Call Option Obligation Cost: $${cost.toFixed(2)}<br>`;
        explanation = `You <strong>sold a call option</strong> on ${teams[ticker].name} (${ticker}). You collected $${totalPremium.toFixed(2)} in premium but must sell at $${strike.toFixed(2)} if exercised. With the price at $${newPrice.toFixed(2)}, your cost is $${cost.toFixed(2)} giving a net of $${profit.toFixed(2)}.`;
      } else if (action === "sell_put") {
        const intrinsicValue = Math.max(strike - newPrice, 0);
        cost = intrinsicValue * 100 * contracts;
        profit = totalPremium - cost;
        logMsg += `Put Option Obligation Cost: $${cost.toFixed(2)}<br>`;
        explanation = `You <strong>sold a put option</strong> on ${teams[ticker].name} (${ticker}). You received a premium of $${totalPremium.toFixed(2)} but must buy at $${strike.toFixed(2)} if exercised. With the price at $${newPrice.toFixed(2)}, your cost is $${cost.toFixed(2)}, netting $${profit.toFixed(2)}.`;
      }
      
      logMsg += `<strong>Net Profit/Loss:</strong> $${profit.toFixed(2)}<br>`;
      
      // Adjust bank based on options outcome.
      if (action === "buy_call" || action === "buy_put") {
        bank += payoff;
      } else if (action === "sell_call" || action === "sell_put") {
        bank -= cost;
      }
      
      updateBankDisplay(oldBank, bank);
      logOptionsMessage(logMsg);
      updateExplanation(explanation);
      updateTicker();
      updatePortfolioDisplay();
    });
    
    // ============================================
    // Periodic Market Updates
    // ============================================
    // Update the simulated live market every 5 seconds
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
