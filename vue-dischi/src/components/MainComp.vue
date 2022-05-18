<template>
    <main>
        <div class="container">
            <div class="row">
              <HeaderComp 
                :apiArray="this.apiArray"
                @newGenre="changeGenre" 
                @newAuthor="changeAuthor"/>
            </div>
            <div v-if="currentGenreValue != 0" class="row">
              <SingleCard 
                v-for="(el, i) in filteredAlbumsByGenre"
                :key="i"
                :album="el"/>
            </div>
            <div v-else-if="currentAuthorValue != 0" class="row">
              <SingleCard 
                v-for="(el, i) in filteredAlbumsByAuthor"
                :key="i"
                :album="el"/>
            </div>
            <div v-else class="row">
              <SingleCard 
                v-for="(el, i) in apiArray"
                :key="i"
                :album="el"/>
            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios';
import HeaderComp from './HeaderComp.vue';
import SingleCard from './SingleCard.vue';

export default {
    components: { SingleCard, HeaderComp },
    data(){
        return{
            apiUrl: 'https://flynn.boolean.careers/exercises/api/array/music',
            apiArray: [],
            currentGenreValue: '',
            currentAuthorValue: '',
        }
    },
    mounted(){
        this.callApi();
    },
    methods:{
        callApi(){
            axios.get(this.apiUrl)
            .then((res)=>{
                this.apiArray = res.data.response;
                // console.log(this.apiArray);
            })
            .catch((e)=>{
                return e;
            })
        },
        changeGenre(value){
            this.currentGenreValue = value;
            this.currentAuthorValue = 0;
            // console.log(this.currentGenreValue);
        },
        changeAuthor(value){
            this.currentAuthorValue = value;
            this.currentGenreValue = 0;
        }
    },
    computed:{
        filteredAlbumsByGenre(){
            let filteredArray = [];

            if(this.currentGenreValue == 0){
                filteredArray = this.apiArray;
            } else{
                filteredArray = this.apiArray.filter((el)=>{
                    // console.log(this.currentGenreValue);
                    return this.currentGenreValue == el.genre
                    // console.log(el.genre);
                })
            }

            // console.log('aray filtrato', filteredArray);
            return filteredArray;
        },
        filteredAlbumsByAuthor(){
            let filteredArray = [];

            if(this.currentAuthorValue == 0){
                filteredArray = this.apiArray;
            } else{
                filteredArray = this.apiArray.filter((el)=>{
                    return this.currentAuthorValue == el.author;
                })
            }

            return filteredArray;
        }
    }
}
</script>

<style scoped lang="scss">
@import '../assets/styles/vars';
main{
    background-color: $primary-color;
    min-height: calc(100vh);
    padding: 0 5vh 5vh 5vh;
}
</style>