<template>
  <div id="app">
    <h1>じゃんけんゲーム</h1>
        <ul class="nav">
            <li><router-link to="/Game">ゲーム</router-link></li>
            <li><router-link to="/Score">せいせき</router-link></li>
        </ul>
        <router-view :scores="scores" :pushScore="pushScore" :resetScore="resetScore"></router-view>
  </div>
  
</template>

<script>
let storage = localStorage;
export default {  
  name: 'App',
  data() {
    return {
      scores: []
    }
  },
  created() {
    this.setScore();
  },
  methods: {
    pushScore(msg) {
      this.scores.push(msg);
      localStorage.setItem('scores',JSON.stringify(this.scores))
    },
    setScore() {
      this.scores = JSON.parse(localStorage.getItem('scores')) || []
    },
    resetScore() {
      localStorage.removeItem('scores');
      this.scores = [];
    }
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
