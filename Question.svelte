<script>
  export let questionText;
</script>

<style>
  h3 {
    font-size: 2em;
    animation: slideLeft 500ms forwards cubic-bezier(0.25, 0.65, 0.31, 1.15);
  }
  @keyframes slideLeft {
    0% {
      transform: translateX(-1000px);
    }
    100% {
      transform: translateX(0);
    }
  }
</style>

<h3>{questionText}</h3>
