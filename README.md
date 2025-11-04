<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Study Helper</title>
 <style>/* ----------------- General Styles ----------------- */
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');

body {
  margin: 0;
  font-family: 'Orbitron', sans-serif;
  background: #0f0c29; /* Dark gradient base */
  background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
  color: #fff;
  transition: background 0.3s ease, color 0.3s ease;
}

.app-wrapper {
  max-width: 1200px;
  margin: auto;
  padding: 20px;
}

/* ----------------- Password Overlay ----------------- */
.password-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(15,12,41,0.95);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.password-box {
  background: #1f1b4d;
  padding: 30px;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 0 30px #ff0080, 0 0 60px #7928ca;
}

.password-box input {
  padding: 12px;
  border-radius: 10px;
  border: none;
  margin-top: 15px;
  width: 200px;
  text-align: center;
}

.password-box button {
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  background: linear-gradient(90deg, #ff0080, #7928ca);
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

.password-box button:hover {
  filter: brightness(1.2);
}

.password-box p {
  margin-top: 10px;
  color: #ff5555;
}

/* ----------------- Header ----------------- */
.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
}

.app-header h1 {
  margin: 0;
  font-size: 2.5rem;
  background: linear-gradient(90deg, #ff0080, #7928ca);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.app-header p {
  margin: 0;
  color: #bbb;
}

.theme-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  background: #ff0080;
  color: #fff;
  cursor: pointer;
  transition: 0.3s;
}

.theme-btn:hover {
  filter: brightness(1.2);
}

/* ----------------- Tabs Navigation ----------------- */
.subject-nav {
  display: flex;
  gap: 10px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}

.subject-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 15px;
  background: #292657;
  color: #fff;
  cursor: pointer;
  transition: 0.3s;
  font-weight: bold;
  text-transform: uppercase;
}

.subject-btn.active,
.subject-btn:hover {
  background: linear-gradient(90deg, #ff0080, #7928ca);
  box-shadow: 0 0 10px #ff0080, 0 0 20px #7928ca;
}

/* ----------------- Tabs Content ----------------- */
.tab-content {
  display: none;
  gap: 20px;
}

.tab-content.active {
  display: flex;
  flex-direction: column;
}

/* ----------------- Input & Output Cards ----------------- */
.input-card, .output-card, .flashcards-card {
  background: #1f1b4d;
  padding: 20px;
  border-radius: 15px;
  margin-bottom: 20px;
  box-shadow: 0 0 20px rgba(255,0,128,0.3);
  transition: transform 0.3s;
}

.input-card:hover, .output-card:hover, .flashcards-card:hover {
  transform: translateY(-5px);
}

.input-card h2, .output-card h2, .flashcards-card h2 {
  margin-top: 0;
  margin-bottom: 15px;
  color: #ff77c9;
}

/* ----------------- Textarea ----------------- */
textarea {
  width: 100%;
  padding: 15px;
  border-radius: 10px;
  border: none;
  resize: none;
  font-family: 'Orbitron', sans-serif;
  font-size: 1rem;
  background: #292657;
  color: #fff;
  margin-bottom: 15px;
}

/* ----------------- Buttons ----------------- */
.ai-btn, #add-flashcard, #generate-flashcards, .voice-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  background: linear-gradient(90deg, #ff0080, #7928ca);
  color: #fff;
  cursor: pointer;
  transition: 0.3s;
  margin-right: 10px;
}

.ai-btn:hover, #add-flashcard:hover, #generate-flashcards:hover, .voice-btn:hover {
  filter: brightness(1.2);
}

/* ----------------- Voice Button ----------------- */
.voice-controls {
  margin-bottom: 10px;
}

/* ----------------- Flashcards ----------------- */
.flashcards-scroll {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  max-height: 400px;
  overflow-y: auto;
}

.flashcard {
  background: #292657;
  padding: 15px 20px;
  border-radius: 12px;
  cursor: pointer;
  flex: 1 0 120px;
  text-align: center;
  transition: 0.3s;
  box-shadow: 0 0 10px rgba(255,0,128,0.3);
}

