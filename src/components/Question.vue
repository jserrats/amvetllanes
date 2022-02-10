<template>
  <div class="hello">
    <transition name="slide-fade" mode="out-in">
      <div :key="question">
        <h1>Quina és una {{ question }}?</h1>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "Question",
  props: {
    question: String,
  },
};
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.2s ease;
}

.slide-fade-leave-active {
  transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter,
.slide-fade-leave-to

/* .slide-fade-leave-active for <2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>