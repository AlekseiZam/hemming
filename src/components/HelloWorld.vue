<template>
  <div class="container">

  <div class="d-inline-flex p-2">
    
    <div class="cell-line">
      <div v-for="a in code">
        <div class="name-cell">a<sub>{{ a.id }}</sub></div>
        <div class="cell" @click="changeData(a)">{{a.value}}</div>
      </div>
    </div>
    <button @click="logo">Пуск</button>
  </div>

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
    {console.log(this.code)},
    getColor(id){
      if (id == 0|| id == 1 || id == 3 || id == 9)
        return 'background-color: greenyellow;'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cell-line
{
  display: flex;

}

.name-cell
{text-align: center;}

.cell-line .cell
{
  border: solid 2px black;
  width: 40px;
  margin-right: -2px;
  text-align: center;
  cursor: pointer;
}

</style>
