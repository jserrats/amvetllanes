<template>
  <div class="hello">
    <h1>Quina és una {{ question }}?</h1>
  </div>
</template>

<script>
console.log("test")
export default {
  name: "Question",
  props: {
    question: String,
  },
};
</script>