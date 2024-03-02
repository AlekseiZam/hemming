<template>
  <div class="container mt-5 col-12" style="max-width: 1000px;">
    <div class="box" style="margin: 0 auto; border: solid dodgerblue 4px; border-radius: 10px; ">
      <div class="title">Код Хемминга</div>
      <div class="container p-2" style="text-align: left">

        <div class="col-12 mb-5 info">
          <div class="col-10 cell-line">
            <div class="mb-2">Исходное сообщение</div>
            <div class="col-8 cell" v-for="a in code" @click="changeData(a)">{{a.value}}</div>
            <button class="col-2 btn btn-primary" style="margin-left: 50px" @click="start">Пуск</button>
          </div>
        </div>

        <div v-if="flag" class="col-12 mb-5 info">
          <div class="cell-line">
            <div class="mb-2">Код Хемминга</div>
            <div class="cell" v-for="b in code_in" v-bind:style="changeColor(b.id)">{{b.value}}</div>
          </div>
        </div>

      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'App',

  data(){
    return{
      flag: false,
      code: [
        {id: 0, value: 0},
        {id: 1, value: 0},
        {id: 2, value: 0},
        {id: 3, value: 0},
        {id: 4, value: 0},
        {id: 5, value: 0},
        {id: 6, value: 0},
        {id: 7, value: 0}
      ],
      code_in: [
        {id: 0, value: 0},
        {id: 1, value: 0},
        {id: 2, value: 0},
        {id: 3, value: 0},
        {id: 4, value: 0},
        {id: 5, value: 0},
        {id: 6, value: 0},
        {id: 7, value: 0},
        {id: 8, value: 0},
        {id: 9, value: 0},
        {id: 10, value: 0},
        {id: 11, value: 0},
      ],
    }
  },
  methods:{
    changeData(a){
      if (a.value == 0)
        this.code[a.id].value = 1
      else
        this.code[a.id].value = 0
    },
    start()
    {
      let k = 0
      for (const i in this.code_in){
        if (((this.code_in[i].id + 1) & this.code_in[i].id) != 0)
        {
          this.code_in[i].value = this.code[k].value
          k = k + 1
        }
      }
      this.flag = true
    },

    changeColor(b)
    {
      if ((b+1 & (b)) == 0)
        return "background: aqua"
    }

  }
}
</script>





<style scoped>
.title
{
  font-size: 30px;
  color: antiquewhite;
  width: 100%;
  background-color: dodgerblue;
  text-align: center;
}
.info
{
  display: block;
}
.cell-line
{
  display: inline-block;
}
.cell-line .cell
{
  display: inline-block;
  width: 50px;
  border: solid 2px black;
  margin-right: -2px;
  text-align: center;
  cursor: pointer;
  padding: 10px;
  height: 50px;
}
</style>
