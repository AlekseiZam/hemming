<template>
  <div class="d-inline-flex p-2">
    <div class="cell-line">
      <div class="cell" v-for="a in code" @click="changeData(a)">{{a.value}}</div>
    </div>
    <button @click="logo">Пуск</button>
  </div>
</template>

<script>
export default {
  data(){
    return{
      code: [
        {id: 0, value: 0},
        {id: 1, value: 0},
        {id: 2, value: 0},
        {id: 3, value: 0},
        {id: 4, value: 0},
        {id: 5, value: 0},
        {id: 6, value: 0},
        {id: 7, value: 0}
      ]
    }
  },
  methods:{
    changeData(a){
      if (a.value == 0)
        this.code[a.id].value = 1
      else
        this.code[a.id].value = 0
    },
    logo()
    {console.log(this.code)}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cell-line
{
  display: flex;

}
.cell-line .cell
{
  border: solid 2px black;
  width: 40px;
  margin-right: -2px;
  text-align: center;
  cursor: pointer;
}
</style>
