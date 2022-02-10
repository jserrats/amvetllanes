<template>
  <div>
   <img @click="answer()"  :src="picPath">
  </div>
</template>

<script>
// <img @click="answer()"  :src="picPath">
// <img @click="answer()" src="../assets/logo.png">
export default {
  name: "Answer",
  props: {
    option: String,
  },
  computed: {
    picPath: function () {
      //return require('@/assets/' +  this.option + '.png');
      return require("@/assets/" + this.option + ".png");
    },
  },
  methods: {
    answer() {
      this.$emit("answer", this.option);
    },
  },
};
</script>