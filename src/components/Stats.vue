<template>
  <div class="hello">
    <table>
      <tr>
        <th>Temps</th>
        <th>Punts</th>
        <th>Encerts</th>
        <th>Errors</th>
      </tr>
      <tr>
        <td>{{ time }}</td>
        <td>{{ score }}</td>
        <td>{{ rights }}</td>
        <td>{{ wrongs }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "Stats",
  props: {
    time: Number,
    score: Number,
    rights: Number,
    wrongs: Number,
  },
};
</script>

<style scoped>
table {
  width: 20%;
  margin-left: auto;
  margin-right: auto;
}
</style>