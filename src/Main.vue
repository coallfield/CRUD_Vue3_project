<template>
    <section class="main">
        <Item @addToPurchase="addToPurchase" :showBtn="showBtn" :cards="cards"></Item>
    </section>
</template>

<script>
export default {
    data(){
        return {
            showBtn: true
        }
    },
    props: {
        cards: {
            type: Array,
            required: true
        },
    },
    methods: {
        addToPurchase(card) {
            this.$emit('addToPurchase', card)
        }
    },
    
    

}
</script>

<style scoped>
.main{
    display:inline-flex;
    flex-wrap: wrap;
}
</style>