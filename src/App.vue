<template>
  <div class="container mt-5 col-12" style="max-width: 1000px;">
    <div class="box" style="margin: 0 auto; border: solid dodgerblue 4px; border-radius: 10px; ">
      <div class="main-title">Код Хемминга</div>
      <div class="container p-2" style="text-align: left">

        <div class="col-12 mb-2 info">
          <div class="col-10 cell-line">
            <div class="title mb-2 p-2">Исходное сообщение</div>
            <div class="left-line col-8">
              <div class="col-8 cell" v-for="a in code" @click="changeData(a)">{{a.value}}</div>
              <br>
              <div class="col-8 title-cell" v-for="a in code">a<sub>{{a.id}}</sub></div>
            </div>
            <div class="right-line col-4">
              <button class="btn btn-primary mt-1 col-8" style="margin-left: 50px" @click="start">Пуск</button>
            </div>
          </div>
        </div>

        <div v-if="flag" class="col-12 mb-2 info">
          <div class="col-10 cell-line">
            <div class="title mb-2 p-2">Код Хемминга</div>
            <div class="left-line col-12">
              <div class="col-8 cell" v-for="b in code_in" v-bind:style="changeColor(b.id)" style="cursor: default">{{b.value}}</div>
              <br>
              <div class="col-8 title-cell" v-for="b in code_in">{{b.title[0]}}<sub>{{b.title[1]}}</sub></div>
            </div>
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
        {id: 0, value: 0, title: 'b0'},
        {id: 1, value: 0, title: 'b1'},
        {id: 2, value: 0, title: 'a0'},
        {id: 3, value: 0, title: 'b2'},
        {id: 4, value: 0, title: 'a1'},
        {id: 5, value: 0, title: 'a2'},
        {id: 6, value: 0, title: 'a3'},
        {id: 7, value: 0, title: 'b3'},
        {id: 8, value: 0, title: 'a4'},
        {id: 9, value: 0, title: 'a5'},
        {id: 10, value: 0, title: 'a6'},
        {id: 11, value: 0, title: 'a7'},
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
.main-title
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
.title
{font-size: 26px}
.cell-line
{display: inline-block;}
.left-line {display: inline-block;}
.right-line
{
  display: inline-block;
  vertical-align: top;
}
.cell-line .cell
{
  display: inline-block;
  width: 50px;
  border: solid 2px black;
  margin-right: -2px;
  text-align: center;
  cursor: pointer;
  height: 50px;
  font-size: 30px;
}
.title-cell
{
  display: inline-block;
  width: 50px;
  margin-right: -2px;
  text-align: center;
  height: 50px;
  font-size: 20px;
}

</style>
