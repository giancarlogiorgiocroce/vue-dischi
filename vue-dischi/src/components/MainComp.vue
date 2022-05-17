<template>
  <main>
      <div class="container">
          <div class="row debug">
              <SingleCard 
                v-for="(el, i) in apiArray"
                :key="i"/>
          </div>
      </div>
  </main>
</template>

<script>
import SingleCard from './SingleCard.vue';
import axios from 'axios';

export default {
    components: { SingleCard },
    data(){
        return{
            apiUrl: 'https://flynn.boolean.careers/exercises/api/array/music',
            apiArray: {},
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
                console.log(this.apiArray);
                // console.log(res.data.response);
            })
            .catch((e)=>{
                return e;
            })
        }
    },
}
</script>

<style scoped lang="scss">
@import '../assets/styles/vars';
main{
    background-color: $primary-color;
    min-height: calc(100vh - 75px);
    padding: 5vh;

}
</style>