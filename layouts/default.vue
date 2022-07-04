<template lang="pug">
.page
    img(:src="`/cube/cube/${cubePos}.png`" :srcset="`/cube/cube/480_${cubePos}.png 480w, /cube/cube/${cubePos}.png 1920w`" alt="un cube qui tournne en fonction du scroll").cube

    nuxt.main


</template>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Courier+Prime:ital,wght@0,400;0,700;1,400;1,700&family=Dosis:wght@200;300;400;500;600;700;800&family=Inter:wght@200;300;400;500;600;700;800;900&display=swap')
html
    user-select: none
    color: #FFF
    font-family: 'Dosis', sans-serif
    background: #181A1B
    background-repeat: no-repeat
    background-size: cover
    &, body
        overflow: hidden
        marging: 0
        padding: 0

</style>

<style lang="sass" scoped>
.main
    overflow-x: auto
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
    data () {
        return {
            cubePos: '0001'
        }
    },
    mounted(){
        var imageObject = []
        for(let i = 0; i<181; i+=2){
            imageObject[i] = new Image();
            imageObject[i+1] = new Image();
            let code = ('0'.repeat(4-('' + i).length) + ('' + i))
            imageObject[i].src = `/cube/cube/${code}.png`
            imageObject[i+1].src = `/cube/cube/480_${code}.png`
        }
        const main = document.querySelector('.main')
        const nbimg = 179
        const nbTour = 1.3*4
        main.onscroll = function(e){
            let scroll = main.scrollTop == 0 ? 1 : main.scrollTop
            let MaxScroll = main.scrollHeight - main.clientHeight

            let t = ((scroll)*nbTour/MaxScroll)*nbimg + nbimg/2

            let img = Math.round(t - nbimg*(Math.round(t/nbimg)) + nbimg/2)+ 1
            
            console.log(img)
            let cubePos = '' + img
            cubePos = '0'.repeat(4-cubePos.length) + cubePos
            window.$nuxt.$children[2].cubePos = cubePos
        }
    }
    
}
</script>