<template>
  <h2>{{titulo}}</h2>
  <h3>{{counter}} <sub>2</sub>= {{correr2}}</h3>
  <hr>
  <button @click="incrementar">+1</button>
  <button @click="decrementar">-1</button>
</template>

<script>
export default {
name:'counter_paptito',
props:{
  title:String,
  start:{
    type:Number,
    default:10,
    required:true,
    validator(value){
      return value>2
    }
  }
},
data(){
    return{
        counter:this.start,
    }
},
methods:{
  correr(){
    console.log('correr');
    return this.counter*this.counter
  },
  incrementar(){
    return this.counter+=1;
  },
  decrementar(){
  return this.counter-=1;
  }
},
computed:{
  correr2(){
    console.log('correr 2');
    return this.counter*this.counter
  },
  titulo(){
    return this.title ? this.title : 'Counters';
  }
}

}
</script>

<style>
button{
  background-color: #64bb87;
  border-radius: 5px;
  color: white;
  margin: 0 5px;
  border: 1px solid white;
  cursor: pointer;
  padding: 5px 15px;
  transition: 0.3s ease-in-out;
}

button:hover{
  background-color: #5aa67b;
  transition: 0.3s ease-in-out;
}

</style>
