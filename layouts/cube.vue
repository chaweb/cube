<template lang="pug">
.page
    img(:src="`/cube/${cubePos}.png`" :srcset="`/cube/480_${cubePos}.png 480w, /cube/${cubePos}.png 1920w`" alt="un cube qui tournne en fonction du scroll").cube

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
    @media screen and (max-width: 920px) 
        width: calc(100vw - 4rem)
        paddin-left: 2rem

.cube
    position: fixed
    top: 0
    left: -25%
    width: 100vw
    z-index: 0
    backdrop-filter: blur(6rem)
    @media screen and (max-width: 920px) 
        width: auto
        height: 100vh
        object-fit: cover
        left: -25%
        padding-left: 1rem

</style>

<script>
export default {
    methods: {
        updateScroll(){
            let scroll = this.main.scrollTop == 0 ? 1 : this.main.scrollTop
            let MaxScroll = this.main.scrollHeight - this.main.clientHeight

            let t = ((scroll)*this.nbTour/MaxScroll)*this.nbimg + this.nbimg/2

            let img = Math.round(t - this.nbimg*(Math.round(t/this.nbimg)) + this.nbimg/2)+ 1
            
            console.log(img)
            let cubePos = '' + img
            cubePos = '0'.repeat(4-cubePos.length) + cubePos
            this.cubePos = cubePos

        }
    },
    data () {
        return {
            cubePos: '0001',
            main: '',
            nbimg: 179,
            nbTour : 1.3*4
        }
    },
    mounted(){
        console.log("hi !")
        var imageObject = []
        for(let i = 0; i<181; i+=2){
            imageObject[i] = new Image();
            imageObject[i+1] = new Image();
            let code = ('0'.repeat(4-('' + i).length) + ('' + i))
            imageObject[i].src = `/cube/${code}.png`
            imageObject[i+1].src = `/cube/480_${code}.png`
        }
        this.main = document.querySelector('.main')
        this.main.addEventListener('scroll', this.updateScroll)
    }
    
}
</script>