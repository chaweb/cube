<script>
export default {
    layout: 'cube',
    computed: {
        phone: function(){
            return this.$breakpoints.sSm
        },
        page2__cubes: function(){
            let baseUrl = `/cube/rendu/presentation/${this.phone ? "400_" : ''}`
            return [
                    {
                        id: "1",
                        title : "cube rouge",
                        color : "red",
                        namefile: `${baseUrl}red.png`,
                        price : "2€99"
                    },
                    {
                        id: "2",
                        title : "cube transparent",
                        color : "transparent",
                        namefile: `${baseUrl}transparent.png`,
                        price : "5€99"
                    },
                    {
                        id: "3",
                        title : "cube vert",
                        color : "green",
                        namefile: `${baseUrl}green.png`,
                        price : "2€99"
                    },
                    {
                        id: "4",
                        title : "cube bleu",
                        color : "blue",
                        namefile: `${baseUrl}blue.png`,
                        price : "2€49"
                    },
                ]
        },
    }
    
}
</script>

<template lang="pug">
include ../../node_modules/bemto.pug/bemto.pug
.content
    +b.page1
        +e.H1.title The Cube
            sup ®
            | !
        +e.UL.atouts
            li pratique pour être poser chez vous
            li sobre pour passer partout
            li ne se salit jamais, 
                i indégradable
                |  !!
    +b.page2
        +e.H2.title Des couleurs !
        +e.cards
            .card(v-for="item in page2__cubes" :key="item.id" :class="item.color")
                img.card__image(:src="item.namefile" width="30px" :alt="`un cube ${item.color} de toute beauté`")
                .card__content
                    .card__title {{item.title}}
                    .card__desc un cube de couleur {{item.color}} !
                    .card__price {{item.price}}
            
    +b.page3

    +b.page4
</template>

<style lang="sass">
p, a, div
    font-family: 'inter', sans-serif
    font-size: 1.5rem

@for $i from 1 through 6 
    h#{7 - $i} 
        font-size: $i * 1.4rem
        font-family: 'dosis', sans-serif
    @media screen and (max-width: 920px) 
        h#{7 - $i}
            font-size: $i * .6rem
            font-family: 'dosis', sans-serif
    
    
sub, sup
    font-size: 4rem


li
    list-style: none

.content
    @for $i from 1 through 4
        &>.page#{$i}
            height: 100vh
            scroll-snap-align: center
            display: flex
</style>


<style lang="sass" scoped>
.page1
    flex-direction: column
    background-image: linear-gradient(90deg, rgba(2,0,36,0) 46%, rgba(52,0,113,.15) 100%) 
    &__atouts
        padding-left: 10vh
        height: 100%
        display: flex
        flex-direction: column
        li
            margin: auto 0
            padding: 1rem 1rem
            width: 100%
            transition: .3s
            border: solid #fff 2px
            border-right: none
            border-top-left-radius: 5px
            border-bottom-left-radius: 5px
            cursor: help
            box-shadow: #000 0 0 0
            &:hover
                transition: .3s
                background: #fff
                color: #000
                transition: .3s
                box-shadow: #aaf3 0 12px 24px, #aaf3 0 -12px 24px, #fff2 0 0 24px
        @media screen and (max-width: 920px) 
            padding-left: 0
            li 
                background: #000000A0
                width: calc(100% - 1rem)

.page2
    flex-direction: column
    background-image: linear-gradient(90deg, rgba(2,0,36,0) 46%, rgba(52,0,113,.15) 100%) 
    &__cards
        max-height: min-content
        width: 100%
        display: flex
        flex-direction: row
        padding: 1rem
        @media screen and (max-height: 800px) 
            padding: 0
            overflow-y: auto
            @media (orientation: "portrait")
                flex-direction: column
        flex-wrap: nowrap
        position: relative

.card
    margin: 2px .5rem
    padding: 2rem
    width: 15%
    background-color: #FFFFFF50

    border-radius: 1rem
    display: flex
    flex-direction: column
    &__image
        width: 100%
    @media screen and (max-height: 800px) 
        @media (orientation: "portrait")
            flex-direction: row
            width: 100%
            padding: 0.5rem
            &__image
                margin: 0.5rem
                width: 100px
        
        @media (orientation: "landscape")
            padding: 0.5rem
            width: 25%
            &__content
                display: none
                background: #00000022
                z-index: 10
                transition: .53s background
                left: 0
                top: 0
            &:hover  &__content
                position: absolute
                display: block
                background: #123123

</style>
