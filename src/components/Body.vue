<template>
    <div class="background">
        <div v-if="albumInfos.length > 0" class="container">
            <Album v-for="(album,index) in albumInfos" :key="index" :details="album" />
        </div>
        <div class="loading" v-else>
            <i class="fas fa-circle-notch"></i>
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
        min-height: calc(100vh - 70px);

        .container{
            width: 70%;
            margin: auto;
            padding: 50px 0;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
        }

        .loading{
            display: flex;
            align-items: center;
            justify-content: center;
            color: #00D856;
            font-size: 200px;
            position: relative;
            top: 300px;
            animation: rotate 2s linear infinite;
        }


        @keyframes rotate {
            to{
                transform: rotate(360deg);
            }
        }
    }
</style>