<template>
  <div class="col">

    <ShownFold :entries="i.children" :name="i.name" v-for="(i,num) in list.filter(j=>hasChecked(j))" :key="num"></ShownFold>
    <!--    @select="select(i,num)"-->
  </div>
</template>

<script>
import ShownFold from "./ShownFold.vue"
export default {
  name: 'ShownList',
  props: {
    name: String,
    list:Array,

  },
  components:{
    ShownFold
  },
  data(){
    return{
    }
  },
  methods:{

    hasChecked(i){
      console.log('hc',i);
      for (let j of i.children){
        if(j.checked) {
          console.log('true');
          return true;
        }
      }
      return false
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
  flex-grow:1;
}
</style>
