<template>
      <header class="top-bar spread">
        <nav class="top-bar-nav">
          <router-link to="/" class="top-bar-link">
            <i class="icofont-spoon-and-fork"></i>
            <span>Home</span>
          </router-link>
          <router-link to="/products" class="top-bar-link">
            <span>Products</span>
          </router-link>
          <router-link to="/past-orders" class="top-bar-link">
            <span>Past Orders</span>
          </router-link>
        </nav>
        <div @click="toggleCartContainer(true)" class="top-bar-cart-link">
          <i class="icofont-cart-alt icofont-1x"></i>
          <span>Cart ({{Object.keys(cart).length}})</span>
        </div>
      </header>
  <router-view :inventory="inventory" :addToCart="addToCart"/>

  <CartContainer
    v-if="showCartContainer"
    :toggle="toggleCartContainer"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>

<script>
import CartContainer from './components/CartContainer.vue'
import food from './food.json'

export default {
  components: {
    CartContainer
  },
  data () {
    return {
      showCartContainer: true,
      inventory: food,
      cart: {}
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleCartContainer (value) {
      this.showCartContainer = value
    },
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>
<!--
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
 -->
