<template>
  <div class="fold"  :class="{open:open}">
    <div class="row">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" @click="toggle()">
        <path d="M 16.25 1.34375 L 7.25 11.34375 L 6.65625 12 L 7.25 12.65625 L 16.25 22.65625 L 17.75 21.34375 L 9.34375 12 L 17.75 2.65625 Z">
        </path>
      </svg>
      <input type="checkbox" :checked="checked" ref="allCheck" @click="checkAll()">
      <div class="title" @click="select">{{ name }}</div>
    </div>
    <div class="body" :class="{open}">

      <div v-for="(i, num) in entries" :key="num">
        <div class="row">
          <input type="checkbox" class="mva" v-model="i.checked">
          <div class="mva">
            {{ i.name }}
          </div>
          <input class="mva mr-10" type="text" v-model="i.num" v-on:keypress="isNumber($event)">
          <div class="color-wrapper">
            <input type="color" v-model="i.color">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Fold",
  data(){
    return{
      open:true,
    }
  },
  props:{
    name:String,
    checked:Boolean,
    entries:Array
  },
  watch:{
    checked(){
      this.$emit('check')
    },
    entries:{
      deep:true,
      handler(){
        let all = true;
        let allOff = true;
        for (let i of this.entries){
          if(!i.checked) all=false;
        }
        for (let i of this.entries){
          if(i.checked) allOff=false;
        }
        if(!all && !allOff)
          console.log(this.$refs.allCheck.indeterminate=true);
        else
          this.$refs.allCheck.indeterminate=false
        this.checked=all;
      }
    },
  },
  methods:{
    checkAll(){
      // alert(this.checked)
      this.checked=!this.checked;
      for (let i of this.entries){
        // alert(i.checked)
        i.checked = this.checked;
      }
    },
    toggle(){
      this.open=!this.open;
    },
    select(){
      // this.$emit('select')
    },
    isNumber: function(evt) {
      evt = (evt) ? evt : window.event;
      var charCode = (evt.which) ? evt.which : evt.keyCode;
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
        evt.preventDefault();
      } else {
        return true;
      }
    }
  }
}
</script>

<style scoped>
.row{
  display:flex;
  padding:6px;
}
.body .row :nth-child(2){
  flex-grow:1;
}
.fold{
  background-color: white;
  padding:10px;
  width:250px;
  margin-bottom:5px;
  border-radius:5px;
}
.fold:not(:last-child){

  box-shadow: 0px 7px 5px -8px black;
}
div svg{
  width:17px;
  transform:rotate(180deg);
  margin-right:5px;
  transition: 0.15s;
}

div.open svg{
  width:17px;
  transform:rotate(270deg);
}

.color-wrapper{
  width: 30px;
  height: 30px;
  border-radius:15px;
  overflow: hidden;
}

.color-wrapper input{
  width:100px;
  height:100px;
  transform:translate(-50%, -50%);
}

.mva{
  margin-top:auto;
  margin-bottom:auto;
 }
.mr-10{
  margin-right:10px;
}
.title{
  flex-grow:1;
}
.body{
  margin-left:30px;
  max-height: 0;
  transition: max-height 0.15s ease-out;
  overflow: hidden;
  /*background: #d5d5d5;*/
}
input[type="text"]{
  width:30px;
  border:none;
  border-bottom:2px solid #929292;
  text-align: center;
}
.open{
  max-height: 500px;
  transition: max-height 0.25s ease-in;
}
input[type=checkbox] {
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius:3px;
  outline: none;
  border: 1px solid #929292;
  margin-right: 15px;
}
input[type=checkbox]:checked {
  appearance: none;
  width: 20px;
  background-color: green;
  /*outline: 1px solid green;*/
  height: 20px;
  border-radius:3px;
  border: 3px solid white;
  box-shadow: 0 0 5px 2px green;
}
input[type=checkbox]:indeterminate{
  background-color: 	#FF7F50;
  border: 7px solid white;
  box-shadow: 0 0 5px 2px 	#FF7F50;
}
</style>