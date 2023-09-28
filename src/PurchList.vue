<template> 
        <div v-if="showPurchList" class="purch-list" >
            <Item @deleteFromPurch="deleteFromPurch" :cards="items" v-if="items.length > 0"></Item>
            <div class="nothing" v-else>You didn't choose anything</div>
            <div class="confirm-wrap" v-if="items.length > 0">
                <div class="total">Total: <span>{{ total }}</span></div>
                <button @click="$emit('update:showPostData', true)" class="confirm-button">Confirm</button>
            </div>
            
        </div>

</template>

<script>
export default {
    data() {
        return {
            total: 0,
        }
    },
    props: {
        items: {
            type: Array,
            requred: true
        },
        showPurchList: {
            type: Boolean
        },
        showPostData: {
            type: Boolean
        }

    },
    methods: {
        countTotal() {
            this.total = 0
            this.items.forEach(item => {
                    this.total += +item.price
            })
        },
        deleteFromPurch(card) {
            this.$emit('deleteFromPurch', card)
        },
        

    },
    updated() {
        this.countTotal()
    }
    
   
}
</script>

<style scoped>
.purch-list {
    position: absolute;
    top:0;
    right: 0;
    margin: 20px;
    border-radius: 25px;
    width: 20%;
    height: 500px;
    background-color: antiquewhite;
    overflow-y: scroll;
    overflow-x: hidden;
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
    flex-direction: column;
    z-index: 900;
    
}

::-webkit-scrollbar{
    outline: none;
    background: none;
}

.nothing {
    width: 110%;
    text-align: center;
    margin-top: 10px;
    font-size: 1.5rem;
}
.confirm-wrap {
    width: 110%; 
    display: flex;
    grid-gap:20px;
    margin-bottom: 10px;
    justify-content: center;
    align-items: center;
}

.total {
    font-size: 1.5rem;
}
span {
    color: brown;
}

.confirm-button {
    height: 40px;
    width: 100px;
    border: transparent;
    border-radius: 60px;
    font-size: 14px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.2em;
    color: antiquewhite;
    background-color: brown;
    outline: none;
}
</style>