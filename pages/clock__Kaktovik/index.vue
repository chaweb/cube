<script>
export default {
    data () {
        return {
            timestamp: [0,0,0],
            temp : 1,
            mounted: false,
            clockBalise : {}
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
                    
                    var botUni = timed % 5 //bar bottom of unit
                    var topUni = ((timed - botUni)/5) % 4//bar top of unit
                    var botDec = (((timed - botUni)/5)- topUni)/4 % 5 //bar bottom of dec
                    var topDec = (((((timed - botUni)/5)- topUni)/4)- botDec)/5 % 4 //bar top of dec

                    this.clockBalise[key].uni.forEach(elem => {
                        if(elem.classList.contains("un")){
                            if(topUni == 0 && botUni == 0){
                                elem.style.border = "black solid 6px"
                            }else{elem.style.border = "none"}
                        }

                        if(elem.classList.contains("de")){
                            if(botUni >= 1){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("tr")){
                            if(botUni >= 2){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("qu")){
                            if(botUni >= 3){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("ci")){
                            if(botUni >= 4){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("si")){
                            if(topUni >= 1){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("se")){
                            if(topUni >= 2){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("hu")){
                            if(topUni >= 3){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                    });

                    this.clockBalise[key].dec.forEach(elem => {
                        if(elem.classList.contains("un")){
                            if(topDec == 0 && botDec == 0){
                                elem.style.border = "black solid 6px"
                            }else{elem.style.border = "none"}
                        }

                        if(elem.classList.contains("de")){
                            if(botDec >= 1){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("tr")){
                            if(botDec >= 2){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("qu")){
                            if(botDec >= 3){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("ci")){
                            if(botDec >= 4){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("si")){
                            if(topDec >= 1){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("se")){
                            if(topDec >= 2){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                        
                        if(elem.classList.contains("hu")){
                            if(topDec >= 3){
                                elem.style.background = "black"
                            }else{elem.style.background = "none"}
                        }
                    });
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
        background-color: white
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