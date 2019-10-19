<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{this.$store.state.city}}</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" v-for="item in hot" :key="item.id" @click="handleCityClick(item.name)">
                        <div class="button">{{item.name}}</div>
                    </div>
                </div>
            </div>
            <div class="area" v-for="(item,key) in cities" :key="key" :ref="key">
                <div class="title border-topbottom">{{key}}</div>
                <div class="item-list">
                    <div class="item border-bottom" v-for="innerItem in item" :key="innerItem.id" @click="handleCityClick(innerItem.name)">
                        {{innerItem.name}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
    props: {
        cities: Object,
        hot: Array,
        letter: String
    },
    name: "CityList",
    data() {
        return {
        }
    },
    computed: {
        ...mapState({
        currentCity: 'city'
        })
    },
    methods: {
        handleCityClick (city) {
            this.$store.dispatch('changeCity',city)
            this.$router.push('/')
            console.log(1234)
        },
        
    },
    mounted () {
        const options = {
            scrollY: true, 
            scrollX: false,
            mouseWheel: true,
            click: true,
            taps: true
        }
        this.scroll = new Bscroll(this.$refs.wrapper,options)
    },
    watch: {
        letter () {
            if (this.letter) {
                console.log(this.letter)
                console.log(this.$refs[this.letter][0])
                const element = this.$refs[this.letter][0]
                this.scroll.scrollToElement(element)
            }
        }
    }
}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.border-topbottom
    &:before
        border-color #cccccc
    &:after 
        border-color #cccccc
.border-bottom
    &:before
        border-color #cccccc
.list 
    overflow hidden
    position absolute
    top 1.58rem
    left 0
    right 0
    bottom 0
    .title
        line-height .54rem
        background #eee
        padding-left .2rem
        fontsize .26rem
        color #666
    .button-list
        padding: .1rem .6rem .1rem .1rem
        overflow hidden
        .button-wrapper 
            float left
            width 33.33%
            .button
                margin .1rem
                padding .1rem 0
                text-align center
                border-radius .06rem
                border .02rem solid #cccccc
    .item-list
        .item
            padding-left .2rem
            line-height .76rem
</style>
