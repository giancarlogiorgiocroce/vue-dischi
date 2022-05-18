<template>
  <main>
      <div class="container">
          <div class="row">
              <HeaderComp :newGenre="currentGenre" />
          </div>
          <div class="row">
              <SingleCard 
                v-for="(el, i) in apiArray"
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
            currentGenre: '',
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
        newGenre(value){
            this.currentGenre = value;
            console.log(this.currentGenre);
        }
    },
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