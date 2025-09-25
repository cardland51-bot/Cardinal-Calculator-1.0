<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap" rel="stylesheet">
<style>
  body {
    font-family: 'Montserrat', sans-serif;
    background: #f8f7f6;
    margin: 0;
    padding: 0;
    color: #333;
  }
  .container {
    max-width: 800px;
    margin: 40px auto;
    background: #fffdfc;
    border-radius: 20px;
    box-shadow: 0 12px 24px rgba(0,0,0,0.12);
    padding: 30px 40px;
  }
  h1 {
    text-align: center;
    color: #800000;
    font-weight: 700;
    margin-bottom: 30px;
  }
  .step {
    display: none;
    transition: opacity 0.5s ease;
  }
  .step.active {
    display: block;
    opacity: 1;
  }
  .progress-bar {
    height: 12px;
    background: #eee;
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 30px;
  }
  .progress {
    background: linear-gradient(90deg, #800000, #a00000);
    height: 100%;
    width: 0%;
    transition: width 0.5s ease-in-out;
    box-shadow: 0 2px 8px rgba(128,0,0,0.4);
  }
  .question {
    margin-bottom: 25px;
    font-size: 1.1rem;
  }
  .options {
    display: flex;
    flex-direction: column;
  }
  .option {
    background: linear-gradient(90deg, #fff 0%, #fdfcfb 100%);
    border-radius: 12px;
    padding: 12px 20px;
    margin-bottom: 10px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 8px rgba(0,0,0,0.05);
  }
  .option:hover {
    box-shadow: 0 6px 15px rgba(128,0,0,0.4);
    transform: translateY(-2px);
  }
  .option.selected {
    background: rgba(128,0,0,0.1);
    box-shadow: 0 6px 15px rgba(128,0,0,0.5);
  }
  button {
    background: #800000;
    color: #fff;
    border: none;
    padding: 12px 25px;
    border-radius: 12px;
    cursor: pointer;
    font-weight: 600;
    font-size: 1rem;
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    transition: transform 0.2s, box-shadow 0.2s;
    margin-top: 20px;
  }
  button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(0,0,0,0.3);
  }
  .additional-info {
    margin-top: 15px;
  }
  textarea {
    width: 100%;
    min-height: 100px;
    border-radius: 12px;
    border: 1px solid #ccc;
    padding: 12px;
    resize: vertical;
  }
  .disclaimer {
    font-size: 0.85rem;
    color: #888;
    text-align: center;
    margin-top: 30px;
  }
  input[type="file"] {
    margin-top: 10px;
  }
</style>
</head>
<body>
<div class="container">
  <h1>Cardinal Landscaping Price Calculator</h1>
  
  <div class="progress-bar">
    <div class="progress" id="progress"></div>
  </div>

  <!-- Step 1: First-time / Recurring -->
  <div class="step active" id="step1">
    <div class="question">Are you a first-time or recurring customer?</div>
    <div class="options">
      <div class="option" onclick="selectOption(this, 'first-time')">First-time</div>
      <div class="option" onclick="selectOption(this, 'recurring')">Recurring</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 2: Package Size -->
  <div class="step" id="step2">
    <div class="question">Select your package size</div>
    <div class="options">
      <div class="option" onclick="selectOption(this,'tiny')">Tiny (Front bed only)</div>
      <div class="option" onclick="selectOption(this,'small')">Small (Front bed + 1-2 island/corner beds)</div>
      <div class="option" onclick="selectOption(this,'medium')">Medium (Front beds, side beds, small back of hoise beds or island beds beds)</div>
      <div class="option" onclick="selectOption(this,'large')">Large (multiple front beds, side beds, back beds, some island beds)</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 3: Mulch -->
  <div class="step" id="step3">
    <div class="question">Do you want mulch?</div>
    <div class="options">
      <div class="option" onclick="selectOption(this,'mulch-yes')">Yes</div>
      <div class="option" onclick="selectOption(this,'mulch-no')">No</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 4: Weeds (shown if mulch yes) -->
  <div class="step" id="step4">
    <div class="question">How extensive are the weeds?</div>
    <div class="options">
      <div class="option" onclick="selectOption(this,'slight')">Slight</div>
      <div class="option" onclick="selectOption(this,'moderate')">Moderate</div>
      <div class="option" onclick="selectOption(this,'heavy')">Heavy</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 5: Overgrowth -->
  <div class="step" id="step5">
    <div class="question">Shrubs overgrowth severity:</div>
    <div class="options">
      <div class="option" onclick="selectOption(this,'slightly-overgrown')">Slightly Overgrown</div>
      <div class="option" onclick="selectOption(this,'moderately-overgrown')">Moderately Overgrown (+15%)</div>
      <div class="option" onclick="selectOption(this,'very-overgrown')">Very Overgrown (+35%)</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 6: Trimming >10ft -->
  <div class="step" id="step6">
    <div class="question">Any shrubs over 10 ft tall?</div>
    <div class="options">
      <div class="option" onclick="selectOption(this,'yes-tall')">Yes (+Dynamic Pricing)</div>
      <div class="option" onclick="selectOption(this,'no-tall')">No</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 7: Attention to Detail -->
  <div class="step" id="step7">
    <div class="question">Attention to Detail</div>
    <div class="options">
      <div class="option" onclick="selectOption(this,'normal-detail')">Normal</div>
      <div class="option" onclick="selectOption(this,'high-detail')">Premium</div>
    </div>
    <button onclick="nextStep()">Next</button>
  </div>

  <!-- Step 8: Additional Info / Photos -->
  <div class="step" id="step8">
    <div class="question">Additional details / scope of work (optional)</div>
    <textarea id="additional-info" placeholder="Type any extra notes here..."></textarea>
    <input type="file" id="photos" multiple>
    <button onclick="nextStep()">See Price</button>
  </div>

  <!-- Step 9: Price Display -->
  <div class="step" id="step9">
    <div class="question">Your Estimated Price</div>
    <div id="final-price" style="font-size:1.8rem; color:#800000; font-weight:700;"></div>
    <div class="disclaimer">All pricing estimates are accurate within ±15%.</div>
  </div>
</div>

<script>
let currentStep = 1;
let selections = {};
const maxPrice = {tiny:550, small:950, medium:1850, large:2900};
const minPrice = {tiny:250, small:450, medium:950, large:1200};

function selectOption(el, value) {
  const options = el.parentNode.querySelectorAll('.option');
  options.forEach(o=>o.classList.remove('selected'));
  el.classList.add('selected');
  selections[el.parentNode.parentNode.id] = value;
  updateDynamicPrice();
}

function nextStep() {
  const step = document.getElementById(`step${currentStep}`);
  step.classList.remove('active');
  currentStep++;
  const next = document.getElementById(`step${currentStep}`);
  if(next) next.classList.add('active');
  updateProgress();
}

function updateProgress() {
  const progress = document.getElementById('progress');
  progress.style.width = ((currentStep-1)/8*100) + '%';
}

function updateDynamicPrice() {
  let base = 0;
  if(selections['step2']){
    const pkg = selections['step2'];
    base = minPrice[pkg];
    // Mulch weed adjustment
    if(selections['step4']){
      if(selections['step4']==='moderate') base *=1.25;
      if(selections['step4']==='heavy') base *=1.5;
    }
    // Overgrowth
    if(selections['step5']){
      if(selections['step5']==='moderately-overgrown') base *=1.15;
      if(selections['step5']==='very-overgrown') base *=1.35;
    }
    // Attention to detail
    if(selections['step7']){
      if(selections['step7']==='normal-detail') base = Math.min(base*1.6, maxPrice[pkg]*0.8);
      if(selections['step7']==='high-detail') base = Math.min(base*1.9, maxPrice[pkg]);
    }
    // Recurring customer discount internally
    if(selections['step1']==='recurring') base *=0.95;
  }
  document.getElementById('final-price').innerText = `$${base.toFixed(0)}`;
}
</script>
</body>
</html>
