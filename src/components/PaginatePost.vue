<script setup>

defineProps(['inicio', 'fin', 'maxPage'])


const emit = defineEmits(['next', 'previus'])

const siguientePagina = ()=>{
  emit('next')
}

const anteriorPagina = ()=>{
  emit('previus')
}

</script>


<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    
    <button 
      @click="anteriorPagina" 
      type="button" 
      class="btn btn-outline-secondary"
      :disabled="inicio <= 0"
      >Previus {{ inicio+1 }}
    </button>

    <button 
      @click="siguientePagina" 
      type="button" 
      class="btn btn-outline-secondary"
      :disabled="fin >= maxPage"
      >Next {{ fin }}
    </button>
  
  </div>
</template>