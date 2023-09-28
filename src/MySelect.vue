<template>
    <select @change="sendValue" value="Filter">
        <option class="opt" disabled>Filter</option>
        <option value="incr" class="opt"> Price increase </option>
        <option value="decr" class="opt"> Price decrease</option>
    </select>

</template>

<script>
export default {
    methods: {
        sendValue(event) {
            this.$emit('getValue', event.target.value)
        }
    }
}
</script>

<style scoped>
select {
  height: 30px;
  width: 250px;
  margin-left: 10px;
  background: antiquewhite;
  border: none;
  outline: none;
  border-radius: 5px;
  color: brown;
}

.opt {
    text-align: center;
}
</style>