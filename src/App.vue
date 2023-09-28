<template>
  <Head 
      @clearList="clearList"
     @getValue="getValue" 
     @deleteFromPurch="deleteFromPurch" 
     :purchasedItems="purchasedItems" 
     v-model="searchQuery" 
     @createItem="createItem">
  </Head>

  <Main  @addToPurchase="addToPurchase" :cards="sortItemsByName"></Main>
</template>

<script>
import axios from 'axios'
import Main from './Main.vue'
import Head from './Head.vue'
export default {
  data() {
    return {
      items: [],
      purchasedItems: [],
      searchQuery: '',
      selectValue: '',
      localStor: JSON.parse(localStorage.getItem('items')) || []
    }
  },
  methods: {
    async fetchItems() {
      try {
        const response = await axios.get('server.json')
        this.items = response.data
        this.items.forEach(item => item.id = crypto.randomUUID())

        if(localStorage.getItem('items')) {
          this.items = this.items.concat(JSON.parse(localStorage.getItem('items')))
        }
        
        
      } catch(e) {
        alert('Wrong!')
      } 
    }, 
    createItem(item) {
      const newItem = {...item}
      this.items.push(newItem)
      console.log(this.localStor)
      this.localStor.push(newItem)
      localStorage.setItem('items', JSON.stringify(this.localStor))
    },
    addToPurchase(card) {
      this.purchasedItems.push(card)
    },
    deleteFromPurch(card) {
      this.purchasedItems = this.purchasedItems.filter(item => item.id !== card.id)
    },
    getValue(event) {
      this.selectValue = event
    },
    clearList() {
      this.purchasedItems = []
    }
    
  },
  mounted() {
    this.fetchItems()
    
  },
  computed: {
    sortItemsByPrice() {
      if(this.selectValue === '') {
        return this.items
      } 
      if(this.selectValue === 'incr') {
        return [...this.items].sort((a, b) => +a.price - +b.price)
      }
      if(this.selectValue === 'decr') {
        return [...this.items].sort((a, b) => +b.price - +a.price)
      }  
    },
    sortItemsByName() {
        return this.sortItemsByPrice.filter(item => item.title.toLowerCase().trim().includes(this.searchQuery.toLowerCase().trim()))
    }
  },
  components: {Head, Main}
}
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
 
}

body {
  background: brown;
}

</style>