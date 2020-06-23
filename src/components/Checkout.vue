<template>
  <div>
    <h1>Checkout Page</h1>

    <div v-for="item in cartItems" :key="item.id" class="shoppingCartItems">
        <span>{{ item.name }}</span>
        <span>${{ item.price.toFixed(2) }}({{ item.count }})</span>
        <b-button variant="danger" class="remove-button" size="sm" @click="removeFromCart(item)">Remove</b-button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Checkout',
    data() {
        return {
            cartItems: this.$store.state.shoppingCart
        }
    },
    methods: {
        showCart() {

        }
    }
}
</script>

<style scoped>

</style>