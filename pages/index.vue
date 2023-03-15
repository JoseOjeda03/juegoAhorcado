<template>
<div class="flex flex-row  justify-between bg-[url('~/img/nube.png')] bg-cover w-screen h-screen">

  <div class="">

    
    <div class="flex flex-col grid justify-items-center w-[70rem]  ">
      <h1 class="text-red-700 text-4xl mb-16">
        Juego del Ahorcado
      </h1>
      <input class="border border-black" v-model="message" :disabled="disabled==1" placeholder="edíteme"  ref="input" @keyup.enter="di(message),validar(message)" maxlength="1">
      <p class="text-lg ">El la letra es: {{ message }}</p>

    </div>
  
    <div>
  
    <div class="flex flex-row ">
      <div v-for="palabras in partida"  >
         <div class="w-16 border-b-4 border-red-500 m-6 grid justify-items-center" ref="contenr"  >
          <p class="text-xl" ref="letras" :ref="palabras"     >
          
          </p>
  
         </div>
      </div>
      
    </div>
  
  
    </div>
      <p>{{partida}}</p>
     
      <div class="grid justify-items-center">
        <h1 class="text-red-600 text-2xl mb-16">HISTORIAL</h1>
        <div class="border-solid border-2 border-indigo-600 w-[50rem] h-[20rem] flex flex-row">
          <div class="mr-6  " v-for="histo in historial">
            <p class="bg-[url('~/img/sisi.jpg)]">
              {{ histo +"," }}
            </p>
            


      </div>

        </div>

      </div>
  </div>
  

 <div class="flex flex-row-reverse " >
  <canvas  class="bg-[url('~/img/lol.jpg')] bg-cover"     ref="canvas" >
  </canvas>
 </div>


<Modal v-show="showModal" v-model="finalJugar" @close-modal="showModal = false" @final=" finalJugar=palabraJu " />
<ModalB v-show="showModalB" @close-modal="showModalB = false" @inicio=" initializeChoices()  " />
</div>


