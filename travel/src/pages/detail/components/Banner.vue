<template>
  <div>
    <div class="banner" @click="handleBannerClick">
      <img class="banner-img" src="https://imgs.qunarzz.com/sight/p0/201404/23/04b92c99462687fa1ba45c1b5ba4ad77.jpg_710x360_075ec9d6.jpg" />
      <div class="banner-info">
        <div class="banner-title">
          大连圣亚海洋世界（AAAA景区）
        </div>
        <div class="banner-number">
          <span class="iconfont banner-icon">&#xe629;</span>
          39
        </div>
      </div>
    </div>
    <common-gallery 
    :imgs="gallaryImgs" 
    v-show="showGallery"
    @close="handleGallaryClick"
    ></common-gallery>
  </div>
</template>

<script>
import CommonGallery from 'common/gallery/Gallery'
export default {
  name: 'DetailBanner',
  data () {
    return {
      showGallery: false
  }
  },
  methods: {
    handleBannerClick () {
      this.showGallery = true
    },
    handleGallaryClick () {
      this.showGallery = false
    }
  },
  components: {
    CommonGallery
  }
}
</script>

<style lang="stylus" scoped>
  .banner
    position: relative
    overflow: hidden
    height: 0
    padding-bottom: 50.7%
    .banner-img
      width: 100%
    .banner-info
      line-height: .6rem
      height: .6rem
      display: flex
      position: absolute
      left: 0
      right: 0
      bottom: 0
      color: #fff
      background-image: linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8))
      .banner-title
        flex: 1
        font-size: .32rem
        padding: 0 .2rem
      .banner-number
        height: .32rem
        line-height: .32rem
        margin-top: .14rem
        padding: 0 .4rem
        background: rgba(0, 0, 0, 0.6)
        border-radius: .2rem
        font-size: .24rem
        .banner-icon
          font-size: .24rem
          margin-right: .05rem
</style>
