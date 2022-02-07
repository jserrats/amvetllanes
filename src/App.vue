<template>
  <div>
    <template v-if="!playing && firstGame">
      <p>
        Aquest joc ha sigut desenvolupat com a prova de concepte de Vue.js 3.
      </p>
      <p>
        Dedicat a la Judit :)
      </p>
      <button class="button" v-on:click="newGame">Comença el joc!</button>
    </template>
    <template v-if="playing">
      <Stats :time="time" :score="score" :rights="rights" :wrongs="wrongs" />
      <Question :question="question" />
      <div class="answers">
        <Answer class="answer" :option="option1" @answer="answered($event)" />
        <Answer class="answer" :option="option2" @answer="answered($event)" />
      </div>
    </template>

    <GameOver
      v-if="!playing && !firstGame"
      :score="score"
      :rights="rights"
      :wrongs="wrongs"
      @newGame="newGame($event)"
    />
  </div>
</template>

<script>
import Answer from "./components/Answer.vue";
import Question from "./components/Question.vue";
import Stats from "./components/Stats.vue";
import GameOver from "./components/GameOver.vue";

export default {
  name: "App",
  components: {
    Question,
    Answer,
    Stats,
    GameOver,
  },
  props: {},
  computed: {
    items: function () {
      return ["avellana", "ametlla"];
    },
  },
  data() {
    return {
      score: 0,
      time: 10,
      question: null,
      playing: false,
      firstGame: true,
      rights: 0,
      wrongs: 0,
    };
  },

  mounted() {
    this.newQuestion();
    setInterval(() => {
      if (this.playing) this.time--;
    }, 1000);
  },
  watch: {
    time(newTime) {
      if (newTime == 0) {
        this.gameOver();
      }
    },
  },
  methods: {
    newGame() {
      this.playing = true;
      this.time = 10;
      this.score = 0;
      this.rights = 0;
      this.wrongs = 0;
    },
    answered(answer) {
      if (answer == this.question) {
        this.score = this.score + 1;
        this.rights++;
      } else {
        this.wrongs++;
        this.score = this.score - 2;
      }
      this.newQuestion();
    },
    newQuestion() {
      this.question = this.items[Math.floor(Math.random() * 2)];
      let tmp = Math.floor(Math.random() * 2);
      this.option1 = this.items[tmp];
      this.option2 = this.items[(tmp + 1) % 2];
      return this.question;
    },
    gameOver() {
      this.playing = false;
      this.firstGame = false;
      //alert("Game Over\nScore: " + this.score);
    },
  },
};
</script>

<style>
#app {
  font-family: "Basier circle", -apple-system, system-ui, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji",
    "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background-color: #cccccc;
}
.answers {
  display: flex;
}

.answer {
  flex: 50%;
  padding: 10px;
}

.button {
  
  background-color: rgba(255, 255, 255, 0.918);
  border: 0 solid #e2e8f0;
  border-radius: 1.5rem;
  box-sizing: border-box;
  color: #0d172a;
  cursor: pointer;
  display: inline-block;
  font-family: "Basier circle", -apple-system, system-ui, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji",
    "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  font-size: 1.1rem;
  font-weight: 600;
  line-height: 1;
  padding: 1rem 1.6rem;
  text-align: center;
  text-decoration: none #0d172a solid;
  text-decoration-thickness: auto;
  transition: all 0.1s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0px 1px 2px rgba(166, 175, 195, 0.25);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button:hover {
  background-color: #1e293b;
  color: #fff;
}

@media (min-width: 768px) {
  .button-81 {
    font-size: 1.125rem;
    padding: 1rem 2rem;
  }
}
</style>