</template>
<script>
import Modal from '~/components/modal.vue'
import ModalB from '~/components/modalB.vue'

  export default {

    components: { Modal ,ModalB,},
    

    data(){
      return {
        disabled:0,
        showModalB:false,
        message: '',
        items: [
  
    ],
    nul:"",
    palabras: [
      
      'website',
      'internet',
      'online',
      'ssd',
      'banco',
      'base',
      'buzon',
      'vaca',
      'venado',
      'perro',
      'delfin',
      'gato',
      'leon',
      'elefante',
      'pato',
      'leopardo',
      'ballena',
      'jirafa',
      'holaaa',
       'hola',
      'ala',
      'ooloo',
      
    
    ],
    palabraJu : '' ,
    partida  : [],
    letracorrecta : null,
    letrasColocadas:[],
    historial:[],
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
    k:0,
    l:0,
  
  
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


       this.$refs.canvas.height = 750;
        this.$refs.canvas.width =800;
        const canvas = this.$refs.canvas.getContext('2d') 
        console.log(canvas)
  
        canvas.beginPath();
        canvas.fillStyle = "Red";
        canvas.strokeStyle = "black";
        canvas.lineWidth=10
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
    
    vacio: function(lete){
      var resultado= false;
      if(lete == ""){
            resultado= true;
          }else{
            resultado=  false
          }
          return resultado;
    },
    esta: function (lete){
      var resultado= false;
        this.historial.forEach(elem =>
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
           letra=this.message.toLowerCase()
          if(this.vacio(letra)){
            alert("repita la letra que esta vacia ")
       
          this.message="";  
          break;
          }else{
            do{

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
        this.l=1;
          }
        
        }while(this.l !=1)
    },
    letracorrect: function (letra){
      console.log(this.esta(letra))
      this.letracorrecta=null;
      this.historial.push(letra);
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
      this.$refs.input.value="" 
      this.contador=0;

      if (this.correctoInco==="correcto"){
        this.letracorrecta=this.elemento;
        this.letrasColocadas.push(this.elemento)
        console.log(this.letrasColocadas)
        alert( this.correctoInco)
       
        this.ganar();
      }else{
        this.intentos++;

        alert("Incorreto")
        this.dibujar()

      }
      this.message="" 
      this.correctoInco=""
    },
    ganar: function(){

      if(this.corretas >= this.partida.length){


        this.numero=this.palabras.indexOf(this.palabraJu ) 
        this.$refs.input.value="" 

        const filteredLibraries =this.palabras.filter((item) => item !== this.palabraJu)
        this.palabras=filteredLibraries;
        console.log( this.palabras)
        this.borrarpa();
      
        


          this.contador=0;
          this.showModalB=true;
          this.message=""
          this.disabled=(this.disabled + 1) % 2
}
    },
    borrarpa: function(){
      this.palabracor.forEach(element => {

         if(this.ultia != element){
          
          this.contador=0;
        }
        else{
          this.contador++;
        }
        this.borrar=this.contador
        console.log(this.contador)
        this. $refs[element][this.contador].textContent = ""
         
         this.ultia=element;
         console.log(this.palabras)
         
      
      });
      this.$refs.input.value="" 
      this.contador=0;



    },
    dibujar: function(){
      if (this.intentos>0){
    
          const canvas = this.$refs.canvas.getContext('2d') 
          canvas.beginPath();
          canvas.strokeStyle = "red";
          canvas.lineWidth=5
          canvas.arc(500, 250, 50, 0, Math.PI * 2, true); 
          canvas.stroke();

      }
      if (this.intentos>1){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.strokeStyle = "red";
          canvas.lineWidth=5
    canvas.moveTo(500, 500);
    canvas.lineTo(500, 300);
    canvas.stroke();

}
if (this.intentos>2){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.strokeStyle = "red";
    canvas.lineWidth=5
    canvas.moveTo(500, 500);
    canvas.lineTo(400, 600);
    canvas.stroke();

}
if (this.intentos>3){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.strokeStyle = "red";
    canvas.lineWidth=5
    canvas.moveTo(500, 500);
    canvas.lineTo(600, 600);
    canvas.stroke();

}
if (this.intentos>4){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.strokeStyle = "red";
    canvas.lineWidth=5
    canvas.moveTo(500, 350);
    canvas.lineTo(400, 400);
    canvas.stroke();

}
if (this.intentos>5){
    
    const canvas = this.$refs.canvas.getContext('2d') 
    canvas.beginPath();
    canvas.strokeStyle = "red";
    canvas.lineWidth=5
    canvas.moveTo(500, 350);
    canvas.lineTo(600, 400);
    canvas.stroke();
    this.disabled=(this.disabled + 1) % 2
    this.showModal = true;

    
     
    


}
    },
    limpar: function (){
      console.log("hola"+ this.borrar)
      this.disabled=0
      this.showModalB=false
      this.message= ''
      this.items=[]
      this.nul=""

      this.palabraJu = '' 
      this.partida  = []
      this.letracorrecta = null
      this.letrasColocadas=[]
      this.historial=[]
      this.palabracor=[]
      this.i=0
      this.ultia=""
      this.ulmimas=""
      this.correctoInco=""
      this.elemento=null
      this.html=null
      this.intentos=0
      this.contador=0
      this.contadors=0
      this.corretas=0
      this.numero=0
      this.borrar=0
      this.k=0
      this.l=0
    }
    }
  }

</script>
<style>
.modal-styles {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  background-color: #000000da;
}

.modal {
  text-align: center;
  background-color: white;
  height: 500px;
  width: 500px;
  margin-top: 10%;
  padding: 60px 0;
  border-radius: 20px;
}
.close {
  margin: 10% 0 0 16px;
  cursor: pointer;
}
  

.check {
  width: 150px;
}

h6 {
  font-weight: 500;
  font-size: 28px;
  margin: 20px 0;
}

p {
  font-size: 16px;
  margin: 20px 0;
}

button {
  background-color: #ac003e;
  width: 150px;
  height: 40px;
  color: white;
  font-size: 14px;
  border-radius: 16px;
  margin-top: 50px;
}
canvas {  display: block; border: 1px solid black; }
</style>


