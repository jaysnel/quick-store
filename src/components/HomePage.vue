<template>
  <div class="HomePage">
      <h1 class="text-center">Quick-Store</h1>
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
}

.store-front-items div img {
  max-width: 100%;
  width: 85px;
}

@media(min-width: 768px) {
    .store-front-items {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
        width: 80%;
        margin: auto;
    }
}
</style>
