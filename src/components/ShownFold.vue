<template>
  <div class="fold"  :class="{open:open}">
    <div class="row">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" @click="toggle()">
        <path d="M 16.25 1.34375 L 7.25 11.34375 L 6.65625 12 L 7.25 12.65625 L 16.25 22.65625 L 17.75 21.34375 L 9.34375 12 L 17.75 2.65625 Z">
        </path>
      </svg>
      <div class="title" @click="select">{{ name }}</div>
      <button @click="shuffled=!shuffled">{{shuffled?"Отсортировать":"Перемешать"}}</button>
    </div>
    <div class="body" :class="{open}">

      <div v-for="(i, num) in colors" :key="num">
<!--        {{i}}-->
        <div class="row">
          <div class="color-wrapper" >
            <div :style="'background-color:'+j" @click="i.num--" v-for="(j,n) in i" :key="n"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

function shuffleArray(array) {
  for (var i = array.length - 1; i > 0; i--) {
    var j = Math.floor(Math.random() * (i + 1));
    var temp = array[i];
    array[i] = array[j];
    array[j] = temp;
  }
  return array
}
export default {
  name: "ShownFold",
  data(){
    return{
      open:true,
      shuffled:true,
    }
  },
  props:{
    name:String,
    entries:Array
  },
  computed:{
    colors(){
      if(this.shuffled) {
        let counts = this.entries.filter(i => i.checked);
        let c2 = [];
        for (let i of counts)
            // c2.push([])
          for (let j = 0; j < i.num; j++)
            c2.push(i.color)

        return [shuffleArray(c2)];
      }
      let res =[];
      for (let i of this.entries.filter(i => i.checked)){
        let t = [];
        for(let j = 0; j<i.num; j++)
          t.push(i.color)
        res.push(t)
      }
      return res;
    }
  },
  methods:{
    toNum(num){
      let i = parseInt(num);
      console.log(i);
      if(isNaN(i)) {
        console.log(0)
        return 0;
      }
      return i;
    },
    toggle(){
      this.open=!this.open;
    },
    select(){
      // this.$emit('select')
    }
  }
}
</script>

<style scoped>
.row{
  display:flex;
  padding:6px;
}
.fold{
  margin-left:5px;
  border-radius:5px;
  box-shadow:1px 1px 5px #929292;
  margin-bottom:15px;
}
.fold{
  padding:10px;
  background-color: white;
}
div svg{
  transition: 0.15s;
  width:17px;
  transform:rotate(-180deg);
  margin-right:5px;
}

div.open svg{
  width:17px;
  transform:rotate(-90deg);
}

.color-wrapper{
  display: flex;

  max-width: 100%;
  flex-wrap: wrap;

}

.color-wrapper div{
  width:10px;
  height:10px;
  margin-right:3px;
  margin-bottom:3px;
  border-radius:2px;
}

.mva{
  margin-top:auto;
  margin-bottom:auto;
}
.number{
  margin-right:10px;
  width:40px;
  margin-top: 0;
}
.title{
  flex-grow:1;
}
.body{
  max-height:0;
  overflow:hidden;
  transition: .2s;
}
.body.open{
  max-height:1000px;
  transition:.3s
}
button{
  background:#123456;
  color:white;
  padding:6px;
  border-radius:6px;
  border:none;
}
</style>