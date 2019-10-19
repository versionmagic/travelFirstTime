<template>
    <div>
        <div class="search">
            <input type="text" class="search-input"
                v-model="keyworld" 
                placeholder="请输入城市的名称或拼音">
        </div>
        <div class="search-content" v-show="keyworld" ref="search">
             <ul>
                <li class="search-item boder-bottom" v-for="item in list" :key="item.id" @click="handleCityClick(item.name)">{{item.name}}</li>
                <li class="search-item border-bottom" v-show="hasNodata"  >
                    没有找到匹配数据
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default{
    name: 'CitySearch',
    props: {
        cities: Object
    },
    data () {
        return {
            list: [],
            keyworld: '',
            timer: null
        }
    },
    methods: {
        Info(){
             //console.log(this.$refs.search)
        },
        handleCityClick(city) {
            this.$store.dispatch('changeCity',city)
            this.$router.push('/')
            console.log(city)
        }
    },
    computed: {
        hasNodata () {
            return !this.list.lenght
        }
    },
    watch: {
        keyworld () {
            if(this.timer){
                clearTimeout(this.timer)
            }
            if(!this.keyworld){
                this.list = []
                return
            }
            this.timer = setTimeout(() =>{
                const result = []
                for (let i in this.cities){
                    this.cities[i].forEach((value)=>{
                        if(value.spell.indexOf(this.keyworld) > -1 ||value.name.indexOf(this.keyworld) > -1){
                           result.push(value) 
                        }
                    })
                }
                 this.list = result
            },100)
        }
    },
    mounted(){
          const options = {
            scrollY: true, 
            scrollX: false,
            mouseWheel: true,
            click: true,
            taps: true
        }
        this.scroll = new Bscroll(this.$refs.search,options)
        
    }
}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.search
    height .72rem
    padding 0 .1rem
    background $bgColor
    .search-input
        box-sizing border-box
        width 100%
        height .62rem
        padding 0 .1rem
        line-height .62rem
        padding-left 2.5rem
        border-radius .06rem
        color #666
.search-content
    z-index 1
    overflow hidden
    position absolute
    top 1.58rem
    left 0 
    right 0 
    bottom 0
    background #eee
    .search-item
        line-height .62rem
        padding-left .2rem
        background #fff

</style>
