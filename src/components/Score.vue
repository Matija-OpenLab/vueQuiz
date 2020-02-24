<template>
  <div>
    <h1>Total: {{ totalAns }}</h1>
    <h1>Correct: {{ correctAns }}</h1>
  </div>
</template>
<script>
export default {
  props: ["totalAns", "correctAns"]
};
</script>
