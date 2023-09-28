<template>
    <div class="modal-item"  v-if="show" @click.stop="hideModal">
        <div @click.stop class="modal-item-content" >
            <MyInput v-model="item.title" name="title" placeholder="Enter title"></MyInput>
            <MyInput v-model="item.body" name="body" placeholder="Enter description"></MyInput>
            <MyInput v-model="item.price" name="price" placeholder="Enter price"></MyInput>
            <MyInput v-model="item.image" name="img" placeholder="Enter link of image"></MyInput>
            <MyButton style="margin-left: 5px" @click="createItem"> Create </MyButton>
            <div style="color: antiquewhite" v-if="isDataEnter">Enter required data</div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            item: {
                title: '',
                body: '',
                price: '',
                image: '',
            }, 
            isDataEnter: false
        }
    },
    props: {
        show: {
            type: Boolean
        },
    },
    methods: {
        hideModal() {
            this.$emit('update:show', false)
        },
        createItem() {
            if(this.item.title.trim() == '' || this.item.body.trim() == '' || this.item.price.match(/[^0-9 ]/g, '') || this.item.image.trim() == '') {
                this.isDataEnter = true
                setTimeout(() => {
                    this.isDataEnter = false
                }, 1000)
                return
            }
            this.item.id = crypto.randomUUID()
            this.$emit('createItem', this.item)
            this.$emit('update:show', false)
            this.item.title = ''
            this.item.body = ''
            this.item.price = ''
            this.item.image = ''
        }
    }
}
</script>

<style scoped>
.modal-item {
    
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display:flex;
    z-index: 999;
    
    
}

 .modal-item-content {
    margin: auto;
    background: brown;
    border-radius: 12px;
    min-height: 50px;
    min-width: 300px;
    padding: 20px;
    display: flex;
    flex-direction: column;

} 
</style>