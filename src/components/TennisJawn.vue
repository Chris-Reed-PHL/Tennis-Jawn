<template>
  <div class="score-board">
    <h1>{{ msg }}</h1>

    <div class="team-one-score">
      {{ teamOneScore }}
    </div>
    <div class="team-two-score">
      {{ teamTwoScore }}
    </div>

    <button
      class="team-one-button"
      v-on:click="addPointTeamOne"
      :disabled="disableButtons"
    >
      Team One
    </button>
    <button
      class="team-two-button"
      v-on:click="addPointTeamTwo"
      :disabled="disableButtons"
    >
      Team Two
    </button>

    <button class="reset" v-on:click="reset" v-show="disableButtons">
      New Game
    </button>
  </div>
</template>

<script>
export default {
  name: "TennisJawn",
  data() {
    return {
      msg: "Tennis Jawn",
      teamOneScore: "Love",
      teamTwoScore: "Love",
      teamOneCounter: 0,
      teamTwoCounter: 0,
      points: [
        "Love",
        "15",
        "30",
        "40",
        "Winner",
        "Deuce",
        "Advantage In",
        "Winner",
        "Advantage Out",
        "Loser",
      ],
    };
  },
  computed: {
    disableButtons() {
      return (
        (this.teamOneScore == this.points[4] ||
          this.teamTwoScore == this.points[4]) == true
      );
    },
  },
  methods: {
    addPointTeamOne() {
      this.teamOneCounter++;
      this.teamOneScore = this.points[this.teamOneCounter];
      this.loser();
      this.deuce();
      this.advantage();
    },
    addPointTeamTwo() {
      this.teamTwoCounter++;
      this.teamTwoScore = this.points[this.teamTwoCounter];
      this.loser();
      this.deuce();
      this.advantage();
    },
    loser() {
      if (this.teamOneScore == this.points[4]) {
        this.teamTwoScore = this.points[this.points.length - 1];
      } else if (this.teamTwoScore == this.points[4]) {
        this.teamOneScore = this.points[this.points.length - 1];
      }
    },

    deuce() {
      if (
        this.teamOneScore == this.points[3] &&
        this.teamOneScore === this.teamTwoScore
      ) {
        this.teamOneScore = this.points[5];
        this.teamTwoScore = this.points[5];

        this.teamOneCounter = +5;
        this.teamTwoCounter = +5;
      }
    },

    advantage() {
      if (
        this.teamOneScore == this.points[6] &&
        this.teamTwoScore == this.points[6]
      ) {
        this.teamOneScore = this.points[5];
        this.teamTwoScore = this.points[5];

        this.teamOneCounter = +5;
        this.teamTwoCounter = +5;
      }
      if (this.teamTwoScore == this.points[6]) {
        this.teamOneScore = this.points[8];
      }
      if (this.teamOneScore == this.points[6]) {
        this.teamTwoScore = this.points[8];
      }
    },

    reset() {
      location.reload();
    },
  },
};
</script>

<style>
.score-board {
  /* margin: 50% auto; */
  display: grid;
  width: 100%;
  height: auto;

  grid-template-areas:
    "head head"
    "score1 score2"
    "button1 button2"
    "reset reset";
  justify-items: center;
  text-align: center;
}
.team-one-score {
  grid-area: score1;
  justify-items: center;
  text-align: center;
  border: #f2f2f2;
  border-style: groove;
  background-color: bisque;
  width: 25vw;
  height: 100%;
}
.team-two-score {
  grid-area: score2;
  justify-items: center;
  text-align: center;
  border: #f2f2f2;
  border-style: groove;
  background-color: bisque;
  width: 25vw;
  height: 100%;
}
.team-one-button {
  grid-area: button1;
}
.team-two-button {
  grid-area: button2;
}
.reset {
  grid-area: reset;
  width: 50%;
  color: bisque;
}
h1 {
  grid-area: head;
  background: #f2f2f2;
  color: #4b86a6;
  padding: 25px;
  font-size: 50px;
  text-transform: uppercase;
  text-align: center;
  margin: 5% 20% 20% 20%;
  border-top-left-radius: 100px;
  border-bottom-left-radius: 100px;
  border-top-right-radius: 100px;
  border-bottom-right-radius: 100px;
}

button {
  color: #4b86a6;
  padding: 50px 50px;
  background-color: yellowgreen;
  border-top-left-radius: 100px;
  border-bottom-left-radius: 100px;
  border-top-right-radius: 100px;
  border-bottom-right-radius: 100px;
  position: relative;
  margin: 10%;
  font-style: italic;
  font-weight: bold;
}
</style>
