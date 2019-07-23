<template>
  <div id="app">
    <HelloWorld msg="井字棋游戏" />
    <div class="row">
      <Cell index="0" @click="clickCell" :result="result"/>
      <Cell index="1" @click="clickCell" :result="result"/>
      <Cell index="2" @click="clickCell" :result="result"/>
    </div>
    <div class="row">
      <Cell index="3" @click="clickCell" :result="result"/>
      <Cell index="4" @click="clickCell" :result="result"/>
      <Cell index="5" @click="clickCell" :result="result"/>
    </div>
    <div class="row">
      <Cell index="6" @click="clickCell" :result="result"/>
      <Cell index="7" @click="clickCell" :result="result"/>
      <Cell index="8" @click="clickCell" :result="result"/>
    </div>
    <div class="result">{{result}}</div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Cell from "./components/Cell";
export default {
  name: "app",
  data: function() {
    return {
      count: 0,
      mapdata: [[null, null, null], [null, null, null], [null, null, null]],
      result: null
    };
  },
  components: {
    HelloWorld,
    Cell
  },
  methods: {
    clickCell: function(index, text) {
      let rowindex = Math.floor(index / 3)
      let columnindex = index % 3
      this.mapdata[rowindex][columnindex] = text
      this.calcResult()
    },
    calcResult: function(){
      let mapdata = this.mapdata;
      // 判断胜负
      for (let i = 0; i < 3; i++) {
        if ( mapdata[i][0] !== null && mapdata[i][0] === mapdata[i][1] && mapdata[i][1] === mapdata[i][2] ) {
          this.result = `游戏结束，获胜的是：${mapdata[i][0]}`
          break
        }
      }
      for (let i = 0; i < 3; i++) {
        if ( mapdata[0][i] !== null && mapdata[0][i] === mapdata[1][i] && mapdata[1][i] === mapdata[2][i] ) {
          this.result = `游戏结束，获胜的是：${mapdata[0][i]}`
          break
        }
      }

      if ( mapdata[0][0] !== null && mapdata[0][0] === mapdata[1][1] && mapdata[1][1] === mapdata[2][2] ) {
        this.result = `游戏结束，获胜的是：${mapdata[0][0]}`
      }
      if ( mapdata[0][2] !== null && mapdata[0][2] === mapdata[1][1] && mapdata[1][1] === mapdata[2][0] ) {
        this.result = `游戏结束，获胜的是：${mapdata[0][2]}`
      }
      if(this.count === 9 && this.result === null){
        console.log('gg')
        this.result = `游戏结束，打成平手`
      }
    }
  }
};
</script>

<style>
.row {
  display: flex;
  justify-content: center;
  align-items: center;
}
.result {
  font-size: 20px;
  color: red;
  text-align: center;
}
</style>
