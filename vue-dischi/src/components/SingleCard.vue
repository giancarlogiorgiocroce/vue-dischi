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
    color:rgb(128, 124, 121);
    width: calc(100% / 5 - 2vw);
    margin: 1vw;
    background-color: $secondary-color;
    padding: 1vw;
    transition-duration: 500ms;
    &:hover{
        cursor: pointer;
    }
    &:active{
        transform: scale(0.9);
    }
}
.image{
    width: 100%;
    img{
        width: 100%;
    }
}
.title{
    text-transform: uppercase;
    color:white;
    font-size: 14px;
    font-weight: 600;
    margin: 15px;
}
</style>