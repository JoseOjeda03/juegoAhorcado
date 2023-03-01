<template>
<div>
  <h1 class="text-red-700">
    Juego del Ahorcado
  </h1>
  
  <div>
    <input v-model="message" placeholder="edíteme"   @keyup.enter="di(message),letracorrect(message)" maxlength="1">
    <p>El mensaje es: {{ message }}</p>
  </div>

  <div>

  <div class="flex flex-row ">
    <div v-for="palabras in partida"  >
       <div class="w-8 border-b-4 border-indigo-500 m-3"></div>
    </div>
    
  </div>


  </div>
    <p>{{partida}}</p>
    <div class="border-l-4 border-indigo-500" ></div>
</div>


</template>
<script>
  export default {


    

    data(){
      return {
        message: '',
        items: [
  
    ],
    palabras: [
      {message: 'holaaa'},
      {message: 'hola'}
    
    ],
    palabraJu : '' ,
    partida  : null
    
  
  
      }
    },
    mounted: function () {
    this.initializeChoices()
  },
    methods: {
      initializeChoices: function () {


       this.palabraJu= this.palabras[this.randon()].message

       this.partida =this.palabraJu.split('')
        


      },
      randon: function () {
  return Math.floor(Math.random() * 2);
},
      di: function (mensje) {
      this.items.push( {mensaje: mensje})
    },
    letracorrect: function (letra){

      this.partida.forEach(element => {
        if(letra === element){
        alert("Please enter")
        
      }
      });
      
    }
    }
  }

</script>


