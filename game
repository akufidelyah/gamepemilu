<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Game Proses Legislasi SMP</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Comic+Sans+MS&display=swap');
  body {
    background: linear-gradient(135deg, #f6d365, #fda085);
    font-family: 'Comic Sans MS', cursive, sans-serif;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    min-height: 100vh;
  }
  #game-container {
    background: #fff8dccc;
    padding: 20px 30px;
    border-radius: 20px;
    box-shadow: 0 6px 20px rgba(0,0,0,0.3);
    width: 420px;
    max-width: 90vw;
    text-align: center;
    margin-top: 40px;
  }
  h1 {
    color: #e65100;
    font-weight: 700;
    margin-bottom: 15px;
    letter-spacing: 1.5px;
  }
  #question {
    font-size: 1.3rem;
    margin-bottom: 15px;
    color: #bf360c;
    min-height: 70px;
  }
  #image-container {
    height: 180px;
    margin-bottom: 20px;
    overflow: hidden;
  }
  #image-container img {
    max-height: 100%;
    max-width: 100%;
    border-radius: 15px;
    transition: transform 0.7s ease;
  }
  .option-btn {
    display: block;
    background-color: #ffcc80;
    border: 3px solid #ffb300;
    padding: 14px 25px;
    margin: 10px 0;
    border-radius: 15px;
    cursor: pointer;
    transition: background-color 0.3s ease, border-color 0.3s ease, transform 0.3s ease;
    color: #4e342e;
    font-weight: 700;
    font-size: 1.1rem;
    box-shadow: 2px 2px 5px #ba6b1d;
  }
  .option-btn:hover {
    background-color: #ffb300;
    color: white;
    border-color: #bf360c;
    transform: scale(1.03);
  }
  .correct {
    background-color: #a5d6a7 !important;
    border-color: #2e7d32 !important;
    color: #1b5e20 !important;
    box-shadow: 0px 0px 10px 2px #2e7d32;
  }
  .wrong {
    background-color: #ef9a9a !important;
    border-color: #c62828 !important;
    color: #b71c1c !important;
    box-shadow: 0px 0px 10px 2px #c62828;
  }
  #progress-bar {
    height: 14px;
    background: #ffd54f;
    border-radius: 20px;
    overflow: hidden;
    margin-bottom: 25px;
    box-shadow: inset 0 2px 5px rgba(0,0,0,0.2);
  }
  #progress {
    height: 100%;
    width: 0%;
    background-color: #f57f17;
    transition: width 0.5s ease;
  }
  #score-container {
    font-size: 1.4rem;
    margin-top: 15px;
    color: #bf360c;
    font-weight: 700;
  }
  #next-btn {
    margin-top: 18px;
    padding: 13px 30px;
    font-size: 1.2rem;
    font-weight: 700;
    color: white;
    background-color: #e65100;
    border: none;
    border-radius: 18px;
    cursor: pointer;
    display: none;
    box-shadow: 0 4px 15px rgba(230, 81, 0, 0.7);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
  }
  #next-btn:hover {
    background-color: #bf360c;
    box-shadow: 0 6px 20px rgba(191, 54, 12, 0.9);
  }
</style>
</head>
<body>
<div id="game-container">
  <h1>Game Proses Legislasi SMP</h1>
  <div id="progress-bar">
    <div id="progress"></div>
  </div>
  <div id="image-container"><img src="" alt="Ilustrasi Proses Legislasi" id="illustration"></div>
  <div id="question">Memuat pertanyaan ...</div>
  <div id="options-container"></div>
  <button id="next-btn">Soal Berikutnya</button>
  <div id="score-container"></div>
</div>

