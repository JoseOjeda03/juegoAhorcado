<template>
    <div class="modal-styles" @click="$emit('close-modal'),$emit('inicio')">
        <div class="modal grid justify-items-center" @click.stop>
         
          <img class="" src="hola.png" alt="">
          <div class="bg-[url('~/img/hola.jpg')] bg-cover w-48 h-48" ></div>
          <h6 class="">GANASTE </h6>
          <p>puedes intentarlo de nuevo </p>
          <button class="close" @click="$emit('close-modal'),$emit('inicio')">JUGAR</button>
        </div>
        <div >
          <img class="close-img" src="" alt="" />
        </div>
      </div>
</template>

<script>


  export default {
    methods :{
        reload: function(){
            location.reload();
        }
    }
}
</script>