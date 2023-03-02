<template>
<div>
  <h1 class="text-red-700">
    Juego del Ahorcado
  </h1>
  
  <div>
    <input v-model="message" placeholder="edíteme"   @keyup.enter="di(message),letracorrect(message)" maxlength="1">
    <p>El mensaje es: {{ message }}</p>
  </div>message

  <div>

  <div class="flex flex-row ">
    <div v-for="palabras in partida"  >
       <div class="w-8 border-b-4 border-indigo-500 m-3"  >
      
        <p   :ref="palabras"  >
 
        </p>
       </div>
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
    partida  : null,
    letracorrecta : null,
    letrasColocadas:[],
    letrascorretas:[],
    palabracor:[],
    i:0,
    ultia:"" 
    
    
  
  
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
      this.letracorrecta=null;
      this.partida.forEach(element => {
        if(letra === element){
        alert(element)
        this.letracorrecta=element;
        this.letrasColocadas.push(element)
         this.palabracor.push(element)
         if(this.ultia != element){
          this. $refs[element][0].textContent = element
         }else{
          alert("se repite")
         }
         this. $refs[element][0].textContent = element
         this.ultia=element;


      }
   
      });
      
    },
    suma: function (ii) {
      this.i=i+ii;
    }
    }
  }

</script>


