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
        <p v-html=html :ref="palabras"></p>

       </div>
    </div>
    
  </div>


  </div>
    <p>{{partida}}</p>
    <div class="border-l-4 border-indigo-500" ></div>

 <div>
  <canvas  class=""      ref="canvas" >
  </canvas>
 </div>

</div>


</template>
<script>
import { nextTick } from 'process'

  export default {


    

    data(){
      return {
        message: '',
        items: [
  
    ],
    palabras: [
      'holaaa',
       'hola',
      'ala',
      'ooloo',
      
    
    ],
    palabraJu : '' ,
    partida  : [],
    letracorrecta : null,
    letrasColocadas:[],
    letrascorretas:[],
    palabracor:[],
    i:0,
    ultia:"",
    ulmimas:"",
    correctoInco:"",
    elemento:null,
    html:null,
    intentos:0,
    contador:0,
    contadors:0,
    corretas:0,
    numero:0,
    borrar:0,
  
  
      }
    },
    mounted: function () {
    this.initializeChoices()
  },
    methods: {
      initializeChoices: function () {
        this.limpar();

       

       this.palabraJu= this.palabras[this.randon()]

       this.partida =this.palabraJu.split('')
       this.palabracor=this.palabraJu.split('')
       console.log(this.partida)


       this.$refs.canvas.height = 800;
        this.$refs.canvas.width =800;
        const canvas = this.$refs.canvas.getContext('2d') 
        console.log(canvas)
  
        canvas.beginPath();
        canvas.fillStyle = "Red";
        canvas.strokeStyle = "red";
        canvas.moveTo(700, 700);
        canvas.lineTo(100, 700);
        canvas.moveTo(200, 700);
        canvas.lineTo(200, 100);
        canvas.lineTo(500, 100);
        canvas.lineTo(500, 200);
        
        canvas.stroke();
        


      },
      randon: function () {
  return Math.floor(Math.random() * this.palabras.length);
},
      di: function (mensje) {
      this.items.push( {mensaje: mensje})
    },
    letracorrect: function (letra){
     
      this.letracorrecta=null;
      this.palabracor.forEach(element => {
        if(letra === element){
         

        this.correctoInco="correcto";
        this.elemento=element;
        this.corretas++;
         if(this.ultia != element){
          
          this.contador=0;
        }
        else{
          this.contador++;
        }
        this.borrar=this.contador
        console.log(this.contador)
        this. $refs[element][this.contador].textContent = element
         
         






         this.ultia=element;
         console.log(this.palabras)
         
      }

      
      
        



      });
      if(this.corretas >= this.partida.length){
          alert("se acaba el juego")

          this.numero=this.palabras.indexOf(this.palabraJu ) 
          
          const filteredLibraries =this.palabras.filter((item) => item !== this.palabraJu)
          this.palabras=filteredLibraries;
          console.log( this.palabras)
          this.partida.forEach(elemetos => {
            if(this.ulmimas != elemetos){
          
          this.contadors=0;
        }
        else{
          this.contadors++;
        }
        console.log(this.contadors)
            this. $refs[elemetos][this.contadors].textContent = ""
           this.ulmimas=elemetos;
          });

          this.contador=0;
          
          this.initializeChoices();
          

         }
      this.contador=0;

      if (this.correctoInco==="correcto"){
        this.letracorrecta=this.elemento;
        this.letrasColocadas.push(this.elemento)
        console.log(this.letrasColocadas)
        alert( this.correctoInco)
      }else{
        this.intentos++;

        alert("Incorreto")
        this.dibujar()

      }

      this.correctoInco=""
    },
    suma: function (ii) {
      this.i=i+ii;
    },
    dibujar: function(){
      if (this.intentos>0){
    
          const canvas = this.$refs.canvas.getContext('2d') 
          canvas.beginPath();

          canvas.arc(500, 250, 50, 0, Math.PI * 2, true); 
          canvas.stroke();

      }
      if (this.intentos>1){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.moveTo(500, 500);
    canvas.lineTo(500, 300);
    canvas.stroke();

}
if (this.intentos>2){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.moveTo(500, 500);
    canvas.lineTo(400, 600);
    canvas.stroke();

}
if (this.intentos>3){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.moveTo(500, 500);
    canvas.lineTo(600, 600);
    canvas.stroke();

}
if (this.intentos>4){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.moveTo(500, 350);
    canvas.lineTo(400, 400);
    canvas.stroke();

}
if (this.intentos>4){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.moveTo(500, 350);
    canvas.lineTo(600, 400);
    canvas.stroke();

}
    },
    colocar: function (){
      this.palabracor.forEach(element => {
           
 
      });
    },
    limpar: function (){
      console.log("hola"+ this.borrar)


    
      this.palabraJu ='' ;
      this.partida  = [];
      this.letracorrecta = null;
      this.letrasColocadas=[];
      this.letrascorretas=[];
      this.palabracor=[];
      this. i=0;
      this.ultia=null;
      this.ulmimas=null;
      this.correctoInco="";
      this.elemento=null;
      this.html=null;
      this.intentos=0;
      this.contador=0;
      this.corretas=0;
      this.numero=0;
    }
    }
  }

</script>
<style>
canvas { background: #eee; display: block; margin: 0 auto; border: 1px solid black; }
</style>


