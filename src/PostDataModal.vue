<template>
    <div @click.stop="$emit('update:showPostData', false)" class="post-data-modal">
        <div @click.stop class="modal-content">
            <form>
                <MyInput v-model="postData.name" placeholder="Enter your name..."></MyInput>
                <MyInput v-model="postData.phone" placeholder="Enter your phone..."></MyInput>
                <MyInput v-model="postData.mail" placeholder="Enter your mail..."></MyInput>
                <MyButton @click="postFetch" style="margin-right: 10px;" type="submit">Submit</MyButton>
                <div style="color: antiquewhite" v-if="isDataEnter">Enter required data</div>
            </form>
        </div>
    </div>
</template>

<script>


export default {

    props: {
        showPostData: {
            type: Boolean
        },
        purchItems: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            postData: {
                name: '',
                phone: '',
                mail: '',
                items: this.purchItems
            },
            isDataEnter: false,
            clearPurchList: []
        }
    },
    methods: {
        postFetch(event) {
            event.preventDefault()
            if(this.postData.name.trim() === '' || this.postData.phone.match(/[^0-9 ]/g, '') || this.postData.mail.trim() === '') {
                this.isDataEnter = true
                setTimeout(() => {
                    this.isDataEnter = false
                }, 1000)
                return
            }
            fetch('db.json', {
                method: "POST",
                body: JSON.stringify(this.postData)
            }).then(() => {
                this.$emit('update:showPostData', false)
                for(let key in this.postData) {
                    key = ''
                }
                this.$emit('clearList', this.clearPurchList)
            }).catch((error) => {
                console.log(error)
            }).finally (() => {
                
            })
            
        }
    }
    
}
</script>

<style scoped>
.post-data-modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    z-index: 999;
    display: flex;
    justify-content: center;
}

.modal-content {
    background-color: brown;
    width: 20%;
    height: 250px;
    margin: auto;
    border-radius:25px ;
}
form {
    width: 100%;
    height: 250px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    grid-gap: 10px
}
</style>