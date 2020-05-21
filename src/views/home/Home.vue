<template>
      <div id="home" class="wrapper">
        <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
        <home-swiper :banners="banners"/>
        <home-recomments :recommends="recommends"/>
        <feature-view/>
        <tab-control class="tab-control"
                   :titles="['流行', '新款', '精选']"
                   @tabClick="tabClick"/>
        <goods-list :goods="goods[currentType].list" />
        <ul>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
          <li>dd</li>
        </ul>
      </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'
import GoodsList from 'components/content/goods/GoodsList'

import HomeSwiper from './childComps/HomeSwiper'
import HomeRecomments from './childComps/HomeRecomments'
import FeatureView from './childComps/FeatureView'

import { getHomeMultidata,getHomeGoods } from "network/home"

export default {
  name: 'Home',
  components: {
    NavBar,
    TabControl,
    GoodsList,
    HomeSwiper,
    HomeRecomments,
    FeatureView
  },
  data() { 
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0,list:[]},
        'new': {page: 0,list:[]},
        'sell': {page: 0,list:[]},
      },
      currentType: 'pop',
    }
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list
    }
  },
  created() {
   this.getHomeMultidata() ;
   this.getHomeGoods('pop');
   this.getHomeGoods('new');
   this.getHomeGoods('sell');
 },
 methods: {
   /*事件监听*/
   tabClick(index) {
     switch(index) {
       case 0:
         this.currentType = 'pop'
         break
       case 1:
         this.currentType = 'new'
         break
       case 2:
         this.currentType = 'sell'
         break
     }
   },
   /*网络请求 */
   getHomeMultidata() {
     getHomeMultidata().then(res => {
     this.banners = res.data.banner.list;
     this.recommends = res.data.recommend.list;
   })
   },
  getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        console.log(res);
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
        })
      }
 }
 }
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 10000;
  }
  .tab-control {
    position: sticky;
    top: 44px;
  }
</style>