<script>
export default {
    data () {
        return {
            audio(){return new Audio('/choice/music.mp3') }
        }
    },
    layout: "none",
    mounted (){
        this.audio = new Audio('/choice/music.mp3')
        this.audio.volume = 0.05
        console.log(this.audio)
        this.audio.play()
        this.audio.addEventListener('ended', function() {
            this.currentTime = 0;
            this.play();
        }, false);
    }
}
</script>

<template lang="pug">
.page
    input(type="range" min="0" max="1" step=".01" v-model="audio.volume")
    .content
        .eye.L
        .eye.R
        .heart.L
            .left
            .right
        .heart.R
            .left
            .right
</template>

<style lang="sass">
body
  background: #123
  display: flex
  align-items: center
  justify-content: center
  width: 100vw
  height: 100vh
  input
    position: absolute
    top: 5%
  
.content
    width: 200px
    height: 300px
    display: flex
    align-items: center
    justify-content: space-around
    position: relative
    .eye
        filter: blur(.45px)
        position: relative
        width: 25px
        height: 25px
        display: flex
        flex-direction: column 
            
        &.L
            animation: eyesL 9s infinite linear
            --rotate: 90deg 
        &.R
            animation: eyesR 9s infinite linear
            --rotate: -90deg 
        
        &::before
            content: ''
            position: relative
            display : inline-block
            height : 0
            width : 0
            border-right : 12px solid transparent
            border-bottom : 13px solid #fff
            border-left : 13px solid transparent
            animation: eyesbottom 9s infinite linear
        
        &::after
            content: ''
            display : inline-block
            height : 0
            width : 0
            border-right : 13px solid transparent
            border-top : 50px solid #fff
            border-left : 12px solid transparent
            animation: eyestop 9s infinite linear

    .heart
        position: absolute
        width: 20px
        height: 20px
        display: flex
        flex-direction: column 
        $color: #e33
        &.L
            left: 25px
        &.R
            right: 25px
        .left
            position: relative
            --translate: -10
            animation: hearth 9s infinite linear
            &::after
                position: absolute
                content: ''
                bottom: -25px
                display : inline-block
                border-top : 10px solid transparent
                border-right : 10px solid $color
                border-bottom : 10px solid transparent
            &::before
                position: absolute
                content: ''
                bottom: -15px
                left: -5px
                width: 15px
                height: 20px
                background-color: $color
                border-radius: 50% 50% 0 50%
        .right
            position: relative
            --translate: 10
            animation: hearth 9s infinite linear
            &::before
                position: absolute
                content: ''
                bottom: -25px
                left: 10px
                display : inline-block
                border-top : 10px solid transparent
                border-left : 10px solid $color
                border-bottom : 10px solid transparent
            &::after
                position: absolute
                content: ''
                bottom: -15px
                right: -5px
                width: 15px
                height: 20px
                background-color: $color
                border-radius: 50% 50% 50% 0

@keyframes hearth
    0% //start
        transform: scale(0)

    18% //love
        transform: scaleX(0)
    20.5%
        transform: scaleX(.9)
    22%
        transform: scaleX(0)

    

    29% //heart control
        transform: scaleX(0)
    32.5%
        transform: scale(1.2) translateX(calc(var(--translate) * .5px)) 
    34%
        transform: rotate(calc(var(--translate) * 2deg)) scale(1.2) translateX(calc(var(--translate) * 1px)) 
    35%
        transform: scaleX(0)

    64.5% //love
        transform: scaleX(0)
    65%
        transform: scaleX(.9)
    66%
        transform: scaleX(0)

    
    
    75.5% //heart control
        transform: scaleX(0)
    77%
        transform: scale(1.2) translateX(calc(var(--translate) * .5px)) 
    78.5%
        transform: rotate(calc(var(--translate) * 2deg)) scale(1.2) translateX(calc(var(--translate) * 1px)) 
    79.5%
        transform: scaleX(0)

    100% //end
        transform: scaleX(0)

$border : "top", "bottom" 

