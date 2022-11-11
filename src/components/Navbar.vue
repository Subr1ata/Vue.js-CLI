<template>
    <nav class="navbar navbar-light fixed-top">
      <div class="navbar-text mr-auto d-flex">
        <button class="btn btn-sm btn-outline-success" @toggle="$emit('')">
            <i class="fa fa-dollar-sign"></i>
            <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
        </button>
        <div class="dropdown ml-2" v-if="cart.length>0">
            <button class="btn btn-success btn-sm dropdown-toggle" id="cartDropdown" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"> 
             <span class="badge badge-pill badge-light">{{cartQty}}</span>
               <i class="fa fa-shopping-cart mx-2"></i>
               <price :value="Number(cartTotal)"></price>
            </button>
        <div class="dropdown-menu dropdown-menu-right" aria-labelledby="cartDropdown">
            <div v-for="(item,index) in cart" :key="index">
              <div class="dropdown-item-text text-nowrap text-right">
                <span class="badge badge-pill badge-warning align-text-top mr-1">{{item.qty}}</span>
                  {{item.product.name}}
                  <b>{{(item.qty * item.product.price) | currency}}</b>
                  <button @click.stop="deleteItem(index)" class="badge badge-danger text-light">-</button>
              </div>
            </div> 
          </div>
        </div>
      </div>
    </nav>
</template>

<script>
import price from './Price.vue'
// import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';

export default {
    name:'nav-bar',
    props:['cart','cartQty','cartTotal'],
    components:{
        price
    }
};
</script>

<style>

</style>