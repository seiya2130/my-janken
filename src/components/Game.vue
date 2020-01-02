<template>
  <div id="game">
    <div><img :src="src" alt=""></div>
    <div v-if="resultMessage">
      <h2>{{ resultMessage }}</h2>
      <div><button @click="start">もう一度</button></div>
    </div>
    <ul>
      <li>
        <button class="button" @click="onSelected" value="0">グー</button></li>
      <li>
        <button class="button" @click="onSelected" value="1">チョキ</button>
      </li>
      <li>
        <button class="button" @click="onSelected" value="2">パー</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'game',
 props: {
    'pushScore': {
      type: Function,
      requrred: true
    }
  },
  data: function(){
    return {
      src: require('../assets/gu.jpg'),
      resultMessage:'',
      imgList: [
        require('../assets/gu.jpg'),
        require('../assets/choki.jpg'),
        require('../assets/par.jpg'),
      ],
      timer: null,
      }
    },
  created: function(){
    this.start()
  },
  methods:{
    changeImg() {
      var num = Math.floor(Math.random() * this.imgList.length);
      this.src = this.imgList[num];
    },
    start(){
      this.reset();
      this.timer = setInterval(this.changeImg,100);
    },
    onSelected(e){
      clearInterval(this.timer);
      let button = e.target;
      let selectNum = parseInt(button.value, 10);
      let resultNum = parseInt(this.imgList.indexOf(this.src), 10);
      let decision = this.decisionJanken(selectNum, resultNum);

      var btns = document.querySelectorAll('.button');
      for( let btn of btns ) {
          btn.setAttribute('disabled', true);
      }

      if(decision == 0){
        this.resultMessage = '引き分け';
      }else if(decision==1){
        this.resultMessage = '負け';
      }else{
        this.resultMessage = '勝ち';
      }
      button.classList.add('is-selected');
      this.pushScore({msg:this.resultMessage});
    },
    decisionJanken(myhand,youhand){
      
      return (myhand - youhand+3)%3;
    },
    reset(){
      var btns = document.querySelectorAll('.button');
      for( let btn of btns ) {
          btn.removeAttribute('disabled');
          btn.classList.remove('is-selected');
      }
      this.resultMessage = '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.is-selected {
  color:black;
  background-color: white;
}
img {
  width: 400px;
  height: 400px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
