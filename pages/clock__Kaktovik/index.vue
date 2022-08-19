<script>
export default {
    data () {
        return {
            timestamp: [0,0,0],
            temp : 1,
            mounted: false,
            clockBalise : {},
            tim : {
                    uni : {
                        bot: 0,
                        top: 0
                    }, 
                    dec : {
                        bot: 0,
                        top: 0
                    }
                }
        }
    },
    mounted(){
        this.mounted = true
        this.clockBalise = {
                    hours: {
                        dec: document.querySelectorAll("div.hours div.dec div.numero"),
                        uni: document.querySelectorAll("div.hours div.uni div.numero")
                    },
                    minutes: {
                        dec: document.querySelectorAll("div.minutes div.dec div.numero"),
                        uni: document.querySelectorAll("div.minutes div.uni div.numero")
                    },
                    secondes: {
                        dec: document.querySelectorAll("div.secondes div.dec div.numero"),
                        uni: document.querySelectorAll("div.secondes div.uni div.numero")
                    },
                }
    },
    layout: "none",
    created() {
        setInterval(this.getNow, 1000);
    },
    methods: {
        getNow: function() {
            const today = new Date();
            const time = [today.getHours(), today.getMinutes(), today.getSeconds()];
            this.timestamp = time;

            if(this.mounted){
                const sec = time[2]
                const min = time[1]
                const hou = time[0]
                
                for(var key in this.clockBalise){
                    if (key == "secondes") var timed = sec
                    if (key == "minutes") var timed = min
                    if (key == "hours") var timed = hou

                    this.tim.uni.bot = timed % 5
                    this.tim.uni.top = (timed - this.tim.uni.bot) / 5 % 4
                    this.tim.dec.bot = (((timed - this.tim.uni.bot) / 5) - this.tim.uni.top)/4 %5,
                    this.tim.dec.top = (((((timed - this.tim.uni.bot) / 5) - this.tim.dec.bot)/4)-  this.tim.dec.bot)/5 % 4
                    for(var num in this.clockBalise[key]){
                        this.clockBalise[key][num].forEach(elem => {
                            if(elem.classList.contains("un")){
                                if(this.tim[num].bot == 0 && this.tim[num].top == 0){
                                    elem.style.border = "black solid 6px"
                                }else{elem.style.border = "none"}
                            }

                            if(elem.classList.contains("de")){
                                if(this.tim[num].bot >= 1){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                            
                            if(elem.classList.contains("tr")){
                                if(this.tim[num].bot >= 2){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                            
                            if(elem.classList.contains("qu")){
                                if(this.tim[num].bot >= 3){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                            
                            if(elem.classList.contains("ci")){
                                if(this.tim[num].bot >= 4){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                            
                            if(elem.classList.contains("si")){
                                if(this.tim[num].top >= 1){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                            
                            if(elem.classList.contains("se")){
                                if(this.tim[num].top >= 2){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                            
                            if(elem.classList.contains("hu")){
                                if(this.tim[num].top >= 3){
                                    elem.style.background = "black"
                                }else{elem.style.background = "none"}
                            }
                        });
                    }
                }
            }
        }
    }
}
</script>

<template lang="pug">
- var type = ["hours", "minutes", "secondes"]
.page
    .title Horloge avec les nombres Kaktovik 
    .clock
        each val in type
            - var n = ["un", "de", "tr", "qu", "ci", "si", "se", "hu"];
            .type(class=val)
                .dec
                    each num in n
                        .numero(class=num)
                .uni
                    each num in n
                        .numero(class=num)
                .point :
    .trueClock {{timestamp[0]}} : {{timestamp[1]}} : {{timestamp[2]}}

</template>

<style lang="sass" scoped>
.page
    width: 100vw
    height: 100vh
    display: flex
    justify-content: center
    align-items: center
    flex-direction: column
    position: relative
    .title
        position: absolute
        top : 10rem
        font-size: 5rem
        font-family: inter

    .trueClock
        position: absolute
        bottom: 10rem
        font-size: 2.5rem

    .clock
        color: black
        background-color: #ddd 
        width: 60vw
        max-width: 100em
        display: flex
        justify-content: center
        align-items: center
        flex-direction: row
        flex-wrap: wrap
        height: 15em
        border-radius: 1em
        .type
            display: flex
            justify-content: flex-end
            align-items: center
            width: 25%
            height: 45%
            .dec, .uni
                width: 50%
                position: relative
            .point
                font-size: 6rem
            &.secondes .point
                display: none

            .numero
                position: absolute
                left: 50%
                width: 10px
                height: 60px
                border-radius: 100rem
                background-color: black
                transition: none
                &.un
                    width: 30px
                    height: 30px
                    transform: translateX(-40%)
                    border: black 6px solid
                    background: none
                &.de
                    transform: translateX(-21px) rotate(-15deg) 
                &.tr
                    transform: translateX(-7px) rotate(15deg) 
                &.qu
                    transform: translateX(7px) rotate(-15deg) 
                &.ci
                    transform: translateX(21px) rotate(15deg) 
                &.si
                    transform: translateY(-30px) rotate(-12deg) rotate(90deg)
                &.se
                    transform: translateY(-42px) rotate(12deg) rotate(90deg)
                &.hu
                    transform: translateY(-54px) rotate(-12deg) rotate(90deg)
                


                



</style>