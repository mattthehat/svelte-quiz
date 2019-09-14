<script>
  export let btnText;
  export let isCorrect = undefined;
  export let isIncorrect = undefined;
</script>

<style>
  .quiz__btn {
    text-align: center;
    width: 80%;
    margin-bottom: 15px;
    animation: slideIn 1s forwards cubic-bezier(0.075, 0.82, 0.165, 1);
  }
  .correct {
    background: #66ad57;
  }
  .incorrect {
    background: #bb2e25;
  }

  @keyframes slideIn {
    0% {
      opacity: 0;
      transform: translateY(1000px);
    }
    100% {
      opacity: 1;
      transform: translateY(0px);
    }
  }
</style>

<button
  class:correct={isCorrect}
  class:incorrect={isIncorrect}
  class="btn btn__primary quiz__btn"
  on:click>
  {btnText}
</button>
