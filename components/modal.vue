<template>
    <div class="modal-overlay" @click="$emit('close-modal'),reload()">
        <div class="modal" @click.stop>
          <img class="check" src="" alt="" />
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