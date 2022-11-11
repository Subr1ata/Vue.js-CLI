<template>
  <div id="app" class="container mt-5">
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle="sliderStatus"></navbar>
    <h1>My Shop</h1>
    <priceslider :sliderStatus="sliderStatus" :maximum.sync="maximum"/>
    <productlist :products="products" :maximum="maximum" @add="addProduct"/>
  </div>
</template>

<script>
import navbar from './components/Navbar.vue'
import productlist from './components/ProductList.vue'
import priceslider from './components/Priceslider.vue'

export default {
  name: 'App',
  data:function(){
    return{
      sliderStatus:true,
      cart:[],
      maximum: 99,
      products: null
    }
  },
  mounted: 
    function () {
      fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data
      });
    },
  components: {
    productlist,
    priceslider,
    navbar
  },
  computed:{
    sliderState:function(){
      return this.sliderStatus? 'd-flex':'d-none';
    },
    cartTotal:function(){
      let sum=0;
      for(let key in this.cart){
        sum = sum + (this.cart[key].product.price * this.cart[key].qty);
      }
      return sum;
    },
    cartQty:function(){
      let qty=0;
      for(let key in this.cart){
        qty = qty + (this.cart[key].qty);
      }
      return qty;
    }
  },
  methods:{
    addProduct:function(product){
      var whichProduct;
      var existing = this.cart.filter(function(item,index){
        if(item.product.id == Number(product.id)){
          whichProduct = index;
          return true;
        }else{
          return false;
        }
      })
      if(existing.length){
        this.cart[whichProduct].qty++;
      }else{
        this.cart.push({product:product, qty:1});
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
