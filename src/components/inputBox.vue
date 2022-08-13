<template>
  Password:<input  id="pass" v-model="input"><br><br>
  <HomeFile v-on:key-is-pressed="write($event)"/>
</template>

<script>
 
import HomeFile from './HomeFile.vue'
export default{
  name:'inputBox',
  components: {
    HomeFile
  },
  data(){
    return{input:''}
  },
  methods:{    
    write(value){
      let val=this.input;
      if(value==='clear'){
         this.input='';
      }
      else if(value==='   space   '){
         this.input+=' ';
      }
      else if(value==='tab'){
        this.input+='  ';
      }
      else if(value==='back'){
        this.input=val.slice(0,-1);
          
      }
      else if(value==='backtab'){
        this.input=val.slice(0,-2);  
      }
      else{
        this.input+=value;
      }

    },
  }
}
</script>
