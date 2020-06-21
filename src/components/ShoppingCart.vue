<template>
    <div>
        <b-button v-b-modal.modal-1 @click="getTotalAmount()">Cart</b-button>

        <b-modal id="modal-1" title="Shopping Cart">
            <div id="ShoppingCartContainer">
                <div>
                    <div v-for="item in cart" :key="item.id" class="shoppingCartItems">
                        <span>{{ item.name }}</span>
                        <span>${{ item.price.toFixed(2) }}({{ item.count }})</span>
                    </div>
                </div>
                <div class="total">
                    Total: ${{ totalAmount.toFixed(2) }}
                </div>
            </div>
        </b-modal>
    </div>
</template>

<script>
export default {
    name: 'ShoppingCart',
    data() {
        return {
            cart: this.$store.state.shoppingCart,
            totalAmount: 0
        }
    },
    methods: {
        getTotalAmount() {
            this.totalAmount = 0; //reset price to keep updated
            this.cart.forEach(el => {
                const amount = el.price * el.count;
                this.totalAmount += amount;
            });
        }
    },
    mounted() {
    }
}
</script>

<style scoped>

#ShoppingCartContainer {
    display: grid;
    grid-template-columns: 2fr 1fr;
    align-content: end;
}

.shoppingCartItems {
    display: grid;
    grid-template-columns: 1fr 1fr;
}

.total {
    color: #ff0000;
}

</style>