<script>
  const questions = [
    {
      question: "Apa tahapan pertama dalam proses legislasi?",
      options: ["Pembahasan di DPR", "Penyusunan RUU", "Pengesahan Presiden", "Pengumuman kepada publik"],
      answer: "Penyusunan RUU",
      image: "https://i.imgur.com/XLbNrT5.png"  // ilustrasi dokumen, bisa diganti dengan url lain
    },
    {
      question: "Siapa yang menyusun Rancangan Undang-Undang (RUU)?",
      options: ["Presiden", "DPR", "Mahkamah Konstitusi", "Masyarakat"],
      answer: "DPR",
      image: "https://i.imgur.com/K3zHzTb.png"  // ilustrasi DPR sidang
    },
    {
      question: "Setelah DPR menyetujui RUU, apa tahap berikutnya?",
      options: ["Pengesahan Presiden", "Pembacaan pertama", "Sidang pleno MPR", "Putusan Mahkamah"],
      answer: "Pengesahan Presiden",
      image: "https://i.imgur.com/LUy0Yns.png"  // ilustrasi palu sidang presiden
    },
    {
      question: "Apa yang terjadi jika Presiden menolak RUU?",
      options: ["RUU batal", "RUU direvisi dan dibahas ulang", "Langsung jadi UU", "DPR dibubarkan"],
      answer: "RUU direvisi dan dibahas ulang",
      image: "https://i.imgur.com/1cmmIT0.png"  // ilustrasi revisi dokumen
    }
  ];

  let currentQuestionIndex = 0;
  let score = 0;
  const totalQuestions = questions.length;
  const questionEl = document.getElementById('question');
  const optionsContainer = document.getElementById('options-container');
  const nextBtn = document.getElementById('next-btn');
  const scoreContainer = document.getElementById('score-container');
  const progressBar = document.getElementById('progress');
  const illustration = document.getElementById('illustration');

  function loadQuestion() {
    clearState();
    let q = questions[currentQuestionIndex];
    questionEl.textContent = q.question;
    // Load image with fade-in animation
    illustration.style.opacity = 0;
    illustration.src = q.image;
    setTimeout(() => {
      illustration.style.opacity = 1;
      illustration.style.transform = "scale(1.05)";
      setTimeout(() => illustration.style.transform = "scale(1)", 400);
    }, 100);

    q.options.forEach(option => {
      const button = document.createElement('button');
      button.textContent = option;
      button.classList.add('option-btn');
      button.onclick = selectAnswer;
      optionsContainer.appendChild(button);
    });

    updateProgress();
  }

  function clearState() {
    nextBtn.style.display = 'none';
    scoreContainer.textContent = '';
    while(optionsContainer.firstChild){
      optionsContainer.removeChild(optionsContainer.firstChild);
    }
  }

  function selectAnswer(e) {
    const selectedBtn = e.target;
    const answer = questions[currentQuestionIndex].answer;
    const isCorrect = selectedBtn.textContent === answer;

    if (isCorrect) {
      selectedBtn.classList.add('correct');
      score++;
    } else {
      selectedBtn.classList.add('wrong');
      // Highlight correct answer
      Array.from(optionsContainer.children).forEach(button => {
        if(button.textContent === answer){
          button.classList.add('correct');
        }
      });
    }

    // Disable all buttons after answer selected
    Array.from(optionsContainer.children).forEach(button => {
      button.disabled = true;
    });

    nextBtn.style.display = 'inline-block';
  }

  nextBtn.onclick = () => {
    currentQuestionIndex++;
    if(currentQuestionIndex < totalQuestions){
      loadQuestion();
    } else {
      showScore();
    }
  };

  function updateProgress() {
    const progressPercent = ((currentQuestionIndex) / totalQuestions) * 100;
    progressBar.style.width = progressPercent + '%';
  }

  function showScore() {
    clearState();
    questionEl.textContent = "Game selesai!";
    scoreContainer.textContent = `Skor Anda: ${score} dari ${totalQuestions}`;
    progressBar.style.width = '100%';
    illustration.style.opacity = 1;
    illustration.style.transform = "scale(1)";
    illustration.src = "https://i.imgur.com/tOPBdoz.png"; // gambar selamat atau piala
  }

  loadQuestion();
</script>
</body>
</html>
