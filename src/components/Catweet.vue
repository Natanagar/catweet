<template>

    <div class="user-profile_catweets-wrapper" >

        <div class="user-profile_catweet"  v-bind:key="index"  v-for="(catweet, index) in catweets" @click="favoriteCatweet(catweet.id)">
            <div class="user-profile_catweet_author">
                {{ catweet.author }}
            </div>
            {{ catweet.content }}
        </div>

    </div>

</template>

<script>

    export default {
        name: "Catweet",
        props: {
            catweets : Array,
            user : Object,
        },
        data(){
            console.log(this.props)
        },
        mounted() {
            console.log(this.props)
        },
        methods : {
            favoriteCatweet(id){
                this.$emit('favorite', id);
            }
        }
    }
</script>

<style scoped>
    .user-profile_catweets-wrapper{
        width: 440px;
        min-height: 100px;
        margin-left: 50px;
        margin-top: 50px;
        background-color: bisque;
        box-shadow: 10px 4px 21px 3px rgba(184,170,184,1);
        transition: background-color 1s linear;
    }
    .user-profile_catweets-wrapper:hover{
        background-color: #f0ffff;
    }
    .user-profile_catweet{
        margin:  50px;
        justify-content: flex-start;
        flex-direction: column;
        text-align: start;

    }
    .user-profile_catweet_author{
        padding : 3px;
        border-radius: 5px;
    }
    .user-profile_catweet_author:hover{
        animation: pulsing 2s infinite;
    }

    @keyframes pulsing {
        0% {
            -webkit-transform: scale(0.5, 0.5);
            transform: scale(0.5, 0.5)
        }
        50% {
            -webkit-transform: scale(1.0, 1.0);
            transform: scale(1.0, 1.0);
        }
        100% {
            -webkit-transform: scale(0.5, 0.5);
            transform: scale(0.5, 0.5);
        }
    }

</style>