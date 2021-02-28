<template>
  <h1> コンビニにお菓子を買いに行きたい </h1>
  <div class="image-wrapper">
  <img :class="{ loading: loading }" :src="imgSrc">
  </div>
  <p> {{result}} </p>
  <div>
    <button class="btn btn-border" v-on:click="changeImg">お菓子チャレンジ</button>
  </div>
  <div class="bar">
    <input type="range" max="1" step="0.01" v-model.number="prob">
  </div>
  <p>食欲 {{ Math.round(prob * 100) }} %</p>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      imgSrc: require('./assets/famima.png'), 
      prob: 0.5,
      result: "ボタンを押してチャレンジ",
      loading: false,
    }
  },
  methods: {
    changeImg: async function() {
      this.imgSrc=require('./assets/cupcake_yellow.png')
      this.result="チャレンジ中..."
      this.loading = true;
      await this.sleep(1000);
      this.loading = false;

      console.log(this.prob);
      if ( Math.random()<this.prob ) {
        this.imgSrc=require('./assets/mirai_go.png')
        this.result="チャレンジ成功"
      } else {
        this.imgSrc=require('./assets/gaman_okashi.png')
        this.result="チャレンジ失敗"
      }
    },
    sleep: function(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.image-wrapper{
  margin:auto;
  height:200px;
  width:200px;
}

img {
  height: 100%;
  width: 100%;
}

img.loading {
  margin-top: 70px;
  height: 30%;
  width: 30%;
  animation: rotate 1s linear infinite;
}
 
@keyframes rotate {
    0%{ transform:rotate(0);}
  100%{ transform:rotate(360deg); }
}

.bar {
  margin-left: auto;
  margin-right: auto;
  margin-top: 24px;
  height: 40px;
  width: 300px;
}


input[type="range"] { 
    margin: auto;
    -webkit-appearance: none;
    position: relative;
    overflow: hidden;
    /* height: 100%; */
    height: 40px;
    width: 100%;
    cursor: pointer;
    border-radius: 0; /* iOS */
}

::-webkit-slider-runnable-track {
    background: #ddd;
}

::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 20px; /* 1 */
    height: 40px;
    /* height:100%; */
    background: #fff;
    /* box-shadow: -100vw 0 0 100vw dodgerblue; */
    box-shadow: -100vw 0 0 100vw orange;
    border: 2px solid #999; /* 1 */
}

::-moz-range-track {
    height: 40px;
    /* height:100%; */
    background: #ddd;
}

::-moz-range-thumb {
    background: #fff;
    height: 40px;
    /* height:100%; */
    width: 20px;
    border: 3px solid #999;
    border-radius: 0 !important;
    /* box-shadow: -100vw 0 0 100vw dodgerblue; */
    box-shadow: -100vw 0 0 100vw orange;
    box-sizing: border-box;
}

::-ms-fill-lower { 
    /* background: dodgerblue; */
    background: orange;
}

::-ms-thumb { 
    background: #fff;
    border: 2px solid #999;
    height: 40px;
    /* height:100%; */
    width: 20px;
    box-sizing: border-box;
}

::-ms-ticks-after { 
    display: none; 
}

::-ms-ticks-before { 
    display: none; 
}

::-ms-track { 
    background: #ddd;
    color: transparent;
    height: 40px;
    /* height:100%; */
    border: none;
}

::-ms-tooltip { 
    display: none;
}

button{
        background-color: transparent;
        border: none;
        cursor: pointer;
        outline: none;
        padding: 0;
        appearance: none;
}

/* 共通部分らしいところ */
*,
*:before,
*:after {
  -webkit-box-sizing: inherit;
  box-sizing: inherit;
}

html {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  font-size: 62.5%;/*rem算出をしやすくするために*/
}

.btn,
button.btn,
button.btn {
  font-size: 1.6rem;
  font-weight: 700;
  line-height: 1.5;
  position: relative;
  display: inline-block;
  padding: 1rem 4rem;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  -webkit-transition: all 0.3s;
  transition: all 0.3s;
  text-align: center;
  vertical-align: middle;
  text-decoration: none;
  letter-spacing: 0.1em;
  color: #212529;
  border-radius: 0.5rem;
}

/* ボタン */

/*
button.btn-border {
  border-radius: 0;
}

button.btn-border:before,
button.btn-border:after {
  position: absolute;

  width: 100%;
  height: 2px;

  content: '';
  -webkit-transition: all .3s;
  transition: all .3s;

  background: #000;
}

button.btn-border:before {
  top: 0;
  left: 0;
}

button.btn-border:after {
  right: 0;
  bottom: 0;
}

button.btn-border:hover:before,
button.btn-border:hover:after {
  width: 0;
}
*/
button.btn-border {
  border: 2px solid #000;
  border-radius: 0;
  background: #fff;
}

button.btn-border:hover {
  color: #fff;
  background: #000;
}
</style>
