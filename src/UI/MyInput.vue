<template>
    <input :value="modelValue" @input="updateInput" type="text" class="input">
</template>

<script>
export default {
    props: {
      modelValue: [String, Number]
    },
    name: 'MyInput',
    methods: {
      updateInput(event) {
         this.$emit('update:modelValue', event.target.value)
      }
    }
}
</script>

<style scoped>
.input {
  outline: none;
  background-color: antiquewhite;
  height: 30px;
  width: 250px;
  border-radius: 5px;
  border: none;
  padding-left: 5px;
  color: grey;
  margin: 5px;
}
</style>