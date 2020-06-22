<template>
    <div>
        <b-button v-b-modal.modal-1 @click="getTotalAmount()">View Cart ({{  this.$store.state.numberOfItemsInCart }})</b-button>
        <b-modal id="modal-1" title="Shopping Cart" ok-only ok-title="Close">
            <div id="ShoppingCartContainer">
                <div>
                    <div v-for="item in cart" :key="item.id" class="shoppingCartItems">
                        <span>{{ item.name }}</span>
                        <span>${{ item.price.toFixed(2) }}({{ item.count }})</span>
                        <b-button variant="danger" class="remove-button" size="sm" @click="removeFromCart(item)">Remove</b-button>
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
    name: 'ViewShoppingCart',
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
        },
        removeFromCart(item) {
            this.cart.forEach((el, index) => { if(item.id === el.id) {el.count = 0; this.cart.splice(index, 1);} })
            this.getTotalAmount();
            this.updateCartItemCount();
        },
        updateCartItemCount() {
            this.$store.state.numberOfItemsInCart = 0; //reset amount to keep updated

            this.cart.forEach(el => {
                this.$store.state.numberOfItemsInCart += el.count;
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
    align-content: end;
}

.shoppingCartItems {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}

.total {
    color: #ff0000;
}

.remove-button {
    padding: 0;
    margin: 1px 0;
}

</style>