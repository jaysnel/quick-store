<template>
  <div class="HomePage">
      <h1 class="text-center">Quick-Store</h1>
      <b-button variant="success" class="btn" @click="addOne();listData()">Store State</b-button>

      <div class="store-front-items">
          <div v-for="item in dataList" :key="item.id">
              <h4>{{ item.name }}</h4>
              <p>{{ item.price }}</p>
              <p>{{ item.condition }}</p>
          </div>
      </div>
  </div>
</template>

<script>
import storeInventory from '../data.js'

export default {
  name: 'HomePage',
  data() {
      return {
          dataList: storeInventory
      }
  },
  props: {
    msg: String
  },
  methods: {
      listData() {
          console.log(this.dataList)
      },
      addOne() {
      this.$store.state.count++
      console.log(this.$store.state.count)
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
}

@media(min-width: 768px) {
    .store-front-items {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-gap: 2px;

        width: 80%;
        margin: auto;
    }
}
</style>
