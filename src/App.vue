<template>
  <div id="app">
    <h1>Item List</h1>

    <item-list @add-to-cart="addToCart"></item-list>

    <h1>Shopping Cart</h1>
    <shopping-cart :cart="cart" @update-quantity="updateQuantity" @remove-from-cart="removeFromCart"></shopping-cart>
  </div>
</template>

<script>
import ItemList from './components/itemList.vue';
import ShoppingCart from './components/shoppingCart.vue';

export default {
  components: {
    ItemList,
    ShoppingCart
  },
  data() {
    return {
      cart: []
    };
  },
  methods: {
    addToCart(item) {
      const existingItemIndex = this.cart.findIndex(i => i.name === item.name);
      if (existingItemIndex !== -1) {
        this.cart[existingItemIndex].quantity++;
      } else {
        this.cart.push({ ...item, quantity: 1 });
      }
    },
    updateQuantity({ index, quantity }) {
      this.cart[index].quantity = quantity;
      if (this.cart[index].quantity <= 0) {
        this.cart.splice(index, 1);
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    }
  }
};
</script>
