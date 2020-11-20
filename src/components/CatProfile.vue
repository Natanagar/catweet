<template>
        <div class="user-profile" v-bind:style="styleObject">
            <div class="user-profile__user-panel">
                <h1 class="user-profile__username">@{{ user.userName }}  {{ fullName }}</h1>
                <div class="user-profile__admin_badge">{{ user.isAdmin ? 'admin' : 'user'}} </div>
                <div class="user-profile_follower-count">
                    <strong>Followers-cats: </strong> {{ followers }}
                </div>
            </div>
        </div>
        <div class="user-profile__catweets_wrapper">
            <div class="user-profile_catweet" v-bind:key="catweet.id"  v-for="catweet in user.catweets">
                {{ catweet.content }}
            </div>
        </div>
</template>

<script>
    export default {
        name: "CatProfile",
        data() {
            return ({
                followers: 0,
                user: {
                    id: 1,
                    userName: 'marsik-darsik',
                    firstName: "Margarita",
                    lastName: "Sergeeva",
                    email: "google@google.com",
                    isAdmin: true,
                    catweets: [
                        {id: 1, content: 'catweets is amazing'},
                        {id: 2, content: 'meow'},
                        {id: 3, content: 'Dont meow in my catweets'},
                        {id: 3, content: ' I/m hungry'}
                    ]
                },
                styleObject: {
                    margin: '50px 0 0 50px',
                    paddingLeft: '40px',
                    border: "1px solid darkgrey",
                    width: "300px",
                    height: "160px",
                    backgroundColor: 'light-grey',
                    fontSize: '13px',
                    boxShadow: '10px 10px 10px -9px rgba(0,0,0,0.75)',
                },
            })},
                watch: {
                followers(newFollowCount, oldFollowCount) {
                    console.log(newFollowCount, oldFollowCount)
                    if (oldFollowCount < newFollowCount) {
                        console.log(`${this.user.userName} has gained a follower!`)
                    }
                }
            },
            computed: {
                fullName() {
                    return `${this.user.firstName} ${this.user.lastName}`
                }
            },
            methods: {
                followsUser() {
                    this.followers++
                }
            },
            mounted() {
                this.followsUser()
            }
        }

</script>

<style scoped>
    .user-profile__admin_badge{
        width : 80px;
        text-align: center;
        background-color: aquamarine;
        font-size: 16px;
        border: 1px solid aqua;
        border-radius: 5px;
    }
    .user-profile__catweets_wrapper{
        display : flex;
        flex-direction: column;
        background-color: beige;
        justify-content: center;
        width : 350px;
        min-height: 500px;
        text-align: center;
        margin : 50px 0 0 50px;
        box-shadow: 10px 4px 21px 3px rgba(184,170,184,1);
    }
</style>