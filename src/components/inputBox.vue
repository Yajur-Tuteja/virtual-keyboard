<template>
  Password:<input id="pass" type="password"><br><br>
  <HomeFile v-on:key-is-pressed="write($event)"  />
</template>

<script>
import HomeFile from './HomeFile.vue'
export default{
  name:'inputBox',
  components: {
    HomeFile
  },
  methods:{
    write(value){
      let val=document.getElementById("pass").value;
      if(value==='back'){
        document.getElementById("pass").value=val.slice(0,-1);
      }
      else if(value==='clear'){
         document.getElementById("pass").value='';
      }
      else if(value==='   space   '){
         document.getElementById("pass").value+=" ";
      }
      else if(value==='caps'){
        return value;
      }
      else{
         document.getElementById("pass").value+=value;
      }

      
    }
  }
}
</script>