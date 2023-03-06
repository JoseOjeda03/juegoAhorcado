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
       <div class="w-8 border-b-4 border-indigo-500 m-3"  :ref="palabras">
      

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
      'aalaa',
      
    
    ],
    palabraJu : '' ,
    partida  : [],
    letracorrecta : null,
    letrasColocadas:[],
    letrascorretas:[],
    palabracor:[],
    i:0,
    ultia:"",
    correctoInco:"",
    elemento:null,
    html:``,
    intentos:0,
    contador:0,
    corretas:0,
    numero:0,
  
  
      }
    },
    mounted: function () {
    this.initializeChoices()
  },
    methods: {
      initializeChoices: function () {


       this.palabraJu= this.palabras[this.randon()]

       this.partida =this.palabraJu.split('')
       this.palabracor=this.palabraJu.split('')
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
         
        alert(element)
        this.correctoInco="correcto";
        this.elemento=element;
        this.corretas++;
         if(this.ultia != element){
          this. $refs[element][0].textContent = element
         }else if(letra== this.ultia &&this.contador <=0){
          alert("se repite 2")
          this. $refs[element][1].textContent = element
          delete(this.palabracor[this.palabracor.indexOf(element)])
          this.contador++;
          console.log(this.contador)

         }
         else if(this.contador > 0 && this.contador <=1){
          alert("se repite 3")
          this. $refs[element][1].textContenintentost = element
          this. $refs[element][2].textContent = element
  
          this.contador++;
          console.log(this.contador)
         }
         else if(this.contador > 1){
          alert("se repite 4")
          this. $refs[element][1].textContent = element
          this. $refs[element][2].textContent = element
          this. $refs[element][3].textContent = element
          
         }


         if(this.corretas >= this.partida.length){
          alert("se acaba el juego")

          this.numero=this.palabras.indexOf(this.palabraJu ) 
          
          delete(this.palabras[this.numero])
          console.log( this.palabras)
          this.initializeChoices();
          

         }

         this. $refs[element][0].textContent = element
         this.palabracor.slice( this.palabracor.indexOf(element), 1)
         this.ultia=element;
         console.log(this.palabracor)
         
      }

      
      
        



      });

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
    }
    }
  }

</script>
<style>
canvas { background: #eee; display: block; margin: 0 auto; border: 1px solid black; }
</style>


