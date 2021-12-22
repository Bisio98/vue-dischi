<template>
    <div class="background">
        <div class="container">
            <Album v-for="(album,index) in albumInfos" :key="index" :details="album" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import Album from './Album.vue'
export default {
  components: { Album },
    name: 'Body',
    data: function(){
        return{
            albumInfos: []
        }
    },
    created: function(){
        axios.get('https://flynn.boolean.careers/exercises/api/array/music')
        .then((response) => {
           this.albumInfos = response.data.response;
        })
    }
}
</script>

<style lang="scss" scoped>
    .background{
        background-color: #1E2D3B;
        height: calc(100vh - 70px);

        .container{
            width: 70%;
            margin: auto;
            padding: 50px 0;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
        }
    }
</style>