.flashcard.flipped {
  background: #ff0080;
  color: #fff;
  transform: rotateY(180deg);
}

/* ----------------- Footer ----------------- */
.app-footer {
  text-align: center;
  margin-top: 50px;
  color: #aaa;
}

/* ----------------- Dark Mode ----------------- */
body.dark {
  background: #111;
  color: #ddd;
}

body.dark .input-card, body.dark .output-card, body.dark .flashcards-card {
  background: #222;
}

body.dark .subject-btn {
  background: #333366;
}

body.dark .subject-btn.active, body.dark .subject-btn:hover {
  background: linear-gradient(90deg, #ff0080, #ff77c9);
}
</style>
</head>
<body>
  <div class="app-wrapper">

    <!-- Header -->
    <header class="app-header">
      <div>
        <h1>AI Study Helper</h1>
        <p>Get answers instantly, talk to AI, and create flashcards!</p>
      </div>
      <button class="theme-btn">🌙 Dark Mode</button>
    </header>

    <!-- Subject Navigation -->
    <nav class="subject-nav">
      <button class="subject-btn active">Math</button>
      <button class="subject-btn">Science</button>
      <button class="subject-btn">History</button>
      <button class="subject-btn">Languages</button>
      <button class="subject-btn">Flashcards</button>
    </nav>

    <!-- Tabs -->
    <!-- Math Tab -->
    <section class="tab-content active">
      <div class="input-card">
        <h2>Math AI Helper</h2>
        <textarea placeholder="Type a math question..."></textarea>
        <div class="btn-group">
          <button class="ai-btn">Get Answer</button>
          <button class="voice-btn">🎤 Speak</button>
        </div>
      </div>
      <div class="output-card">
        <h2>Answer</h2>
        <div class="ai-output"></div>
      </div>
    </section>

    <!-- Science Tab -->
    <section class="tab-content">
      <div class="input-card">
        <h2>Science AI Helper</h2>
        <textarea placeholder="Type a science question..."></textarea>
        <div class="btn-group">
          <button class="ai-btn">Get Answer</button>
          <button class="voice-btn">🎤 Speak</button>
        </div>
      </div>
      <div class="output-card">
        <h2>Answer</h2>
        <div class="ai-output"></div>
      </div>
    </section>

    <!-- History Tab -->
    <section class="tab-content">
      <div class="input-card">
        <h2>History AI Helper</h2>
        <textarea placeholder="Type a history question..."></textarea>
        <div class="btn-group">
          <button class="ai-btn">Get Answer</button>
          <button class="voice-btn">🎤 Speak</button>
        </div>
      </div>
      <div class="output-card">
        <h2>Answer</h2>
        <div class="ai-output"></div>
      </div>
    </section>

    <!-- Languages Tab -->
    <section class="tab-content">
      <div class="input-card">
        <h2>Language AI Helper</h2>
        <textarea placeholder="Type a language question..."></textarea>
        <div class="btn-group">
          <button class="ai-btn">Get Answer</button>
          <button class="voice-btn">🎤 Speak</button>
        </div>
      </div>
      <div class="output-card">
        <h2>Answer</h2>
        <div class="ai-output"></div>
      </div>
    </section>

    <!-- Flashcards Tab -->
    <section class="tab-content">
      <div class="flashcards-card">
        <h2>Flashcards</h2>
        <div class="flashcard-input-group">
          <input type="text" id="flashcard-input" placeholder="Enter flashcard text">
          <button id="add-flashcard">Add</button>
        </div>
        <div class="flashcards-scroll"></div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="app-footer">
      &copy; 2025 AI Study Helper
    </footer>

  </div>

  <script>// ----------------- Subject Tabs -----------------
const subjectButtons = document.querySelectorAll(".subject-btn");
const tabContents = document.querySelectorAll(".tab-content");

subjectButtons.forEach((btn, index) => {
  btn.addEventListener("click", () => {
    subjectButtons.forEach(b => b.classList.remove("active"));
    tabContents.forEach(t => t.classList.remove("active"));
    btn.classList.add("active");
    tabContents[index].classList.add("active");
  });
});

// ----------------- Dark Mode -----------------
const themeBtn = document.querySelector(".theme-btn");
themeBtn.addEventListener("click", () => {
  document.body.classList.toggle("dark");
  themeBtn.textContent = document.body.classList.contains("dark")
    ? "☀️ Light Mode"
    : "🌙 Dark Mode";
});

// ----------------- AI Study Helper -----------------
const OPENAI_API_KEY = "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"; // 🔒 Replace with your API key

const sections = document.querySelectorAll(".tab-content");
sections.forEach(section => {
  const input = section.querySelector("textarea");
  const btn = section.querySelector("button");
  const output = section.querySelector(".ai-output");
  const voiceBtn = section.querySelector(".voice-btn"); // optional voice button

  if (!input || !btn || !output) return;

  // Fetch AI Answer
  const fetchAIAnswer = async (prompt) => {
    try {
      output.textContent = "Thinking... 🤖";

      const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${OPENAI_API_KEY}`,
        },
        body: JSON.stringify({
          model: "gpt-4",
          messages: [{ role: "user", content: prompt }],
          max_tokens: 2000,
          temperature: 0.7,
        }),
      });

      const data = await response.json();
      if (data.error) throw new Error(data.error.message);

      output.textContent = data.choices?.[0]?.message?.content || "No response found.";
    } catch (err) {
      output.textContent = "Error: " + err.message;
      console.error(err);
    }
  };

  // Button click
  btn.addEventListener("click", () => {
    const prompt = input.value.trim();
    if (!prompt) {
      output.textContent = "Please type a question!";
      return;
    }
    fetchAIAnswer(prompt);
  });

  // Enter key triggers AI helper
  input.addEventListener("keydown", e => {
    if (e.key === "Enter" && !e.shiftKey) {
      e.preventDefault();
      btn.click();
    }
  });

  // ----------------- Voice Command -----------------
  if (voiceBtn && "webkitSpeechRecognition" in window) {
    const recognition = new webkitSpeechRecognition();
    recognition.continuous = false;
    recognition.interimResults = false;
    recognition.lang = "en-US";

    voiceBtn.addEventListener("click", () => {
      recognition.start();
    });

    recognition.onresult = (event) => {
      const transcript = event.results[0][0].transcript;
      input.value = transcript;
      fetchAIAnswer(transcript);
    };

    recognition.onerror = (event) => {
      console.error("Speech recognition error:", event.error);
    };
  }
});

// ----------------- Flashcards Tab -----------------
const flashcardContainer = document.querySelector(".flashcards-scroll");
const flashcardInput = document.getElementById("flashcard-input");
const flashcardAddBtn = document.getElementById("add-flashcard");

const loadFlashcards = () => {
  const saved = JSON.parse(localStorage.getItem("flashcards") || "[]");
  flashcardContainer.innerHTML = "";
  saved.forEach(text => createFlashcard(text, false));
};

const createFlashcard = (text, save = true) => {
  const card = document.createElement("div");
  card.classList.add("flashcard");
  card.textContent = text;

  card.addEventListener("click", () => {
    card.classList.toggle("flipped");
    card.textContent = card.classList.contains("flipped") ? "❓" : text;
  });

  flashcardContainer.appendChild(card);

  if (save) {
    const saved = JSON.parse(localStorage.getItem("flashcards") || "[]");
    saved.push(text);
    localStorage.setItem("flashcards", JSON.stringify(saved));
  }
};

flashcardAddBtn.addEventListener("click", () => {
  const text = flashcardInput.value.trim();
  if (!text) return;
  createFlashcard(text);
  flashcardInput.value = "";
});

loadFlashcards();
</script>
</body>
</html>
