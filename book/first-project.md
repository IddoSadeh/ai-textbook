# First Machine Learning Project

This project uses [P5.js](https://p5js.org/) and [Teachable Machine](https://teachablemachine.withgoogle.com/) to build a simple game. If you do not have any web development background, or are not familiar with p5.js, consider going through the tutorials availabel on the p5js website before attempting this project.

## Part A — Build the tiny game (no AI)

Create `index.html`.

### Step 1: draw a background

Copy this whole file in, then we’ll replace the `<script>` as we go.

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Red Light, Green Light (No AI)</title>
    <style>html, body { margin:0; height:100%; } canvas { display:block; }</style>
  </head>
  <body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.7.0/p5.min.js"></script>
    <script>
      function setup() {
        createCanvas(640, 200);
        textFont('system-ui, sans-serif');
      }
      function draw() {
        background(240);
      }
    </script>
  </body>
</html>
```

### Step 2: draw player and goal zone

Replace the `<script>` with:

```html
<script>
  let x = 20;                 // player x-position
  const y = 140;              // player baseline
  const w = 30, h = 30;       // player size
  const goalStart = 440;      // goal zone
  const goalEnd   = 540;

  function setup() {
    createCanvas(640, 200);
    textFont('system-ui, sans-serif');
  }

  function draw() {
    background(240);

    // goal zone
    noStroke(); fill(190, 240, 200);
    rect(goalStart, 0, goalEnd - goalStart, height);

    // player
    fill(40);
    rect(x, y - h, w, h, 6);

    // HUD
    fill(0); textSize(14);
    text("Goal: stop inside the green zone", 10, 20);
  }
</script>
```

### Step 3: make it move on “G” (go) and stop on “S”

Replace the `<script>`:

```html
<script>
  let x = 20, moving = false;
  const y = 140, w = 30, h = 30, speed = 3;
  const goalStart = 440, goalEnd = 540;

  function setup() {
    createCanvas(640, 200);
    textFont('system-ui, sans-serif');
  }

  function draw() {
    background(240);

    // goal zone
    noStroke(); fill(190, 240, 200);
    rect(goalStart, 0, goalEnd - goalStart, height);

    // move when "going"
    if (moving) x += speed;

    // draw player
    fill(40);
    rect(x, y - h, w, h, 6);

    // HUD
    fill(0); textSize(14);
    text("Press G to GO, S to STOP. Stop inside the green zone.", 10, 20);
  }

  function keyPressed() {
    if (key === 'g' || key === 'G') moving = true;
    if (key === 's' || key === 'S') moving = false;
  }
</script>
```

### Step 4: win/lose and restart (R)

Replace the `<script>`:

```html
<script>
  let x, moving, finished, win;
  const y = 140, w = 30, h = 30, speed = 3;
  const goalStart = 440, goalEnd = 540;

  function resetGame() {
    x = 20; moving = false; finished = false; win = false;
    loop();
  }

  function setup() {
    createCanvas(640, 200);
    textFont('system-ui, sans-serif');
    resetGame();
  }

  function draw() {
    background(240);

    // goal zone
    noStroke(); fill(190, 240, 200);
    rect(goalStart, 0, goalEnd - goalStart, height);

    if (!finished && moving) x += speed;

    // overshoot = lose
    if (!finished && x > width - w) {
      finished = true; win = false; noLoop();
    }

    // player
    fill(40);
    rect(x, y - h, w, h, 6);

    // HUD
    fill(0); textSize(14);
    if (!finished) {
      text("Press G to GO, S to STOP. Stop inside the green zone.", 10, 20);
    } else {
      text(win ? "You WIN! Press R to restart" : "Too far / wrong spot — Press R to try again", 10, 20);
    }
  }

  // Stopping attempts only count when you press S
  function keyPressed() {
    if (key === 'g' || key === 'G') moving = true;
    if (key === 's' || key === 'S') {
      moving = false;
      if (!finished) {
        if (x >= goalStart && x + w <= goalEnd) { finished = true; win = true; noLoop(); }
        else { finished = true; win = false; noLoop(); }
      }
    }
    if (key === 'r' || key === 'R') resetGame();
  }
</script>
```

That’s the whole game. Coding time: tiny.

---

## Part B — Train the AI (2 classes)

Before starting this step, play around with building different models on Teachable Machine. When ready use **Teachable Machine → Image Project**.

1. Make two classes named exactly: `go` and `stop`.
2. For each class, capture \~40–60 webcam snapshots.

   * Use hand signs or colored cards (green = go, palm = stop).
   * Vary distance, angle, lighting, and background.
3. Click **Train Model**.
4. Click **Export Model → Upload (hosted)**.
5. Copy the **model URL** (it ends with a `/`). Keep it open.

---

## Part C — Integrate the AI 

We’ll read the model’s label (`go` or `stop`) and treat **go** like pressing **G**, and a **new stop** like pressing **S**. Keyboard still works.

**Replace your entire `index.html` with this final version**, then paste the model URL.

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Red Light, Green Light + AI</title>
    <style>html, body { margin:0; height:100%; } canvas { display:block; }</style>
  </head>
  <body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.7.0/p5.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest"></script>
    <script>
      // === Paste your Teachable Machine model URL (must end with /) ===
      const MODEL_URL = "https://teachablemachine.withgoogle.com/models/REPLACE_ME/";

      // === Game state ===
      let x, moving, finished, win;
      const y = 140, w = 30, h = 30, speed = 3;
      const goalStart = 440, goalEnd = 540;

      // === AI state ===
      let model = null, video = null;
      let aiLabel = "idle", lastAiLabel = "idle"; // edge-detect 'stop'
      let aiEnabled = true; // flip to false if you want to demo keyboard-only

      function resetGame() {
        x = 20; moving = false; finished = false; win = false;
        loop();
      }

      function setup() {
        createCanvas(640, 200);
        textFont('system-ui, sans-serif');
        resetGame();

        // webcam for the classifier (hidden DOM video element)
        video = createCapture(VIDEO);
        video.size(320, 240);
        video.hide();

        // load model WITHOUT async/await
        tmImage.load(MODEL_URL + "model.json", MODEL_URL + "metadata.json")
          .then(m => { model = m; startClassifyLoop(); })
          .catch(err => console.error("Model load failed:", err));
      }

      function startClassifyLoop() {
        // check prediction ~6-7 times/sec to keep it stable for kids
        setInterval(function () {
          if (!model || !video) return;
          model.predict(video.elt).then(preds => {
            preds.sort((a,b) => b.probability - a.probability);
            aiLabel = preds[0].className.toLowerCase(); // 'go' or 'stop'
          }).catch(err => console.error("Predict error:", err));
        }, 150);
      }

      function draw() {
        background(240);

        // goal zone
        noStroke(); fill(190, 240, 200);
        rect(goalStart, 0, goalEnd - goalStart, height);

        // AI → controls (edge-detect stop)
        if (aiEnabled && !finished) {
          if (aiLabel === 'go') moving = true;
          if (aiLabel === 'stop' && lastAiLabel !== 'stop') {
            // treat a new 'stop' as pressing S once
            moving = false;
            if (x >= goalStart && x + w <= goalEnd) { finished = true; win = true; noLoop(); }
            else { finished = true; win = false; noLoop(); }
          }
          lastAiLabel = aiLabel;
        }

        if (!finished && moving) x += speed;

        // overshoot = lose
        if (!finished && x > width - w) {
          finished = true; win = false; noLoop();
        }

        // player
        fill(40); rect(x, y - h, w, h, 6);

        // HUD
        fill(0); textSize(14);
        if (!finished) {
          text("Press G to GO, S to STOP. Goal: stop in the green zone.", 10, 20);
          text("AI Label: " + aiLabel, 10, 40);
          // webcam preview (tiny)
          image(video, 10, 60, 120, 90);
        } else {
          text(win ? "You WIN! Press R to restart" : "Too far / wrong spot — Press R to try again", 10, 20);
          text("AI Label: " + aiLabel, 10, 40);
          image(video, 10, 60, 120, 90);
        }
      }

      // Keyboard stays as a fallback and for demos
      function keyPressed() {
        if (key === 'g' || key === 'G') moving = true;
        if (key === 's' || key === 'S') {
          moving = false;
          if (!finished) {
            if (x >= goalStart && x + w <= goalEnd) { finished = true; win = true; noLoop(); }
            else { finished = true; win = false; noLoop(); }
          }
        }
        if (key === 'r' || key === 'R') resetGame();
      }
    </script>
  </body>
</html>
```
