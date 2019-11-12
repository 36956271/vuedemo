<template>
  <div class="shop-cart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo">
            <i class="icon-shopping_cart"></i>
          </div>
          <div class="num"></div>
        </div>
        <div class="price">￥{{totalPrice}}元</div>
        <div class="desc">另需配送费{{deliveryPrice}}</div>
      </div>
      <div class="content-right">
        <div class="pay">{{payDesc}}</div>
      </div>
    </div>
  </div>
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
    },
    computed: {
      totalPrice () {
        return 20
      },
      payDesc () {
        return '20元'
      }
    }
  }
</script>

<style lang="stylus" rel="stylussheet/stylus">
  .shop-cart
    position fixed
    bottom 0px
    left 0px
    z-index 50px
    width 100%
    height 46px

    .content
      display flex
      font-size 0
      color: rgba(255, 255, 255, 0.4)
      background-color black

      .content-left
        display inline-block
        flex 1

      .content-right
        display inline-block
        flex 0 0 105px

        .pay
          width 105px
          font-size 12px
          font-weight 700
          line-height 46px
          text-align center
</style>
