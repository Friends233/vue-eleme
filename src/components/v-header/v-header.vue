<template>
  <div class="header" @click="showDetail">
    <div class="conttent-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟到达
        </div>
        <div class="support" v-if="seller.supports">
          <support-ico :size=1 :type="seller.supports[0].type"></support-ico>
          <span class="text">
            {{seller.supports[0].description}}
          </span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bullentin-wrapper">
      <span class="bulletin-title"></span><span class="bullentin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img width="100%" height="100%" :src="seller.avatar">
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import SupportIco from '../support-ico/support-ico'

  export default {
    name: 'v-header',
    props: {
      seller: {
        type: Object,
        default () {
          return {}
        }
      }
    },
    data () {
      return {
        detailShow: false
      }
    },
    methods: {
      showDetail () {
        this.headerDetailComp = this.headerDetailComp || this
          .$createHeaderDetail({
            $props: {
              seller: 'seller'
            }
          })
        this.headerDetailComp.show()
      }
    },
    components: {
      SupportIco
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/mixin"
  @import "~common/stylus/variable"

  .header
    color $color-white
    overflow hidden
    background $color-background-ss
    position relative
    .conttent-wrapper
      position relative
      padding 24px 12px 18px 24px
      font-size 0
      .avatar
        display inline-block
        img
          border-radius 2px
      .content
        display inline-block
        vertical-align top
        margin-left 16px
        .title
          margin 2px 0 8px 0
          .brand
            display inline-block
            vertical-align top
            width 30px
            height 18px
            bg-image('brand')
            background-size 30px 18px
            background-repeat no-repeat
          .name
            margin-left 6px
            font-size $fontsize-large
            font-weight bold
            line-height 18px
        .description
          font-size $fontsize-small
          font-weight 200
          line-height 12px
          margin-bottom 10px
        .support
          .support-ico
            vertical-align top
            margin-right 4px
          .text
            line-height 12px
            font-size $fontsize-small-s
      .support-count
        position absolute
        right 12px
        bottom 14px
        padding 0 8px
        height 24px
        line-height 24px
        border-radius 14px
        background $color-background-sss
        text-align center
        .count
          font-size $fontsize-small-s
          vertical-align top
        .icon-keyboard_arrow_right
          font-size $fontsize-small-s
          line-height 24px
          margin-left 2px
    .bullentin-wrapper
      position relative
      height 28px
      line-height 28px
      padding 0 22px 0 12px
      white-space nowrap
      overflow hidden
      text-overflow ellipsis
      background $color-background-sss
      .bulletin-title
        display inline-block
        vertical-align top
        width 22px
        height 12px
        bg-image('bulletin')
        background-size 22px 12px
        background-repeat no-repeat
        margin-top 8px
      .bullentin-text
        vertical-align top
        font-size $fontsize-small-s
        margin 0 4px
      .icon-keyboard_arrow_right
        position absolute
        font-size $fontsize-small-s
        right 12px
        top 8px
    .background
      position absolute
      top 0
      left 0
      width 100%
      height 100%
      z-index -1
      filter blur(10px)
</style>
