<template>
  <div>
    <div class="cell" @click="onClickCell">{{text}}</div>
  </div>
</template>
<script>
export default {
  name: "cell",
  props: {
    index: String,
    result: String    
  },
  data: function() {
    return {
      text: null
    };
  },
  methods: {
    onClickCell: function() {
      if (this.text !== null || this.result !== null) {
        return;
      }
      
      this.text = this.$parent.count % 2 === 0 ? "X" : "O";
      this.$parent.count += 1;
      this.$emit('click', this.index, this.text)
    }
  }  
};
</script>

<style scoped>
.cell {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  border: 1px solid black;
  font-size: 40px;
}
</style>

