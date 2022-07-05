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
</style>


<script>
export default {
    layout: 'cube',
}
</script>