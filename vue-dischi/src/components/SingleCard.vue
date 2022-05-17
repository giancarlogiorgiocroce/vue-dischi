<template>
<div class="my-container text-center">
    <div class="image">
        <img :src="album.poster" :alt="album.title">
    </div>
    <div class="title">
        {{album.title}}
    </div>
    <div class="author">
        {{album.author}}
    </div>
    <div class="year">
        {{album.year}}
    </div>
</div>  
</template>

<script>
export default {
props:{
    album: Object,
}
}
</script>

<style scoped lang="scss">
@import '../assets/styles/vars';

.my-container{
    color:white;
    width: calc(100% / 5 - 2vw);
    margin: 1vw;
    background-color: $secondary-color;
    padding: 1vw;
}
.image{
    width: 100%;
    img{
        width: 100%;
    }
}
</style>