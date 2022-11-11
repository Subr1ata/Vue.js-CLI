<template>
  <span>{{this.prefix + Number.parseFloat(Number(this.value)*this.conversion).toFixed(this.precision)}}</span>
</template>

<script>
export default {
    name:"PriceComponent",
    props:{
    value:Number,
    prefix:{
      type:String,
      default:'$'
    },
    conversion:{
      type:Number,
      default:1
    },
    precision:{
      type:Number,
      default:2
    },
    country:{
      type:String,
      default:'Euro'
    }
  },
}
</script>

<style>

</style>