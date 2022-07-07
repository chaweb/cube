<template lang="pug">
.page
    img(:src="`${baseURLrendu}${cubePos}.png`" alt="un cube qui tournne en fonction du scroll").cube

    nuxt.main


</template>

<style lang="sass" scoped>
.main
    overflow-x: hidden
    height: 100vh
    position: absolute
    scroll-snap-type: y mandatory
    top:0
    right: 0
    width: 50vw
    padding-left: 50vw
    z-index: 10
    @media (orientation: portrait) 
        width: calc(100vw - 4rem)
        paddin-left: 2rem

.cube
    position: fixed
    top: 0
    left: 0
    width: 100vw
    z-index: 0
    backdrop-filter: blur(6rem)

</style>

<script>
export default {
  watch: {
    baseURLrendu(){
        console.log(`url actuel : ${this.baseURLrendu}`)
        for(let i = 0; i<181; i+=2){
            this.imageObject[i] = new Image();
            let code = ('0'.repeat(4-('' + i).length) + ('' + i))
            this.imageObject[i].src = `${this.baseURLrendu}${code}.png`
        }
    }
  },
    head: {
        title: "the cube",
        link: [
            { rel: 'icon', type: 'image/x-icon', href: '/cube/favicon.ico' }
        ]
    },
    computed: {
        orientation: function () {
            return this.$breakpoints.orientation
        },
        phone: function(){
            return this.$breakpoints.sSm
        },
        tablet: function(){
            return this.$breakpoints.sMd && this.$breakpoints.lSm
        },
        baseURLrendu: function(){
            return  `/cube/rendu/${this.orientation == "portrait"? "portrait_" : ''}${this.phone ? "480_" : (this.tablet ? "960_" : '')}`
        },
    },
    methods: {
        updateScroll(){
            let scroll = this.main.scrollTop 
            let MaxScroll = this.main.scrollHeight - this.main.clientHeight

            let t = ((scroll)*this.nbTour/MaxScroll)*this.nbimg + this.nbimg/2

            let img = Math.round(t - this.nbimg*(Math.round(t/this.nbimg)) + this.nbimg/2)
            
            let cubePos = '' + (img == 0 ? 1 : img)
            cubePos = '0'.repeat(4-cubePos.length) + cubePos
            this.cubePos = cubePos

        }
    },
    data () {
        return {
            cubePos: '0001',
            main: '',
            nbimg: 179,
            nbTour : 0.249*4,
            imageObject: []
        }
    },
    mounted(){
        for(let i = 0; i<181; i+=2){
            this.imageObject[i] = new Image();
            let code = ('0'.repeat(4-('' + i).length) + ('' + i))
            this.imageObject[i].src = `${this.baseURLrendu}${code}.png`
        }
        this.main = document.querySelector('.main')
        this.main.addEventListener('scroll', this.updateScroll)
    }
    
}
</script>