<template>
    <div>
        <home-header></home-header>
        <home-swiper :isList="swiperList"></home-swiper>
        <home-icons :isList="iconList"></home-icons>
        <home-recommend :isList="recommendList"></home-recommend>
        <home-weekend :isList="weekendList"></home-weekend>
    </div>
</template>
<script>
import HomeHeader from'./components/header'
import HomeSwiper from'./components/swiper'
import HomeIcons from'./components/icons'
import HomeRecommend from'./components/Recommend'
import HomeWeekend from'./components/Weekend'
import axios from 'axios'
import { mapState } from 'vuex' 
export default {
    name: 'Home',
    components: {
        HomeHeader,
        HomeSwiper,
        HomeIcons,
        HomeWeekend,
        HomeRecommend
    },
    data() {
        return {
            swiperList: [],
            iconList: [],
            weekendList: [],
            recommendList: []
        }
    },
    methods: {
        getHomeInfo () {
            axios.get('/api/index.json')
                 .then(this.getHomeInfoSucc)
        },
        getHomeInfoSucc (res) {
            res = res.data
            if(res.ret && res.data){
                const data = res.data
                 //console.log(data)
                 this.swiperList = data.swiperList
                 this.iconList = data.iconList
                 this.weekendList = data.weekendList
                 this.recommendList = data.recommendList
            }
        }
    },
    mounted () {
        this.getHomeInfo()
    }
}
</script>
<style>

</style>
