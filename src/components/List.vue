<template>
  <div class="col">
    <Fold :entries="i.children" :name="i.name" :checked="i.checked" @check="check(i)" v-for="(i,num) in list" :key="num" ></Fold>
<!--    @select="select(i,num)"-->
  </div>
</template>

<script>
import Fold from "./Fold.vue"
export default {
  name: 'List',
  props: {
    name: String,
    list:Array,

  },
  components:{
    Fold
  },
  data(){
    return{
      // list:[
      //   {
      //     name:"A",
      //     children:[{
      //       name:"A1"
      //     },{
      //     name: "A2"
      //     }]
      //   }
      // ]
    }
  },
  methods:{
    check(i){
      i.checked=!i.checked;
    },

    select(i,num){
      // alert(i);
      this.$emit('select',i,num)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.col{
  display:flex;
  flex-direction:column;

  box-shadow:1px 1px 5px #929292;
  border-radius:5px;
  margin-right: 10px;
}
</style>
