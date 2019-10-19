<template>
    <div>
       <div class="banner" @click="handleBannerClick">
           <img :src="bannerImg" alt="" class="banner-img">
           <div class="banner-info">
               <div class="banner-title">
                   {{this.sightName}}
               </div>
               <div class="banner-number">
                    <span class="banner-icon iconfont">&#xe692;</span>
                    {{this.bannerImgs.length}}
               </div>
           </div>
       </div>
       <fade-animiation>
           <common-gallery :imgs="bannerImgs" @close="handleGllaryClose" v-show="shwoGallary"></common-gallery>
       </fade-animiation>
    </div>
</template>
<script>
import CommonGallery from '../../../common/gallary/gallary'
import FadeAnimiation from '../../../common/fade/fadeAnimiation'
export default {
    name:'DetailBanner',
    components: {
        CommonGallery,
        FadeAnimiation
    },
    props:{
        sightName: String,
        bannerImg: String,
        bannerImgs: Array
    },
    data() {
        return {
            shwoGallary: false
        }
    },
    methods: {
        handleBannerClick () {
            this.shwoGallary = true
        },
        handleGllaryClose(){
            this.shwoGallary = false
        }
    }
}
</script>
<style lang="stylus" scoped>
 .banner
    position relative
    overflow hidden
    height 0
    padding-bottom 55%
    .banner-img 
        width 100%
    .banner-info
        display flex
        position absolute
        left 0
        right 0
        bottom 0
        color #fff
        background-image: linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8))
        .banner-title
            flex 1
            font-size .32rem
            padding 0 .2rem
        .banner-number
            height .32rem
            line-height .32rem
            margin-top 0
            padding 0 .4rem
            border-radius .2rem
            background-color rgba(0,0,0,.8)
            font-size .24rem
            .banner-icon
                 font-size .24rem
            
</style>
