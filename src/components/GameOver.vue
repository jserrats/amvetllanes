<template>
  <div class="hello">
    <table>
      <tr>
        <th>Punts</th>
        <th>Encerts</th>
        <th>Errors</th>
      </tr>
      <tr>
        <td>{{ score }}</td>
        <td>{{ rights }}</td>
        <td>{{ wrongs }}</td>
      </tr>
    </table>
    
    <button class="button" v-if="!playing" v-on:click="answer()">
      Vull tornar a jugar!

    </button>
  </div>
</template>

<script>
export default {
  name: "GameOver",
  props: {
    score: Number,
    rights: Number,
    wrongs: Number,
  },
  methods: {
    answer() {
      this.$emit("newGame");
    },
  },
};
</script>
<style scoped>
table {
  width: 50%;
  margin-left: auto;
  margin-right: auto;
  font-size: xx-large;
}
</style>