
<!DOCTYPE html>
<html lang="ta">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, initial-scale=1.0">

  <title>Sakhi AI - உங்கள் தோழி</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f2f7f2;
      color: #193c2c;
    }

    header {
      background: #205c40;
      color: white;
      padding: 20px;
      text-align: center;
    }

    header h1 {
      margin: 0 0 6px;
      font-size: 28px;
    }

    header p {
      margin: 0;
      font-size: 14px;
    }

    main {
      width: 92%;
      max-width: 520px;
      margin: 24px auto;
    }

    .card {
      background: white;
      padding: 22px;
      border-radius: 18px;
      box-shadow: 0 4px 18px #183c2c12;
    }

    h2 {
      font-size: 23px;
      margin-top: 0;
    }

    .intro {
      color: #52685a;
      line-height: 1.6;
    }

    label {
      display: block;
      margin: 20px 0 8px;
      font-weight: bold;
    }

    textarea {
      width: 100%;
      min-height: 110px;
      padding: 14px;
      border: 1px solid #cbd9ce;
      border-radius: 12px;
      font-size: 16px;
      font-family: inherit;
      resize: vertical;
    }

    button {
      width: 100%;
      padding: 14px;
      margin-top: 12px;
      border: none;
      border-radius: 12px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    #askBtn {
      background: #205c40;
      color: white;
    }

    #voiceBtn {
      background: #e4f0e7;
      color: #205c40;
      border: 1px solid #b9d3c0;
    }

    #answer {
      display: none;
      margin-top: 20px;
      padding: 16px;
      background: #edf6ef;
      border-radius: 12px;
      line-height: 1.8;
      overflow-wrap: anywhere;
    }

    #officialLink {
      color: #205c40;
      font-weight: bold;
      overflow-wrap: anywhere;
    }

    .note {
      margin-top: 18px;
      color: #627367;
      font-size: 12px;
      line-height: 1.6;
    }

    footer {
      text-align: center;
      padding: 18px;
      color: #627367;
      font-size: 12px;
    }
  </style>
</head>

<body>
  <header>
    <h1>🌿 Sakhi AI</h1>
    <p>உங்கள் தோழி • Your digital companion</p>
  </header>

  <main>
    <section class="card">
      <h2>வணக்கம்! 👋</h2>

      <p class="intro">
        அரசுத் திட்டங்களைப் பற்றி தெரிந்துகொள்ள
        நான் உங்களுக்கு உதவுகிறேன்.
        உங்கள் கேள்வியைத் தமிழில் கேளுங்கள்.
      </p>

      <label for="question">
        உங்கள் கேள்வி என்ன?
      </label>

      <textarea
        id="question"
        placeholder="உதாரணம்: இந்தத் திட்டத்திற்கு எப்படி விண்ணப்பிப்பது?"
      ></textarea>

      <button id="askBtn" onclick="askQuestion()">
        கேள்வியைக் கேளுங்கள்
      </button>

      <button id="voiceBtn" onclick="startVoice()">
        🎤 பேசித் தொடங்குங்கள்
      </button>

      <div id="answer" aria-live="polite"></div>

      <p class="note">
        குறிப்பு: இது ஆரம்பகட்ட மாதிரி.
        விண்ணப்பிக்கும் முன் அதிகாரப்பூர்வ
        அரசுத் தகவல்களைச் சரிபார்க்கவும்.
      </p>
    </section>
  </main>

  <footer>
    Sakhi AI • அனைவருக்கும் எளிய டிஜிட்டல் சேவை
  </footer>

  <script>
    function askQuestion() {
      const question = document
        .getElementById("question")
        .value.trim();

      const answer = document.getElementById("answer");

      if (!question) {
        alert("தயவுசெய்து உங்கள் கேள்வியை எழுதுங்கள்!");
        return;
      }

      answer.style.display = "block";

      answer.textContent =
        "உங்கள் கேள்வி: " + question +
        "\n\nஇது ஆரம்பகட்ட மாதிரி. " +
        "அடுத்த படியில் Gemini AI-ஐ இணைத்து, " +
        "சரிபார்க்கப்பட்ட அரசுத் தகவல்களின் " +
        "அடிப்படையில் பதில் வழங்குவோம்.";
    }

    function startVoice() {
      const SpeechRecognition =
        window.SpeechRecognition ||
        window.webkitSpeechRecognition;

      if (!SpeechRecognition) {
        alert(
          "இந்த browser-ல் voice recognition " +
          "கிடைக்கவில்லை. Chrome-ல் முயற்சிக்கவும்."
        );
        return;
      }

      const recognition = new SpeechRecognition();

      recognition.lang = "ta-IN";
      recognition.interimResults = false;
      recognition.maxAlternatives = 1;

      recognition.onstart = function () {
        document.getElementById("voiceBtn")
          .textContent = "🎤 கேட்கிறேன்...";
      };

      recognition.onresult = function (event) {
        document.getElementById("question").value =
          event.results[0][0].transcript;
      };

      recognition.onerror = function () {
        alert("குரலைப் பதிவு செய்ய முடியவில்லை. மீண்டும் முயற்சிக்கவும்.");
      };

      recognition.onend = function () {
        document.getElementById("voiceBtn")
          .textContent = "🎤 பேசித் தொடங்குங்கள்";
      };

      recognition.start();
    }
  </script>
</body>
</html>
# SAKHI-AI