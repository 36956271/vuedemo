<template>
  <div class="shop-cart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight':totalCount>0}">
            <i class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></i>
          </div>
          <div class="num" v-show="totalCount>0">{{totalCount}}</div>
        </div>
        <div class="price" :class="{'highlight': totalPrice>0}">￥{{totalPrice}}元</div>
        <div class="desc">另需配送费{{deliveryPrice}}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="payClass">{{payPrice}}</div>
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
        }
      },
      deliveryPrice: {type: Number, default: 0},
      minPrice: {type: Number, default: 0}
    },
    computed: {
      totalCount () {
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })
        return count
      },
      totalPrice () {
        let total = 0
        this.selectFoods.forEach((food) => {
          total += food.price * food.count
        })
        return total
      },
      payPrice () {
        if (this.totalPrice === 0) {
          return `￥${this.minPrice}元起送`
        } else if (this.totalPrice < this.minPrice) {
          let diff = this.minPrice - this.totalPrice
          return `还差￥${diff}配送`
        } else {
          return '结算'
        }
      },
      payClass () {
        if (this.totalPrice < this.minPrice) {
          return 'not-enough'
        } else {
          return 'enough'
        }
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
      background-color: #141d27

      .content-left
        flex 1

        .logo-wrapper
          display inline-block
          position relative
          margin 0 10px
          width 56px
          height 56px
          border-radius 50%
          box-sizing border-box
          background-color: #141d27
          padding: 6px
          top -8px

          .logo
            display inline-block
            vertical-align top
            width 100%
            height 100%
            text-align center
            background-color: #2b343c
            border-radius 50%

            &.highlight
              background-color rgb(0, 160, 220)

            .icon-shopping_cart
              font-size 24px
              color: #80858a
              line-height 46px

              &.highlight
                color white

          .num
            position: absolute
            top: 0
            right: 0
            width: 24px
            height: 16px
            line-height: 16px
            text-align: center
            border-radius: 16px
            font-size: 9px
            font-weight: 700
            color: #fff
            background-color: rgb(240, 20, 20)
            box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)

        .price
          display inline-block
          vertical-align top
          font-size 16px
          font-weight 700
          margin-top: 12px
          padding-right 12px
          line-height 22px
          box-sizing border-box
          border-right: 1px solid rgba(255, 255, 255, 0.1)

          &.highlight
            color #fff

        .desc
          display inline-block
          vertical-align top
          padding-left 12px
          font-size 12px
          font-weight 700px
          line-height 46px
          background-color: #141d27

      .content-right
        flex 0 0 105px
        width 105px

        .pay
          font-size 12px
          font-weight 700
          line-height 46px
          text-align center

          &.not-enough
            background-color: #2b333b

          &.enough
            background-color: #00b43c
            color: #fff
</style>
