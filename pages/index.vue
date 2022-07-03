<template lang="pug">
.content
    .page1
        h1.page1__title The Cube
            sup ®
            | !
        ul.page1__atouts
            li pratique pour être poser chez vous
            li sobre pour passer partout
            li ne se salit jamais, 
                i indégradable
                |  !!
    .page2

    .page3

    .page4
</template>

<style lang="sass">
p, a, div
    font-family: 'inter', sans-serif
    font-size: 1.5rem

@for $i from 1 through 6 
    h#{7 - $i} 
        font-size: $i * 1.4rem
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
        li
            padding: 1rem 1rem
            margin: 4rem 0
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
</style>