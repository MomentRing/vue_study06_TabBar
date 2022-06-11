<template>
  <div>
    <MyHeader
      :title="'tabbar案例'"
      :color="'white'"
      :background="'skyblue'"
    ></MyHeader>
    <div class="main">
      <keep-alive>
        <Component :is="comName"></Component>
      </keep-alive>
    </div>
    <MyTabBar :arr="tabList" @changeCom="comFn"></MyTabBar>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyTabBar from './components/MyTabBar.vue'
import MyGoodsList from './components/views/MyGoodsList.vue'
import MyGoodsSearch from './components/views/MyGoodsSearch.vue'
import MyUserInfo from './components/views/MyUserInfo.vue'
export default {
  created() {},
  data() {
    return {
      tabList: [
        {
          iconText: 'icon-shangpinliebiao',
          text: '商品列表',
          componentName: 'MyGoodsList',
        },
        {
          iconText: 'icon-sousuo',
          text: '商品搜索',
          componentName: 'MyGoodsSearch',
        },
        {
          iconText: 'icon-user',
          text: '我的信息',
          componentName: 'MyUserInfo',
        },
      ],
      comName: 'MyGoodsList',
    }
  },
  methods: {
    comFn(cn) {
      this.comName = cn
    },
  },
  computed: {},
  watch: {},
  filters: {},
  components: {
    MyHeader,
    MyTabBar,
    MyGoodsList,
    MyGoodsSearch,
    MyUserInfo,
  },
}
</script>

<style scoped>
.main {
  padding-top: 45px;
  padding-bottom: 51px;
}
</style>
