<template>
    <div class="header">
        <div class="title">CHOOSE ITEM</div>
        <MyInput :value="modelValue" @input="updateValue" class="input" placeholder="Search..."></MyInput>
        <MyButton @click="show = true">Create Item</MyButton>
        <MySelect @getValue="getValue"></MySelect>
        <MyButton @click="clearLocal"> Clear Local Storage </MyButton>
        <ItemModal @createItem="createItem" v-model:show="show"></ItemModal>
        <div @mouseover="showPurchList = true" class="list">
          <div class="button-list">
            <div class="counter"> {{purchasedItems.length}} </div>
          </div>
       </div>
       <PurchList 
          @deleteFromPurch="deleteFromPurch" 
          @mouseleave="showPurchList = false" 
          v-model:showPurchList="showPurchList" 
          v-model:showPostData="showPostDataModal"
          :items="purchasedItems">
        </PurchList>
       <PostDataModal @clearList="this.$emit('clearList', purchasedItems)" :purchItems="purchasedItems"   v-if="showPostDataModal" v-model:showPostData="showPostDataModal"></PostDataModal>
    </div>
    
    
</template>




<script>
import PostDataModal from './PostDataModal.vue'
import ItemModal from './ItemModal.vue'
import MySelect from './MySelect.vue'
import PurchList from './PurchList.vue'
export default {
  props: {
    modelValue: [String],
    purchasedItems: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      show: false,
      showPurchList: false,
      showPostDataModal: false
    }
  },
  methods: {
    createItem(item) {
      this.$emit('createItem', item)
    },
    updateValue(event) {
      this.$emit('update:modelValue', event.target.value)
    },
    deleteFromPurch(card) {
      this.$emit('deleteFromPurch', card)
    },
    getValue(event) {
      this.$emit('getValue', event)
    },
    afterSubmit(items) {
      this.$emit('afterSubmit', items)
    },
    clearLocal() {
      localStorage.clear()
    }
  },
  components: { ItemModal, PurchList, MySelect, PostDataModal }
}
</script>


<style scoped>
.header {
  margin: 20px;
}

.title{ 
  color:antiquewhite;
  font-size: 6rem;
}


.list {
  width: 50px;
  height: 50px;
  background-color: antiquewhite;
  border-radius: 50px;
  right: 0;
  top: 0;
  position: absolute;
  margin: 10px;
}

.counter {
  color: antiquewhite;
  text-align: center;
  padding-top: 6px;
  width: 35px;
  height: 35px;
  background-color: brown;
  border: 1.5px solid antiquewhite;
  border-radius: 50px;
  margin-top: 20px;
 
}

</style>