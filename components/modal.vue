<template>
    <div class="modal-overlay" @click="$emit('close-modal'),reload()">
        <div class="modal grid justify-items-center" @click.stop>
         
          <div class="bg-[url('~/img/pendej.gif')] bg-cover w-80 h-48" ></div>
          <h6>GAMER OVER </h6>
          <p>puedes intentarlo de nuevo </p>
          <button class="close" @click="$emit('close-modal'),reload() ">Go Home</button>
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