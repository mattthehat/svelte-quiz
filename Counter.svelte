<script>
  export let questionNumber;
  export let questions;
</script>

<style>
  span {
    position: absolute;
    top: 5px;
    right: 10px;
    animation: fadeIn 0.4s forwards;
  }
  @keyframes faeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>

<span>Question {questionNumber} of {questions}</span>
