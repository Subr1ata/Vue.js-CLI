<template>
  <!-- eslint-disable vue/no-use-v-if-with-v-for -->
  <transition-group name="fade" tag="div" @beforeEnter="beforeEnter" @enter="enter" @leave="leave">
    <div class="row d-none mb-3" v-for="item in products" :key="item.id" v-if="item.price<=Number(maximum)" data-index="index">
        <div class="col-1 m-auto">
          <button class="btn btn-info mx-3" @click="$emit('add',item)">+</button>
        </div>
        <div class="col-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.name">
        </div>
        
        <div class="col">
          <h3 class="text-info">{{ item.name }}</h3>
          <p class="mb-0">{{ item.description }}</p>
          <div class="h5 float-right mx-4">
            <price :precision="2" :value="Number(item.price)" :sign="'&euro;'" :conversion="0.87"></price>
          </div> 
        </div>
    </div>
  </transition-group>
</template>

<script>
import price from './Price.vue'

export default {
    name:"product-list",
    components:{
        price
    },
    props:['products','maximum'],
    methods:{
        beforeEnter:function(el){
            el.className = 'd-none';
        },
        enter:function(el){
            let delay = el.dataset.index * 100;
            setTimeout(()=>{
                el.className = "row d-flex animate__animated animate__fadeInRight";
            },delay);
        },
        leave:function(el){
            let delay = el.dataset.index * 100;
            setTimeout(()=>{
                el.className = "row d-flex animate__animated animate__fadeOutRight";
            },delay);
        }
    }
}
</script>

<style>

</style>