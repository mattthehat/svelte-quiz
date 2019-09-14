<script>
  import Button from "./Button.svelte";
  import Question from "./Question.svelte";
  import Counter from "./Counter.svelte";
  let quizData;
  let currentUrl;
  let fetchUrl;
  let quizStart = false;
  let questionIndex = 0;
  let score = 0;
  let quizEnd = false;
  let numOfQuestions;
  let questionsAnswered = 0;
  let percentageRight;
  let show = true;
  let isCorrect = false;
  let isIncorrect = false;
  let answeredCorrectly = false;
  let answeredIncorrectly = false;
  const startQuiz = () => {
    quizStart = true;
  };
  const submitAnswer = correct => {
    if (correct) {
      score++;
    }
    show = false;
    isCorrect = false;
    isIncorrect = false;
    answeredCorrectly = false;
    answeredIncorrectly = false;
    setTimeout(() => {
      show = true;
    }, 1);
    questionsAnswered++;
    if (questionsAnswered === numOfQuestions) {
      quizEnd = true;
      return;
    }
    questionIndex++; // Move to next question
  };

  const submit = correct => {
    isCorrect = true;
    isIncorrect = true;
    if (correct) {
      answeredCorrectly = true;
    } else {
      answeredIncorrectly = true;
    }
    setTimeout(() => {
      submitAnswer(correct);
    }, 2000);
  };

  $: percentageRight = (score / numOfQuestions) * 100;
  $: console.log(questionIndex);
  $: console.log(isCorrect);

  onMount(() => {
    quizData = {
      id: 2,
      title: "Test Quiz",
      slug: "test-quiz",
      image: "156786573769761639_10156633813153786_7280544727265443840_o.jpg",
      intro:
        "<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Dolor sed viverra ipsum nunc aliquet bibendum enim. In massa tempor nec feugiat. Nunc aliquet bibendum enim facilisis gravida. Nisl nunc mi ipsum faucibus vitae aliquet nec ullamcorper.</p>",
      published: 1,
      published_at: "2019-09-10 12:00:00",
      created_at: "2019-09-07 16:05:42",
      updated_at: "2019-09-07 16:05:42",
      questions: [
        {
          id: 1,
          quiz_id: 2,
          title: "Who is a guitarist?",
          answers: [
            {
              id: 1,
              question_id: 1,
              content: "Bobby Brown",
              is_correct: 0
            },
            {
              id: 2,
              question_id: 1,
              content: "Geoff Capes",
              is_correct: 0
            },
            {
              id: 3,
              question_id: 1,
              content: "Dave Stewart",
              is_correct: 1
            },
            {
              id: 4,
              question_id: 1,
              content: "Billy Bush",
              is_correct: 0
            }
          ]
        },
        {
          id: 2,
          quiz_id: 2,
          title: "Who is a snooker player?",
          answers: [
            {
              id: 5,
              question_id: 2,
              content: "Roger Black",
              is_correct: 0
            },
            {
              id: 6,
              question_id: 2,
              content: "Steve Davies",
              is_correct: 1
            },
            {
              id: 7,
              question_id: 2,
              content: "Les Dennis",
              is_correct: 0
            },
            {
              id: 8,
              question_id: 2,
              content: "Nick Nolte",
              is_correct: 0
            }
          ]
        },
        {
          id: 5,
          quiz_id: 2,
          title: "Who was in Pink Floyd?",
          answers: [
            {
              id: 13,
              question_id: 5,
              content: "Jerry Jackson",
              is_correct: 0
            },
            {
              id: 14,
              question_id: 5,
              content: "Nick Mason",
              is_correct: 1
            },
            {
              id: 15,
              question_id: 5,
              content: "Barbera Wintergreen",
              is_correct: 0
            },
            {
              id: 16,
              question_id: 5,
              content: "Frank Gambale",
              is_correct: 0
            }
          ]
        }
      ]
    };
  });
</script>

