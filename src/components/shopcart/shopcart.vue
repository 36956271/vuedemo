<template>
  <div class="shop-cart">123</div>
</template>

<script>
  export default {
    name: 'shopcart',
    props: {
      selectFoods: {
        type: Array,
        default () {
          return []
        },
        deliveryPrice: {type: Number, default: 0},
        minPrice: {type: Number, default: 0}
      }
    }
  }
</script>

<style lang="stylus" rel="stylussheet/stylus">

</style>
