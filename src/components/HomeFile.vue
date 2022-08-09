<template>
<div class="keyboard">
  <div class="a" v-for="line in vals.users" :key="line">
     <div class="b" v-for="ch in line.chars" :key="ch">
         <button id="c" v-if="vals.tog && line.type!='special keys'" v-on:click="write(ch.toUpperCase());shuffle(vals.users)">{{ch.toUpperCase()}}</button>
         <button id="c" v-else v-on:click="write(ch);shuffle(vals.users)">{{ch}}</button>
     </div> 
  </div>
  <button v-on:click="vals.tog=!vals.tog">caps</button>
</div>
</template>

<script>
export default {
  name: 'HomeFile',
  props:{
    data:String,
    msg:String,
    val:String 
  },data(){
      return{ 
        vals:{users:[
            {type:'numbers',chars:['1','2','3','4','5','6','7','8','9','0']},
            {row:'letters',chars:['q','w','e','r','t','y','u','i','o','p','a','s','d','f','g','h','j','k','l','z','x','c','v','b','n','m']},
            {type:'sp',chars:['!','@','#','~','`','$','%','^','&','*','(',')','-','_','|','?',',','.','<','>',':','{','[',']','=','+','/',';']},
            {type:'special keys',chars:['back','clear','   space   ']}
       ],tog:false}
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
    flex-wrap: wrap;
    justify-content: left;
  }

</style>
