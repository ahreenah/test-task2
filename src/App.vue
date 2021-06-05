<template>
  <div id="app">
    <List  :list="lists" @select="selectList"></List>

    <ShownList  :list="lists"></ShownList>
  </div>
</template>

<script>
 import List from './components/List.vue'
 import ShownList from "@/components/ShownList";

export default {
  name: 'App',
  components: {
    List,
    ShownList
  },
  methods:{
    selectList(a,b){
      alert(a);
      alert(b)
    }
  },
  data() {
    return {
      lists: [{
        name: "A",
        checked:false,
        children: [{
          checked:false,
          name: "A1",
          num:2,
          color:"#d95db6"
        }, {
          checked:false,
          name: "A2",
          num:6,
          color:"#936265"
        }]
      },{
        checked:false,
        name: "B",
        children: [{
          checked:false,
          name: "B1",
          num:11,
          color:"#F80367"
        }, {
          checked:false,
          name: "B2",
          num:11,
          color:"#F8F2F4"
        }]
      },{
        checked:false,
        name: "C",
        children: [{
          checked:false,
          name: "B1",
          num:11,
          color:"#FAEDFF"
        }, {
          checked:false,
          name: "B2",
          num:11,
          color:"#123456"
        }, {
          checked:false,
          name: "B3",
          num:11,
          color:"#229999"
        }, {
          checked:false,
          name: "B4",
          num:11,
          color:"#936592"
        }]
      }]
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

#app {
  display:flex;
  flex-firection:row;
  font-family: "Roboto";
}
</style>
