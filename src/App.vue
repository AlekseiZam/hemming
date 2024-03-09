<template>
  <div class="container mt-5 col-12" style="min-width: 1000px;">
    <div class="box" style="margin: 0 auto; border: solid dodgerblue 4px; border-radius: 10px; ">
      <div class="main-title">Код Хемминга</div>
      <div class="container p-2" style="text-align: left">

        <div class="col-12 mb-2 info">
          <div class="col-10 cell-line">
            <div class="title mb-2 p-2">Исходное сообщение</div>
            <div class="left-line col-8">
              <div class="col-8 cell" v-for="a in code" @click="changeData(a)">{{a.value}}</div>
              <br>
              <div class="col-8 title-cell" v-for="a in code">a<sub>{{a.id+1}}</sub></div>
            </div>
            <div class="right-line col-4">
              <button class="btn btn-primary mt-1 col-8" style="margin-left: 50px; font-size: 15px;" @click="start">Получить код Хэмминга</button>
            </div>
          </div>
        </div>

        <div v-if="flag" class="col-12 mb-2 info">
          <div class="col-12 cell-line">
            <div class="title mb-2 p-2">Код Хемминга</div>
            <div class="left-line col-7">
              <div class="col-7 title-cell-info" v-for="b in code_hem">{{b.title}}</div>
              <br>
              <div class="col-7 cell" v-for="b in code_hem" v-bind:style="changeColor(b.id)" style="cursor: default">{{b.value}}</div>
              <br>
              <div class="col-7 title-cell" v-for="b in code_hem">b<sub>{{b.id+1}}</sub></div>
            </div>
            <div class="right-line col-5">
              <div class="text">
                <h6>Вычисление контрольных разрядов:</h6>
                b{{ code_hem[0].id + 1 }} = b{{ code_hem[2].id + 1 }} ⊕ b{{ code_hem[4].id + 1 }} ⊕
                b{{ code_hem[6].id + 1 }} ⊕ b{{ code_hem[8].id + 1 }} ⊕ b{{ code_hem[10].id + 1 }} =
                {{ code_hem[2].value }} ⊕ {{ code_hem[4].value }} ⊕ {{ code_hem[6].value }} ⊕ {{ code_hem[8].value }} ⊕
                {{ code_hem[10].value }} =
                {{ code_hem[2].value ^ code_hem[4].value ^ code_hem[6].value ^ code_hem[8].value ^ code_hem[10].value }}
                <br>
                b{{ code_hem[1].id + 1 }} = b{{ code_hem[2].id + 1 }} ⊕ b{{ code_hem[5].id + 1 }} ⊕
                b{{ code_hem[6].id + 1 }} ⊕ b{{ code_hem[9].id + 1 }} ⊕ b{{ code_hem[10].id + 1 }} =
                {{ code_hem[2].value }} ⊕ {{ code_hem[5].value }} ⊕ {{ code_hem[6].value }} ⊕ {{ code_hem[9].value }} ⊕
                {{ code_hem[10].value }} =
                {{ code_hem[2].value ^ code_hem[5].value ^ code_hem[6].value ^ code_hem[9].value ^ code_hem[10].value }}
                <br>
                b{{ code_hem[3].id + 1 }} = b{{ code_hem[4].id + 1 }} ⊕ b{{ code_hem[5].id + 1 }} ⊕
                b{{ code_hem[6].id + 1 }} ⊕ b{{ code_hem[11].id + 1 }} =
                {{ code_hem[4].value }} ⊕ {{ code_hem[5].value }} ⊕ {{ code_hem[6].value }} ⊕ {{ code_hem[11].value }}=
                {{ code_hem[4].value ^ code_hem[5].value ^ code_hem[6].value ^ code_hem[11].value }}
                <br>
                b{{ code_hem[7].id + 1 }} = b{{ code_hem[8].id + 1 }} ⊕ b{{ code_hem[9].id + 1 }} ⊕
                b{{ code_hem[10].id + 1 }} ⊕ b{{ code_hem[11].id + 1 }} =
                {{ code_hem[8].value }} ⊕ {{ code_hem[9].value }} ⊕ {{ code_hem[10].value }} ⊕ {{ code_hem[11].value }}=
                {{ code_hem[8].value ^ code_hem[9].value ^ code_hem[10].value ^ code_hem[11].value }}
              </div>
            </div>
          </div>
        </div>

        <div v-if="flag" class="col-12 mb-2 info">
          <div class="col-12 cell-line">
            <div class="title mb-2 p-2">Помеха</div>
            <div v-if="!err_flag" class="left-line col-7">
              <div class="col-7 cell" v-for="e in code_err" style="cursor: pointer" @click="changeErr(e)">{{e.value}}</div>
            </div>
            <div v-if="err_flag" class="left-line col-7">
              <div class="col-7 cell" v-for="e in code_err" style="cursor: default">{{e.value}}</div>
            </div>
            <div class="right-line col-5">
                <button v-if="!err_flag" class="btn btn-primary mt-1 col-8" style="margin-left: 5px" @click="start2">Продолжить без помех</button>
                <button v-if="err_flag" class="btn btn-primary mt-1 col-5" style="margin-left: 5px" @click="start2">Внести помеху</button>
                <button v-if="err_flag" class="btn btn-primary mt-1 col-5" style="margin-left: 5px" @click="not_err">Сбросить</button>
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
      code_hem: [
        {id: 0, value: 0, title: 'КР'},
        {id: 1, value: 0, title: 'КР'},
        {id: 2, value: 0, title: 'a1'},
        {id: 3, value: 0, title: 'КР'},
        {id: 4, value: 0, title: 'a2'},
        {id: 5, value: 0, title: 'a3'},
        {id: 6, value: 0, title: 'a4'},
        {id: 7, value: 0, title: 'КР'},
        {id: 8, value: 0, title: 'a5'},
        {id: 9, value: 0, title: 'a6'},
        {id: 10, value: 0, title: 'a7'},
        {id: 11, value: 0, title: 'a8'},
      ],
      err_flag: false,
      code_err: [
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
      if (!a.value)
        this.code[a.id].value = 1
      else
        this.code[a.id].value = 0
    },

    start()
    {
      let k = 0
      for (const i in this.code_hem){
        if (((this.code_hem[i].id + 1) & this.code_hem[i].id) != 0)
        {
          this.code_hem[i].value = this.code[k].value
          k = k + 1
        }
      }
      this.code_hem[0].value = this.code_hem[2].value ^ this.code_hem[4].value ^ this.code_hem[6].value ^ this.code_hem[8].value ^ this.code_hem[10].value
      this.code_hem[1].value = this.code_hem[2].value ^ this.code_hem[5].value ^ this.code_hem[6].value ^ this.code_hem[9].value ^ this.code_hem[10].value
      this.code_hem[3].value = this.code_hem[4].value ^ this.code_hem[5].value ^ this.code_hem[6].value ^ this.code_hem[11].value
      this.code_hem[7].value = this.code_hem[8].value ^ this.code_hem[9].value ^ this.code_hem[10].value ^ this.code_hem[11].value
      this.flag = true
    },

    changeColor(b)
    {
      if ((b+1 & (b)) == 0)
        return "background: aqua"
    },

    changeErr(e){
      this.code_err[e.id].value = 1
      this.err_flag = true
    },

    not_err(){
      for(const e in this.code_err)
        this.code_err[e].value = 0
      this.err_flag = false
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
.title-cell-info
{
  display: inline-block;
  width: 50px;
  margin-right: -2px;
  text-align: center;
  height: 50px;
  font-size: 15px;
  margin-bottom: -25px;
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
