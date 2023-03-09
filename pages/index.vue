<template>
<div>
  <h1 class="text-red-700">
    Juego del Ahorcado
  </h1>
  
  <div>
    <input v-model="message" placeholder="edíteme"  ref="input" @keyup.enter="di(message),validar(message)" maxlength="1">
    <p>El mensaje es: {{ message }}</p>
  </div>

  <div>

  <div class="flex flex-row ">
    <div v-for="palabras in partida"  >
       <div class="w-8 border-b-4 border-indigo-500 m-3" ref="contenr"  >
        <p ref="value" :ref="palabras"     >
        
        {{  }}</p>

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


  export default {


    

    data(){
      return {
        message: '',
        items: [
  
    ],
    nul:"",
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
        this.$refs.input.value="" 
       

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
    repetidas: function(lettras){
      let conten=0;
      this.palabracor.forEach(elen=> {
          if(lettras !=elen ){
            conten=0;
          }
          else{
            conten++;
          }
          return conten
      })
    },
    esta: function (lete){
      var resultado= false;
        this.letrasColocadas.forEach(elem =>
        {
          if(elem == lete){
            resultado= true;
          }else{
            resultado=  false
          }
        })
        
        return resultado;
    },
    validar: function(letra){


        do{
          letra=this.message
          if(this.esta(letra)){
          alert("repita el valor que la letra ya esta colocada")
          this.$refs.input.value="" 
          
          }else{
            console.log("no repite")
            this.letracorrect(letra)
            this.k=1;
           this.$refs.input.value="" 

            letra=""
          }
        } while(this.k !=1)

    },
    letracorrect: function (letra){
      console.log(this.esta(letra))
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

      this.contador=0;

      if (this.correctoInco==="correcto"){
        this.letracorrecta=this.elemento;
        this.letrasColocadas.push(this.elemento)
        console.log(this.letrasColocadas)
        alert( this.correctoInco)

        if(this.corretas >= this.partida.length){


          this.numero=this.palabras.indexOf(this.palabraJu ) 
          this.$refs.input.value="" 
          
          const filteredLibraries =this.palabras.filter((item) => item !== this.palabraJu)
          this.palabras=filteredLibraries;
          console.log( this.palabras)
          this.palabracor.forEach(elemetos => {
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
                    this.palabracor.forEach(elemetos => {
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
          alert("se acaba el juego")
          this.initializeChoices();
          
        

         }
      }else{
        this.intentos++;

        alert("Incorreto")
        this.dibujar()

      }
      this.$refs.input.value="" 
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

      
      
      this.$refs.input.value="" 
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


