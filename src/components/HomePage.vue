<template>
  <div class="HomePage">
      <h1 class="text-center">Simple Market</h1>
      <ViewShoppingCart />
      <div class="store-front-items">
          <div v-for="item in dataList" :key="item.id">
            <img v-bind:src="item.picture">
              <h4>{{ item.name }}</h4>
              <p>${{ item.price.toFixed(2) }}</p>
              <p>{{ item.condition }}</p>
              <b-button variant="danger"  @click="addToCart(item)">Add To Cart</b-button>
          </div>
      </div>

  </div>
</template>

<script>
import storeInventory from '../data.js'
import ViewShoppingCart from './ViewShoppingCart.vue'

export default {
  name: 'HomePage',
  data() {
      return {
          dataList: storeInventory,
          cart: this.$store.state.shoppingCart,
          numberOfItemsInCart: this.$store.state.numberOfItemsInCart
      }
  },
  components: {
    ViewShoppingCart
  },
  props: {
    msg: String
  },
  methods: {
      listData() {
          console.log(this.dataList)
      },
    addToCart(item) {
      if(this.$store.state.shoppingCart.length === 0) {
          item.count++;
          this.$store.state.shoppingCart.push(item);
      } else {
          let found = false;
          for(let i = 0; i < this.$store.state.shoppingCart.length; i++) {
            if(item.name == this.$store.state.shoppingCart[i].name) {
              this.$store.state.shoppingCart[i].count++
              found = true;
              break;
            }
          }
          if(!found) {
            item.count++;
            this.$store.state.shoppingCart.push(item);
          }
      }
      this.updateCartItemCount();
    },
    updateCartItemCount() {
        this.$store.state.numberOfItemsInCart = 0; //reset amount to keep updated

        this.cart.forEach(el => {
            this.$store.state.numberOfItemsInCart += el.count;
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.HomePage {
  width: 80%;
  margin: auto
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.store-front-items div {
    background: #D0734C;
    border-radius: 3px;
    margin: 5px 5px;
    padding: 15px;
}

.store-front-items div:nth-child(1) {
    background: #D0734C;
}
.store-front-items div:nth-child(2) {
    background: #DB854E;
}
.store-front-items div:nth-child(3) {
    background: #EABB59;
}
.store-front-items div:nth-child(4) {
    background: #C65B41;
}
.store-front-items div:nth-child(5) {
    background: #9BA25A;
}
.store-front-items div:nth-child(6) {
    background: #B48A61;
}
.store-front-items div:nth-child(7) {
    background: #CFC269;
}
.store-front-items div:nth-child(8) {
    background: #B76BA0;
}
.store-front-items div:nth-child(9) {
    background: #6EBACB;
}

.store-front-items div p {
  padding: 0;
  margin: 0;
}

.store-front-items div img {
  max-width: 100%;
  width: 85px;
}

@media(min-width: 768px) {
    .store-front-items {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        width: 80%;
        margin: auto;
    }
}

@media(max-width: 1100px) and (min-width: 768px) {
    .store-front-items {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        width: 80%;
        margin: auto;
    }
}
</style>