<style>
  .quiz__container {
    width: 100%;
    max-width: 900px;
    height: 500px;
    border: 1px solid #ccc;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: #d3cce3;
    background: linear-gradient(to right, #e9e4f0, #d3cce3);
    margin-bottom: 5em;
    overflow: hidden;
    position: relative;
    animation: fadeIn 0.6s forwards;
  }
  .quiz__end {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    animation: fadeIn 1s forwards;
  }
  .quiz__end > h3 {
    font-size: 2em;
    margin: 0.3em 0;
  }
  .quiz__end-result {
    font-size: 1.2em;
  }
  .quiz__end-img {
    width: auto;
    height: 200px !important;
  }
  .quiz__list {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    list-style: none;
    width: 100%;
  }
  .quiz__item {
    width: 100%;
    display: flex;
    justify-content: center;
  }
  .btn__start {
    display: block;
    font-size: 4em;
    margin: 1em auto 3em auto;
  }
  .answer-correct {
    font-size: 1.2em;
    padding: 15px;
    position: absolute;
    bottom: 40px;
    width: 40%;
    color: #fff;
    background: #66ad57;
    text-align: center;
    display: block;
    border-radius: 15px;
    animation: popUp 0.3s forwards cubic-bezier(0.08, 0.82, 0.39, 1.24);
  }
  .answer-incorrect {
    font-size: 1.2em;
    padding: 15px;
    position: absolute;
    bottom: 40px;
    width: 40%;
    color: #fff;
    background: #bb2e25;
    text-align: center;
    display: block;
    border-radius: 15px;
    animation: popUp 0.3s forwards cubic-bezier(0.08, 0.82, 0.39, 1.24);
  }
  .icon-check::after {
    color: #fff;
  }

  .icon-close::after {
    color: #fff;
  }
  .quiz__bubble1 {
    position: absolute;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 100px;
    bottom: -70px;
    animation: slide 70s infinite;
  }
  .quiz__bubble2 {
    position: absolute;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 500px;
    bottom: -300px;
    animation: slide 35s infinite;
  }
  .quiz__bubble3 {
    position: absolute;
    width: 70px;
    height: 70px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 200px;
    bottom: -300px;
    animation: slide 50s infinite;
  }
  .quiz__bubble4 {
    position: absolute;
    width: 70px;
    height: 70px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 430px;
    bottom: -300px;
    animation: slide 50s infinite;
  }
  .quiz__bubble5 {
    position: absolute;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 650px;
    bottom: -100px;
    animation: slide 60s infinite;
  }
  .quiz__bubble6 {
    position: absolute;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 580px;
    bottom: -100px;
    animation: slide 30s infinite;
  }
  .quiz__bubble7 {
    position: absolute;
    width: 90px;
    height: 90px;
    border-radius: 50%;
    background: rgb(169, 160, 194);
    transform: rotate(10deg);
    left: 770px;
    bottom: -100px;
    animation: slide 45s infinite;
  }
  @keyframes slide {
    0% {
      transform: translateY(0px);
      opacity: 1;
    }
    50% {
      opacity: 0;
    }
    100% {
      transform: translateY(-800px);
      opacity: 0;
    }
  }
  @keyframes fadeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
  @keyframes popUp {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
</style>

{#if quizStart}
  <div class="quiz__container bb-shadow">
    <div class="quiz__bubble1" />
    <div class="quiz__bubble2" />
    <div class="quiz__bubble3" />
    <div class="quiz__bubble4" />
    <div class="quiz__bubble5" />
    <div class="quiz__bubble6" />
    <div class="quiz__bubble7" />
    {#if !quizEnd}
      {#if quizData}
        {#if show}
          <Counter
            questionNumber={questionsAnswered + 1}
            questions={numOfQuestions} />
          <Question questionText={quizData.questions[questionIndex].title} />
          <ul class="quiz__list">
            {#each quizData.questions[questionIndex].answers as answer}
              <li class="quiz__item">
                <Button
                  isCorrect={answer.is_correct ? isCorrect : null}
                  isIncorrect={!answer.is_correct ? isCorrect : null}
                  btnText={answer.content}
                  class="btn btn__primary quiz__btn"
                  on:click={e => submit(answer.is_correct)} />
              </li>
            {/each}
          </ul>
          {#if answeredCorrectly}
            <span class="answer-correct icon-check">Correct</span>
          {/if}
          {#if answeredIncorrectly}
            <span class="answer-incorrect icon-close">Wrong</span>
          {/if}
        {/if}
      {/if}
    {:else}
      <div class="quiz__end">
        <h3>Final Score {score}/{numOfQuestions}</h3>
        <p class="quiz__end-result">
          You Got {Math.floor(percentageRight)}% Correct
        </p>
        {#if percentageRight === 0}
          <p>That must be fake news?</p>
          <img
            class="quiz__end-img"
            src="https://media1.tenor.com/images/8e812b44e11d586aff5880bb52e74837/tenor.gif?itemid=4522223"
            alt="Smiley face"
            height="342"
            width="342" />
        {:else if percentageRight === 100}
          <p>Are you some sort of genius?</p>
          <img
            class="quiz__end-img"
            src="https://media1.tenor.com/images/594248287a966cab434eb8221e621ba4/tenor.gif?itemid=11410651"
            alt="Smiley face"
            height="342"
            width="342" />
        {:else if percentageRight === 50}
          <p>Not a bad start?</p>
          <img
            class="quiz__end-img"
            src="https://media1.tenor.com/images/3266283f2dfc7231df6a14ec657eb009/tenor.gif?itemid=5538639"
            alt="Smiley face"
            height="342"
            width="342" />
        {/if}
      </div>
    {/if}
  </div>
{/if}
{#if !quizStart}
  <button class="btn btn__primary btn__start" on:click={startQuiz}>
    Start Quiz
  </button>
{/if}
