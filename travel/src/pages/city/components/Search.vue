<template>
  <div>
    <div class="search">
      <input  v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音" />
    </div>
    <div 
      class="search-content" 
      ref="seaech"
      v-show="keyword"
    >
      <ul>
        <li 
        class="search-item border-bottom" 
        v-for="item of list" 
        :key="item.id"
        @click="handleCityClick(item.name)"
        >{{item.name}}</li>
        <li class="search-item border-bottom" v-show="hasNoData">
          没有找到匹配数据
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import {mapMutations} from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  computed: {
    hasNoData () {
      return  !this.list.length
    }
  },
  watch: {
    keyword () {
      // 函数节流
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  methods: {
    handleCityClick(city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.seaech)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
    .search 
      height .72rem
      background $bgColor
      padding 0 .1rem
      .search-input
        box-sizing border-box
        width 100%
        height .62rem
        padding 0 .1rem
        line-height .62rem
        text-align center
        border-radius .06rem
        color #666
    .search-content
      overflow: hidden
      background: #eee
      position: absolute
      top: 1.58rem
      left: 0
      right: 0
      bottom: 0
      z-index: 1
      .search-item
        line-height: .62rem
        color: #666
        background: #fff
        padding-left: .2rem
</style>