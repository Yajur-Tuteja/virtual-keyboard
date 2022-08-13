<template>
<div class="keyboard">
  <div class="a" v-for="kind in vals.users" :key="kind">
     <div class="b" v-for="ch in kind.chars" :key="ch"> 
        <button id="k" v-if="vals.isTab && ch=='back'" v-on:click="vals.isTab=false;write('backtab')">{{ch}}</button>
        <button id="k" v-else-if="vals.tog && kind.type!='special keys'" v-on:click="write(ch.toUpperCase());shuffle(vals.users)">{{ch.toUpperCase()}}</button>
        <button id="k" v-else v-on:click="write(ch);shuffle(vals.users)">{{ch}}</button>
     </div> 
  </div>
  
  <button v-on:click="vals.tog=!vals.tog">caps</button>
  <button v-on:click="write('tab');vals.isTab=true">tab</button>
</div>
</template>

<script>
export default {
  name: 'HomeFile',
  props:{
    data:String
  },
  data(){
      return{ 
        vals:{users:[
            {type:'numbers',chars:['1','2','3','4','5','6','7','8','9','0']},
            {type:'letters',chars:['q','w','e','r','t','y','u','i','o','p','a','s','d','f','g','h','j','k','l','z','x','c','v','b','n','m']},
            {type:'symbols',chars:['!','@','#','~','`','$','%','^','&','*','(',')','-','_','|','?',',','.','<','>',':','{','[',']','=','+','/',';']},
            {type:'special keys',chars:['back','clear','   space   ']}
       ],tog:false,isTab:false}
      }
    },
methods:{
  write(value){
      this.$emit("key-is-pressed",value);
    },
   shuffle(keys){
      for(let i=0;i<keys.length-1;i++){
        for(let j=keys[i].chars.length-1;j>0;j--){
            const k=Math.floor(Math.random()*(j+1));
            const temp=keys[i].chars[j];
            keys[i].chars[j]=keys[i].chars[k];
            keys[i].chars[k]=temp;
          }
        }
      }
    }
}

</script>

<style>
  .a{
    display: flex;
    justify-content: left;
  }
</style>
