<template>
    <button class="button">
        <slot></slot>
    </button>
</template>

<script>
export default {
    
    name: 'MyButton'
}
</script>

<style scoped>
.button {
  height: 30px;
  width: 250px;
  margin-left: 10px;
  background: antiquewhite;
  border: none;
  outline: none;
  border-radius: 5px;
  color: brown;
  
}
</style>