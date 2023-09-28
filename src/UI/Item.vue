<template>
    <TransitionGroup  name="cards">
     <div v-for="(card) in cards" :key="card.id" class="card" >
            <div class="products-img">
                <img :src="card.image" class="img">
            </div>
            <div class="card-info">
              <button @click="$emit('deleteFromPurch', card)" v-if="!showBtn" class="delete">×</button>
                <div class="card-text">
                    <h2>{{card.title}}</h2>
                    <p>{{ card.body }}</p>
                </div>
                <div class="price-buy">
                    <p><span>{{card.price}}$</span></p>
                    <button v-if="showBtn" @click="addToPurchase(card)" class="buy-button">BUY NOW</button>
                </div>
            </div>  
        </div>
      </TransitionGroup>
</template>

<script>
export default {
    name: 'Item',
    data() {
      return {
        cardForPurch: {}
      }
    },
    props: {
        cards: {
            type: Array,
            required: true
        },
        showBtn: {
          type: Boolean,
          required: false
        }
    },
    methods: {
      addToPurchase(card) {
          this.cardForPurch = {...card}
          this.cardForPurch.id = crypto.randomUUID()
          this.$emit('addToPurchase', this.cardForPurch)
      }
    }
}
    
</script>

<style scoped>
.card {
  height: 210px;
  width: 325px;
  margin: 50px;
  border-radius: 7px 7px 7px 7px;
  background-color: antiquewhite;
  -webkit-box-shadow: 0px 14px 32px 0px rgba(0, 0, 0, 0.15);
  -moz-box-shadow: 0px 14px 32px 0px rgba(0, 0, 0, 0.15);
  box-shadow: 0px 14px 32px 0px rgba(0, 0, 0, 0.15);
  
}

.products-img {
  height: 210px;
  width: 140px;
  float: left
}

.img {
  height: 210px;
  width: 140px;
  filter: grayscale(100%);
}


.card-info {
  
  float: left;
  min-height: 210px;
  min-width: 185px;
  max-width: 500px;
  border-radius: 0 7px 10px 7px;
  background-color: antiquewhite;
}

.card-text {
  height: 150px;
  width: 140px;
}

.card-text h2 {
  word-break: break-all;
  
  overflow-y: scroll;
  letter-spacing: 0.1em;
  margin: 0 0 0 19px;
  padding-top: 26px;
  font-size: 25px;
  color: black;
  height: 60px
}

.card-text p {
  overflow-wrap: break-word;
  overflow-y: scroll;
  height: 62px;
  margin: 0 0 0 19px;
  color: black;
  line-height: 1.2em;
  font-size: 20px;
  font-weight: lighter;
  
}

.price-buy {
  height: 51px;
  width: 180px;
  margin-top: 8.5px;
  position: relative;
}

.price-buy p {
  display: inline-block;
    position: absolute;
    top: 2.5px;
    height: 50px;
    margin: 0 0 0 15px;
    font-size: 28px;
    font-weight: lighter;
    color: black;
}


.buy-button {
  display: inline-block;
    height: 40px;
    width: 100px;
    margin: 0 40px 0 75px;
    box-sizing: border-box;
    border: transparent;
    border-radius: 60px;
    font-size: 14px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.2em;
    color: antiquewhite;
    background-color: brown;
    cursor: pointer;
    outline: none;
}

.delete {
 font-size: 3rem;
 position: absolute;
 margin-left: 150px;
 background-color: none;
 outline: none;
 background: none;
 border: none;
 color: brown
}

::-webkit-scrollbar {
  outline: none;
  background: none;
}

.cards-move, 
.cards-enter-active,
.cards-leave-active {
  transition: all 0.5s ease;
}

.cards-enter-from,
.cards-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>