@each $type in $border
    @keyframes eyes#{$type}
        0% //start
            border-#{$type}-color: #fff


        24% //brain
            border-#{$type}-color: #fff
        25.5% 
            border-#{$type}-color: #6E2020
        27%
            border-#{$type}-color: #fff
        
        38% //Caffeinate 
            border-#{$type}-color: #fff
        39.5%
            border-#{$type}-color: #4a3
        40%
            border-#{$type}-color: #fff


        53% //Melatonin        
            border-#{$type}-color: #fff
        58%
            
            border-#{$type}-color: #132
        60%
            
            border-#{$type}-color: #fff            

        86.5% //Caffeinate !
            
            border-#{$type}-color: #fff
        87%
            
            border-#{$type}-color: #4a3
        87.5%
            
            border-#{$type}-color: #fff
            
        100%//end
            border-#{$type}-color: #fff


// yeux droit
@keyframes eyesR
    0% //start
        transform: rotate(var(--rotate)) scaleX(0)

    19% //love
        transform: rotate(var(--rotate)) scaleX(0)
    20%
        transform: rotate(var(--rotate)) scaleX(1)

    
    22.5% //brain
        transform: rotate(var(--rotate)) scaleX(1)

    29.5% //heart control
        transform: rotate(var(--rotate)) scaleX(1)
    30%
        transform: rotate(var(--rotate)) scale(1.2) 
    30.5%
        transform: rotate(var(--rotate)) scaleX(1)

    39% //Caffeinate !
        transform: rotate(var(--rotate)) scaleX(1)
    39.5%
        transform: rotate(var(--rotate)) scaleX(1) rotate(-360deg)
    40%
        transform: rotate(var(--rotate)) scaleX(1)

    53% //Melatonin
        transform: rotate(var(--rotate)) scaleX(1)
    58%
        transform: rotate(calc(var(--rotate) /1.5))  scaleX(.3) 
    60%
        transform: rotate(var(--rotate)) scaleX(1)


    65%  //love
        transform: rotate(var(--rotate)) scaleX(1)

    

    75.5% //heart control
        transform: rotate(var(--rotate)) scaleX(1)
    76%
        transform: rotate(var(--rotate)) scale(1.2) 
    76.5%
        transform: rotate(var(--rotate)) scaleX(1)

        

    86.5% //Caffeinate !
        transform: rotate(var(--rotate)) scaleX(1)
    87%
        transform: rotate(var(--rotate)) scaleX(1) rotate(360deg)
    87.5%
        transform: rotate(var(--rotate)) scaleX(1)

    93.5% //You get me going
        transform: rotate(var(--rotate)) scaleX(1)
    95%
        transform: rotate(var(--rotate)) scaleX(0)
    96%
        transform: rotate(var(--rotate)) scaleX(1)

    99%
        transform: rotate(var(--rotate)) scaleX(1)
    100% //end
        transform: rotate(var(--rotate)) scaleX(0)



// yeux gauche
@keyframes eyesL
    0% //start
        transform: rotate(var(--rotate)) scaleX(0)

    19% //love
        transform: rotate(var(--rotate)) scaleX(0)
    20%
        transform: rotate(var(--rotate)) scaleX(1)

    
    22.5% //brain
        transform: rotate(var(--rotate)) scaleX(1)

    29.5% //heart control
        transform: rotate(var(--rotate)) scaleX(1)
    30%
        transform: rotate(var(--rotate)) scale(1.2) 
    30.5%
        transform: rotate(var(--rotate)) scaleX(1)

    39% //Caffeinate !
        transform: rotate(var(--rotate)) scaleX(1)
    39.5%
        transform: rotate(var(--rotate)) scaleX(1) rotate(360deg)
    40%
        transform: rotate(var(--rotate)) scaleX(1)

    53% //Melatonin
        transform: rotate(var(--rotate)) scaleX(1)
    58%
        transform: rotate(calc(var(--rotate) /1.5)) scaleX(.3) 
    60%
        transform: rotate(var(--rotate)) scaleX(1)


    65%  //love
        transform: rotate(var(--rotate)) scaleX(1)

    

    75.5% //heart control
        transform: rotate(var(--rotate)) scaleX(1)
    76%
        transform: rotate(var(--rotate)) scale(1.2) 
    76.5%
        transform: rotate(var(--rotate)) scaleX(1)

        

    86.5% //Caffeinate !
        transform: rotate(var(--rotate)) scaleX(1)
    87%
        transform: rotate(var(--rotate)) scaleX(1) rotate(360deg)
    87.5%
        transform: rotate(var(--rotate)) scaleX(1)

    99%
        transform: rotate(var(--rotate)) scaleX(1)
    100% //end
        transform: rotate(var(--rotate)) scaleX(0)



</style>