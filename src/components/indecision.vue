<template>
  <h1>Indecisión</h1>
  <img v-if="img" :src="img" alt="bg" />
  <div class="bg-darck"></div>
    <div class="indecision-container">
        <input v-model="question" type="text" placeholder="Hazme una pregunta?" />
        <p>Recuerda terminar con un signo de interrogación (?)</p>
        <div v-if="isvalidQ">
        <h2>{{ question }}</h2>
        <h1>{{answer}}</h1>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      question: "hola mundo",
      answer:null,
      img:null,
      isvalidQ:false,
    };
  },
  methods: {
    async getAnswer() {
        this.answer='pensando ....'
        const {answer,image }=await fetch('https://yesno.wtf/api').then(resp=>resp.json() );
        //console.log({answer,image});
       
        this.answer=answer==="yes"?'SI !':'NO !';
        this.img=image;
    }
  },
  watch: {
    question(valor, oldvalor) {
      //console.log({ valor, oldvalor });
      this.isvalidQ=false;
      if(!valor.includes("?")) return
      this.isvalidQ=true;
    this.getAnswer();
    },
  },
};
</script>

<style scoped>
img,
.bg-dark {
  height: 100vh;
  left: 0px;
  max-height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0px;
  width: 100vw;
}

.bg-dark {
  background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
  position: relative;
  z-index: 99;
}

input {
  width: 250px;
  padding: 10px 15px;
  border-radius: 5px;
  border: none;
}
input:focus {
  outline: none;
}

p {
  color: white;
  font-size: 20px;
  margin-top: 0px;
}

h1,
h2 {
  color: white;
}

h2 {
  margin-top: 150px;
}
</style>
