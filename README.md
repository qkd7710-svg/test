<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>나의 봉사 성향 테스트</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      font-family:
        Pretendard,
        "Noto Sans KR",
        "Apple SD Gothic Neo",
        "Malgun Gothic",
        sans-serif;
      background: #f5f7fb;
      color: #1f3d5a;
    }

    button,
    input {
      font: inherit;
    }

    button {
      cursor: pointer;
    }

    .container {
      width: min(92%, 720px);
      margin: 0 auto;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 30px 0;
    }

    .screen {
      display: none;
      width: 100%;
    }

    .screen.active {
      display: block;
    }

    .card {
      background: #ffffff;
      border-radius: 28px;
      padding: 38px 30px;
      box-shadow: 0 18px 50px rgba(0, 0, 0, 0.08);
    }

    /* 시작 화면 */

    .start-card {
      text-align: center;
    }

    .small-title {
      display: inline-block;
      padding: 7px 13px;
      border-radius: 999px;
      background: #eaf4ff;
      color: #3a83ca;
      font-size: 13px;
      font-weight: 800;
      letter-spacing: 1px;
    }

    h1 {
      margin: 17px 0 12px;
      font-size: 40px;
      letter-spacing: -2px;
    }

    .intro {
      color: #6f7c89;
      line-height: 1.7;
      margin-bottom: 26px;
    }

    .type-list {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 28px;
      text-align: left;
    }

    .type-list div {
      padding: 12px 14px;
      border-radius: 14px;
      background: #f8fafc;
      border: 1px solid #e5ebf1;
      font-size: 14px;
      font-weight: 700;
    }

    .type-list div:last-child {
      grid-column: 1 / -1;
    }

    .name-label {
      display: block;
      text-align: left;
      font-weight: 800;
      margin-bottom: 8px;
    }

    .name-input {
      width: 100%;
      height: 52px;
      border-radius: 14px;
      border: 1.5px solid #dce4ec;
      padding: 0 15px;
      outline: none;
    }

    .name-input:focus {
      border-color: #4a95db;
    }

    .main-btn {
      width: 100%;
      height: 54px;
      border: none;
      border-radius: 15px;
      margin-top: 16px;
      background: #438fd5;
      color: white;
      font-weight: 900;
      font-size: 16px;
    }

    .notice {
      margin-top: 15px;
      font-size: 13px;
      color: #929ba5;
    }

    /* 질문 화면 */

    .quiz-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .back-btn {
      border: none;
      background: none;
      color: #6d7883;
      font-weight: 800;
    }

    .counter {
      font-size: 14px;
      font-weight: 800;
      color: #77818c;
    }

    .progress {
      margin-top: 16px;
      width: 100%;
      height: 8px;
      background: #ebeff4;
      border-radius: 999px;
      overflow: hidden;
    }

    .progress-bar {
      height: 100%;
      width: 10%;
      background: #53a0dd;
      transition: width 0.25s;
    }

    .question-box {
      padding: 36px 0 24px;
    }

    .question-number {
      margin: 0 0 8px;
      color: #4187c9;
      font-size: 13px;
      font-weight: 900;
    }

    .question-text {
      margin: 0;
      line-height: 1.5;
      font-size: 26px;
      letter-spacing: -1px;
    }

    .answer-list {
      display: grid;
      gap: 11px;
    }

    .answer-btn {
      width: 100%;
      min-height: 64px;
      display: flex;
      gap: 12px;
      align-items: center;
      padding: 14px;
      border-radius: 16px;
      border: 1.5px solid #e1e7ed;
      background: white;
      text-align: left;
      color: #253f59;
    }

    .answer-btn:hover {
      background: #f7fbff;
      border-color: #83b8e5;
    }

    .answer-letter {
      flex: 0 0 34px;
      width: 34px;
      height: 34px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 50%;
      background: #eaf4fd;
      color: #347fc4;
      font-weight: 900;
    }

    /* 결과 */

    .result-top {
      text-align: center;
      margin-bottom: 15px;
      font-weight: 800;
      color: #7a8590;
    }

    .result-card {
      padding: 30px;
      border-radius: 24px;
      border: 2px solid #ffc5d1;
      background: white;
    }

    .result-icon {
      width: 68px;
      height: 68px;
      border-radius: 20px;
      background: #fff0f4;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 33px;
    }

    .result-label {
      margin: 22px 0 4px;
      font-weight: 900;
    }

    .result-title {
      margin: 0;
      font-size: 38px;
      letter-spacing: -2px;
    }

    .result-tagline {
      font-size: 17px;
      font-weight: 800;
      line-height: 1.6;
    }

    .result-description {
      color: #65717d;
      line-height: 1.8;
    }

    .result-section {
      border-top: 1px dashed #d9dfe5;
      margin-top: 22px;
      padding-top: 18px;
    }

    .result-section h3 {
      margin: 0 0 12px;
      font-size: 15px;
    }

    .tag-box {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .tag {
      padding: 8px 10px;
      border-radius: 999px;
      font-size: 13px;
      font-weight: 800;
    }

    .result-message {
      margin-top: 22px;
      background: #f8fafc;
      padding: 15px;
      border-radius: 14px;
      font-weight: 800;
      line-height: 1.6;
    }

    .result-buttons {
      margin-top: 16px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }

    .sub-btn {
      border: none;
      border-radius: 14px;
      min-height: 52px;
      font-weight: 900;
      background: #eaf4ff;
      color: #347fc4;
    }

    .restart-btn {
      border: none;
      border-radius: 14px;
      min-height: 52px;
      font-weight: 900;
      background: #438fd5;
      color: white;
    }

    @media (max-width: 520px) {
      .card {
        padding: 27px 18px;
        border-radius: 22px;
      }

      h1 {
        font-size: 32px;
      }

      .type-list {
        grid-template-columns: 1fr;
      }

      .type-list div:last-child {
        grid-column: auto;
      }

      .question-text {
        font-size: 22px;
      }

      .result-title {
        font-size: 32px;
      }

      .result-buttons {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>

<body>

<div class="container">

  <!-- 시작 화면 -->
  <section id="startScreen" class="screen active">
    <div class="card start-card">

      <div class="small-title">VOLUNTEER TYPE TEST</div>

      <h1>나의 봉사 성향 테스트</h1>

      <p class="intro">
        나는 어떤 봉사와 가장 잘 맞을까요?<br>
        10개의 질문에 답하고 나의 봉사 성향을 확인해보세요!
      </p>

      <div class="type-list">
        <div>❤️ 따뜻한 나눔형</div>
        <div>⭐ 함께하는 리더형</div>
        <div>🌱 환경 실천형</div>
        <div>🎨 재능나눔형</div>
        <div>📚 성장 지원형</div>
      </div>

      <label class="name-label">
        이름 <span style="font-weight:normal;color:#999;">(선택)</span>
      </label>

      <input
        type="text"
        id="nameInput"
        class="name-input"
        placeholder="이름을 입력해주세요"
        maxlength="10"
      >

      <button class="main-btn" onclick="startTest()">
        테스트 시작하기
      </button>

      <div class="notice">
        정답은 없어요! 나와 가장 가까운 답을 골라주세요.
      </div>

    </div>
  </section>


  <!-- 질문 화면 -->
  <section id="quizScreen" class="screen">
    <div class="card">

      <div class="quiz-header">

        <button class="back-btn" onclick="goBack()">
          ← 이전
        </button>

        <div class="counter">
          <span id="currentQuestion">1</span> / 10
        </div>

      </div>

      <div class="progress">
        <div id="progressBar" class="progress-bar"></div>
      </div>

      <div class="question-box">

        <p id="questionNumber" class="question-number">
          QUESTION 01
        </p>

        <h2 id="questionText" class="question-text"></h2>

      </div>

      <div id="answerList" class="answer-list"></div>

    </div>
  </section>


  <!-- 결과 화면 -->
  <section id="resultScreen" class="screen">

    <div class="card">

      <div class="result-top">
        나의 봉사 성향은?
      </div>

      <div id="resultCard" class="result-card">

        <div id="resultIcon" class="result-icon"></div>

        <div id="resultLabel" class="result-label">
          나의 봉사 성향
        </div>

        <h2 id="resultTitle" class="result-title"></h2>

        <p id="resultTagline" class="result-tagline"></p>

        <p id="resultDescription" class="result-description"></p>


        <div class="result-section">

          <h3>나의 봉사 키워드</h3>

          <div id="keywordList" class="tag-box"></div>

        </div>


        <div class="result-section">

          <h3>나에게 잘 맞는 봉사활동</h3>

          <div id="recommendList" class="tag-box"></div>

        </div>


        <div id="resultMessage" class="result-message"></div>

      </div>


      <div class="result-buttons">

        <button class="sub-btn" onclick="shareResult()">
          결과 공유하기
        </button>

        <button class="restart-btn" onclick="restartTest()">
          다시 테스트하기
        </button>

      </div>

    </div>

  </section>

</div>


<script>

const TYPES = {

  A: {
    title: "따뜻한 나눔형",
    icon: "❤️",
    tagline: "따뜻한 마음으로 이웃에게 힘이 되어주는 봉사자",
    description:
      "다른 사람의 이야기에 귀 기울이고, 도움이 필요한 사람을 직접 돕는 활동에서 보람을 느끼는 유형이에요. 작은 관심과 배려를 통해 누군가에게 따뜻한 하루를 선물하는 것을 좋아해요.",

    keywords: [
      "공감",
      "배려",
      "소통",
      "돌봄"
    ],

    recommends: [
      "어르신 말벗",
      "취약계층 나눔",
      "도시락·반찬 나눔",
      "아동 돌봄 보조",
      "안부 확인 활동"
    ],

    message:
      "당신의 따뜻한 관심은 누군가에게 큰 힘이 됩니다!",

    color: "#ef607d",
    soft: "#fff0f4",
    border: "#ffc5d1"
  },


  B: {
    title: "함께하는 리더형",
    icon: "⭐",
    tagline: "사람들과 힘을 모아 변화를 만들어가는 봉사자",

    description:
      "여러 사람과 함께 활동하고 의견을 나누는 것을 좋아하는 유형이에요. 활동을 계획하거나 친구들을 이끌고, 모두가 함께 참여할 수 있도록 분위기를 만드는 데 강점이 있어요.",

    keywords: [
      "리더십",
      "협동",
      "적극성",
      "소통"
    ],

    recommends: [
      "캠페인 운영",
      "행사 진행 보조",
      "봉사단 활동",
      "체험부스 운영",
      "지역사회 홍보활동"
    ],

    message:
      "함께할 때 더 큰 변화를 만드는 당신은 우리 동네의 든든한 리더!",

    color: "#3488d1",
    soft: "#edf7ff",
    border: "#acd4f3"
  },


  C: {
    title: "환경 실천형",
    icon: "🌱",
    tagline: "작은 실천으로 지구와 우리 동네를 지키는 봉사자",

    description:
      "환경문제에 관심이 많고 일상에서 직접 실천하는 것을 중요하게 생각하는 유형이에요. 환경을 위한 작은 행동도 꾸준히 이어지면 큰 변화를 만들 수 있다고 믿어요.",

    keywords: [
      "실천",
      "환경",
      "책임감",
      "지속가능성"
    ],

    recommends: [
      "플로깅",
      "자원순환 활동",
      "환경캠페인",
      "생태보호 활동",
      "탄소중립 실천",
      "환경교육 보조"
    ],

    message:
      "오늘의 작은 실천이 내일의 지구를 바꿉니다!",

    color: "#37a55a",
    soft: "#eefaf0",
    border: "#bce3c6"
  },


  D: {
    title: "재능나눔형",
    icon: "🎨",
    tagline: "내가 잘하고 좋아하는 것으로 나눔을 실천하는 봉사자",

    description:
      "그림, 음악, 만들기, 사진, 글쓰기 등 자신의 재능과 관심사를 다른 사람과 나눌 때 즐거움을 느끼는 유형이에요. 내가 가진 작은 재능도 누군가에게는 특별한 선물이 될 수 있어요.",

    keywords: [
      "창의성",
      "재능",
      "표현",
      "즐거움"
    ],

    recommends: [
      "미술·공예 봉사",
      "공연 봉사",
      "사진·영상 촬영",
      "디자인·홍보 봉사",
      "교육 재능기부"
    ],

    message:
      "당신의 재능이 누군가에게 특별한 선물이 될 수 있어요!",

    color: "#8d65c7",
    soft: "#f5f0fc",
    border: "#d6c4ed"
  },


  E: {
    title: "성장 지원형",
    icon: "📚",
    tagline: "배움과 경험을 나누며 함께 성장하는 봉사자",

    description:
      "새로운 것을 배우고 알려주는 것을 좋아하며, 다른 사람의 성장을 돕는 과정에서 보람을 느끼는 유형이에요. 지식과 경험을 나누면서 나 자신도 함께 성장하는 봉사를 선호해요.",

    keywords: [
      "배움",
      "교육",
      "성장",
      "책임감"
    ],

    recommends: [
      "학습 멘토링",
      "진로 멘토링",
      "교육 보조",
      "아동·청소년 프로그램 지원",
      "디지털 교육 봉사"
    ],

    message:
      "함께 배우고 성장할 때 더 나은 내일이 만들어집니다!",

    color: "#ec8a22",
    soft: "#fff5e8",
    border: "#ffd29d"
  }

};



const QUESTIONS = [

{
  text: "봉사활동을 시작한다면 가장 끌리는 활동은?",

  answers: {
    A: "혼자 계신 어르신의 말벗이 되어드리기",
    B: "친구들과 함께 캠페인을 기획하고 진행하기",
    C: "우리 동네를 걸으며 환경정화 활동하기",
    D: "그림이나 만들기 재능을 활용해 나눔하기",
    E: "어린 친구들의 공부나 체험활동 도와주기"
  }
},


{
  text: "친구들과 무언가를 준비할 때 나는?",

  answers: {
    A: "힘들어하는 친구가 없는지 먼저 살펴본다.",
    B: "우리 이렇게 해보자! 의견을 내고 역할을 정한다.",
    C: "일회용품이나 불필요한 쓰레기를 줄일 방법을 생각한다.",
    D: "재미있고 새로운 아이디어를 제안한다.",
    E: "친구들이 어려워하는 부분을 설명해준다."
  }
},


{
  text: "봉사활동을 마친 뒤 가장 뿌듯할 것 같은 순간은?",

  answers: {
    A: "덕분에 힘이 됐어요라는 말을 들었을 때",
    B: "모두가 힘을 합쳐 목표를 달성했을 때",
    C: "내가 실천한 만큼 주변 환경이 깨끗해졌을 때",
    D: "내가 만든 작품이나 공연으로 사람들이 즐거워할 때",
    E: "내가 도운 사람이 새로운 것을 배우거나 성장했을 때"
  }
},


{
  text: "자유시간이 생겼다! 가장 해보고 싶은 것은?",

  answers: {
    A: "가족이나 친구와 이야기하며 시간 보내기",
    B: "친구들을 모아 재미있는 활동 계획하기",
    C: "공원이나 자연 속에서 시간 보내기",
    D: "그림, 음악, 사진, 만들기 등 취미생활 하기",
    E: "새로운 분야를 배우거나 체험하기"
  }
},


{
  text: "우리 동네에 봉사활동을 하나 만든다면?",

  answers: {
    A: "홀로 지내는 이웃에게 안부를 전하는 활동",
    B: "주민들이 함께 참여하는 즐거운 캠페인",
    C: "깨끗한 우리 동네를 만드는 환경 프로젝트",
    D: "주민들과 함께하는 문화·예술 체험활동",
    E: "아이들과 함께 배우는 교육·멘토링 활동"
  }
},


{
  text: "누군가 도움을 요청한다면 나는?",

  answers: {
    A: "먼저 이야기를 들어주고 마음을 살핀다.",
    B: "주변 사람들과 함께 해결할 방법을 찾는다.",
    C: "작은 것부터 바로 행동으로 옮긴다.",
    D: "내가 잘하는 것을 활용해 도와준다.",
    E: "스스로 해결할 수 있도록 방법을 알려준다."
  }
},


{
  text: "봉사활동에서 내가 맡고 싶은 역할은?",

  answers: {
    A: "참여자를 세심하게 챙기는 역할",
    B: "사람들을 이끌고 전체 활동을 진행하는 역할",
    C: "직접 움직이며 현장에서 실천하는 역할",
    D: "홍보물이나 체험 프로그램을 만드는 역할",
    E: "활동 내용을 설명하고 알려주는 역할"
  }
},


{
  text: "다음 중 가장 마음에 드는 말은?",

  answers: {
    A: "따뜻한 관심이 누군가에게 힘이 된다.",
    B: "함께하면 더 큰 변화를 만들 수 있다.",
    C: "작은 실천이 세상을 바꾼다.",
    D: "나의 재능도 특별한 나눔이 될 수 있다.",
    E: "배움을 나누면 함께 성장할 수 있다."
  }
},


{
  text: "새로운 봉사활동에 참여하게 됐다. 나는?",

  answers: {
    A: "함께하는 사람들과 먼저 친해지고 싶다.",
    B: "어떤 역할을 맡으면 좋을지 적극적으로 찾아본다.",
    C: "말보다는 직접 행동하면서 참여하고 싶다.",
    D: "나만의 방식으로 재미있게 참여하고 싶다.",
    E: "활동의 의미와 방법부터 자세히 알아보고 싶다."
  }
},


{
  text: "내가 생각하는 가장 멋진 봉사자는?",

  answers: {
    A: "다른 사람의 마음을 따뜻하게 보듬어주는 사람",
    B: "여러 사람을 하나로 모으고 함께 행동하는 사람",
    C: "작은 일이라도 꾸준히 실천하는 사람",
    D: "자신이 가진 재능을 기꺼이 나누는 사람",
    E: "자신의 경험과 지식을 다른 사람과 나누는 사람"
  }
}

];



let currentQuestion = 0;

let answers = new Array(
  QUESTIONS.length
).fill(null);

let userName = "";



function showScreen(id) {

  document
    .querySelectorAll(".screen")
    .forEach(screen =>
      screen.classList.remove("active")
    );

  document
    .getElementById(id)
    .classList.add("active");

  window.scrollTo(0, 0);
}



function startTest() {

  userName =
    document
      .getElementById("nameInput")
      .value
      .trim();

  currentQuestion = 0;

  answers =
    new Array(
      QUESTIONS.length
    ).fill(null);

  renderQuestion();

  showScreen("quizScreen");
}



function renderQuestion() {

  const question =
    QUESTIONS[currentQuestion];

  document
    .getElementById("currentQuestion")
    .textContent =
    currentQuestion + 1;

  document
    .getElementById("questionNumber")
    .textContent =
    "QUESTION " +
    String(currentQuestion + 1)
      .padStart(2, "0");

  document
    .getElementById("questionText")
    .textContent =
    question.text;


  const progress =
    ((currentQuestion + 1) /
      QUESTIONS.length) *
    100;

  document
    .getElementById("progressBar")
    .style.width =
    progress + "%";


  const list =
    document
      .getElementById("answerList");

  list.innerHTML = "";


  Object
    .entries(question.answers)
    .forEach(([type, text]) => {

      const button =
        document.createElement("button");

      button.className =
        "answer-btn";

      button.innerHTML = `
        <span class="answer-letter">
          ${type}
        </span>

        <span>
          ${text}
        </span>
      `;


      button.onclick = () => {

        answers[currentQuestion] =
          type;

        if (
          currentQuestion <
          QUESTIONS.length - 1
        ) {

          currentQuestion++;

          renderQuestion();

        } else {

          showResult();

        }

      };


      list.appendChild(button);

    });


  document
    .querySelector(".back-btn")
    .style.visibility =
    currentQuestion === 0
      ? "hidden"
      : "visible";

}



function goBack() {

  if (currentQuestion > 0) {

    currentQuestion--;

    renderQuestion();

  }

}



function calculateResult() {

  const score = {
    A: 0,
    B: 0,
    C: 0,
    D: 0,
    E: 0
  };


  answers.forEach(answer => {

    if (answer) {

      score[answer]++;

    }

  });


  const maxScore =
    Math.max(
      ...Object.values(score)
    );


  const tied =
    Object
      .keys(score)
      .filter(
        key =>
          score[key] === maxScore
      );


  if (tied.length === 1) {

    return tied[0];

  }


  /*
  동점일 경우
  Q3 선택을 먼저 반영
  */

  if (
    tied.includes(answers[2])
  ) {

    return answers[2];

  }


  /*
  그래도 동점이면
  Q1 선택 반영
  */

  if (
    tied.includes(answers[0])
  ) {

    return answers[0];

  }


  return tied[0];

}



function showResult() {

  const resultType =
    calculateResult();

  const result =
    TYPES[resultType];


  document
    .getElementById("resultIcon")
    .textContent =
    result.icon;


  document
    .getElementById("resultTitle")
    .textContent =
    result.title;


  document
    .getElementById("resultTagline")
    .textContent =
    result.tagline;


  document
    .getElementById("resultDescription")
    .textContent =
    result.description;


  document
    .getElementById("resultMessage")
    .textContent =
    "“" +
    result.message +
    "”";


  const resultLabel =
    document
      .getElementById("resultLabel");


  if (userName) {

    resultLabel.textContent =
      userName +
      "님의 봉사 성향은?";

  } else {

    resultLabel.textContent =
      "나의 봉사 성향은?";

  }



  const keywordList =
    document
      .getElementById("keywordList");


  keywordList.innerHTML = "";


  result.keywords
    .forEach(keyword => {

      const tag =
        document.createElement("span");

      tag.className =
        "tag";

      tag.textContent =
        keyword;

      tag.style.background =
        result.soft;

      tag.style.color =
        result.color;

      keywordList
        .appendChild(tag);

    });



  const recommendList =
    document
      .getElementById("recommendList");


  recommendList.innerHTML = "";


  result.recommends
    .forEach(item => {

      const tag =
        document.createElement("span");

      tag.className =
        "tag";

      tag.textContent =
        item;

      tag.style.background =
        result.soft;

      tag.style.color =
        result.color;

      recommendList
        .appendChild(tag);

    });



  const card =
    document
      .getElementById("resultCard");


  card.style.borderColor =
    result.border;


  document
    .getElementById("resultTitle")
    .style.color =
    result.color;


  document
    .getElementById("resultLabel")
    .style.color =
    result.color;


  document
    .getElementById("resultIcon")
    .style.background =
    result.soft;


  showScreen("resultScreen");

}



function restartTest() {

  currentQuestion = 0;

  answers =
    new Array(
      QUESTIONS.length
    ).fill(null);

  userName = "";

  document
    .getElementById("nameInput")
    .value = "";

  showScreen("startScreen");

}



async function shareResult() {

  const type =
    calculateResult();

  const result =
    TYPES[type];


  let text = "";

  if (userName) {

    text +=
      userName +
      "님의 ";

  } else {

    text +=
      "나의 ";

  }


  text +=
    `봉사 성향은 "${result.title}" ${result.icon}

${result.message}

${window.location.href}`;


  if (navigator.share) {

    try {

      await navigator.share({

        title:
          "나의 봉사 성향 테스트",

        text: text

      });

    } catch (e) {}

  } else {

    try {

      await navigator.clipboard
        .writeText(text);

      alert(
        "결과와 링크가 복사되었습니다!"
      );

    } catch (e) {

      alert(
        "공유 기능을 사용할 수 없습니다."
      );

    }

  }

}

</script>

</body>
</html>
