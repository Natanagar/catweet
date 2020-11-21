<template>
    <div class="user-profile_wrapper_post">
        <div class="user-profile" v-bind:style="styleObject">
            <div class="user-profile__user-panel">
                <h1 class="user-profile__username">@{{ user.userName }}  {{ fullName }}</h1>
                <div class="user-profile__admin_badge">{{ user.isAdmin ? 'admin' : 'user'}} </div>
                <div class="user-profile_follower-count">
                    <strong>Followers-cats: </strong> {{ followers }}
                </div>
            </div>
        </div>
    <Catweet :catweets="this.catweets" @favorite="toogleFavorite"/>

    </div>
    <form class="user-profile__create_catweet" @submit.prevent="createNewCatweet">
        <label for="newCatweet">
            <strong> Say yours meow</strong>
        </label>
            <textarea id="newCatweet" rows="4" v-model.trim="newCatweetContent" name="newCatweet"/>
        <div class="user-profile__create_catweet_type">
            <label for="newCatweetType">
                <strong>Type: </strong>
            </label>
            <select id="newCatweetType" v-model="selectedCatweetType" name="selectedCatweetType">
                <option :value="option.value" :key="index" v-for="(option, index) in catweetTypes">
                    {{ option.value }}
                </option>
            </select>
            <label for="catweetAuthor">
                <strong> Stay in touch </strong>
            </label>
            <input id="catweetAuthor" name="catweetAuthor" v-model="catweetAuthor"/>

        </div>
        <div class="user-profile__catweets_wrapper_submit">
            <input type="submit" value="meow"/>
        </div>

    </form>
</template>

<script>
    import Catweet from "./Catweet";

    Catweet
    export default {
        name: "CatProfile",
        components : {
            Catweet,
        },
        data() {
            return ({
                followers: 0,
                newCatweetContent : '',
                selectedCatweetType : 'instant',
                catweetAuthor : '@white-cat',
                catweetTypes : [
                    { value : 'draft', name : 'draft'},
                    { value : 'instant', name : 'instant' }
                ],
                user: {
                    id: 1,
                    userName: 'marsik-darsik',
                    firstName: "Margarita",
                    lastName: "Sergeeva",
                    email: "google@google.com",
                    isAdmin: true,

                },
                catweets: [
                    {id: 1, content: 'catweets is amazing', author : "@alice_homepussycat"},
                    {id: 2, content: 'meow', author : '@bubble_whichsaysmeow'},
                    {id: 3, content: 'Dont meow in my catweets', author : '@blinded_tom'},
                    {id: 3, content: ' I/m hungry', author : '@stray'},
                ],
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
                followsUser (){
                    this.followers++
                },
                toogleFavorite(id){
                    console.log(`Favorite catweets ${id}`)
                },
                createNewCatweet (e){
                    e.preventDefault();
                    console.log(this.newCatweetContent, this.selectedCatweetType, this.catweetAuthor)
                    if(this.newCatweetContent && this.selectedCatweetType !== 'draft'){
                        this.catweets.unshift({
                            id : this.catweets.length + 1,
                            content : this.newCatweetContent,
                            author : this.catweetAuthor,
                        })
                    }

                },

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

        min-height: 500px;
        text-align: center;
        margin : 50px 0 0 50px;
        box-shadow: 10px 4px 21px 3px rgba(184,170,184,1);
    }
    .user-profile_wrapper_post{
        display: inline-flex;
    }
    .user-profile__create_catweet{
        flex-direction: column;
        background-color: antiquewhite;
        height : max-content;
        margin-left: 440px;
        margin-top: 20px;
        width : 400px;
        padding : 20px;
    }
    .user-profile__create_catweet label{
        display: block;
    }
    .user-profile__create_catweet textarea{
       margin: 10px auto 10px 10px;
        width : 360px;
    }
    #newCatweetType{
        width : 100px;
        height: 30px;
        font-size: 16px;
        margin-left: 10px;
        margin-bottom: 50px;
    }
    .user-profile__catweets_wrapper_submit button{
        margin : 20px auto 20px auto;
        padding : 5px;
        width : 100px;
        background-color: khaki;
        border-radius: 5px;
    }
</style>