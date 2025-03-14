<template>
  <div id="app">
    <h1>POS System</h1>
    <div class="product-list">
      <h2>Products</h2>
      <ul>
        <li v-for="product in products" :key="product.id">
          {{ product.name }} - ${{ product.price }}
          <button @click="addToCart(product)">Add to Cart</button>
        </li>
      </ul>
    </div>
    <div class="cart">
      <h2>Cart</h2>
      <ul>
        <li v-for="item in cart" :key="item.id">
          {{ item.name }} - ${{ item.price }} x {{ item.quantity }}
          <button @click="removeFromCart(item)">Remove</button>
        </li>
      </ul>
      <p>Total: ${{ total }}</p>
      <button @click="checkout">Checkout</button>
    </div>
  </div>
</template>
 
<script>
export default {
  name: 'App',
  data() {
    return {
      products: [
        { id: 1, name: 'Product 1', price: 10 },
        { id: 2, name: 'Product 2', price: 20 },
        { id: 3, name: 'Product 3', price: 30 },
      ],
      cart: [],
    };
  },
  computed: {
    total() {
      return this.cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
    },
  },
  methods: {
    addToCart(product) {
      const cartItem = this.cart.find(item => item.id === product.id);
      if (cartItem) {
        cartItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(item) {
      const index = this.cart.findIndex(cartItem => cartItem.id === item.id);
      if (index !== -1) {
        if (this.cart[index].quantity > 1) {
          this.cart[index].quantity--;
        } else {
          this.cart.splice(index, 1);
        }
      }
    },
    checkout() {
      alert(`Total amount: $${this.total}`);
      this.cart = [];
    },
  },
};
</script>
 
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
 
.product-list, .cart {
  margin: 20px;
}
 
button {
  margin-left: 10px;
}
</style>
