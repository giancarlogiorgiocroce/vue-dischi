<template>
  <main>
      <div class="container">
          <div class="row">
              <HeaderComp @newGenre="changeGenre" />
          </div>
          <div class="row">
              <SingleCard 
                v-for="(el, i) in filteredAlbumsByGenre"
                :key="i"
                :album="el"/>
          </div>
      </div>
  </main>
</template>

<script>
import SingleCard from './SingleCard.vue';
import axios from 'axios';
import HeaderComp from './HeaderComp.vue';

export default {
    components: { SingleCard, HeaderComp },
    data(){
        return{
            apiUrl: 'https://flynn.boolean.careers/exercises/api/array/music',
            apiArray: {},
            currentGenreValue: '',
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
            // console.log(this.currentGenreValue);
        }
    },
    computed:{
        filteredAlbumsByGenre(){
            let filteredArray = {};

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