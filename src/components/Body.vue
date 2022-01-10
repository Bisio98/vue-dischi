<template>
    <div class="background">
        <div class="search">
            <select v-model="activeGenre" name="Genere" id="">
                <option v-for="(genre,index) in allGenres" :key="index"> {{ genre }} </option>
                
            </select>
            <button v-on:click="reset">RESET</button>
            <select v-model="activeAuthor" name="Author" id="">
                <option v-for="(author,index) in allAuthors" :key="index"> {{ author }}</option>
                
            </select>
        </div>
        <div v-if="albumInfos.length > 0" class="container">
            <Album :class="{ hide: ((!albumInfos[index].genre.includes(activeGenre)) || (!albumInfos[index].author.includes(activeAuthor))) }" v-for="(album,index) in albumInfos" :key="index" :details="album" />
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
            albumInfos: [],
            allGenres: [],
            allAuthors: [],
            activeGenre: '',
            activeAuthor: ''
        }
    },
    methods: {
        reset: function(){
            this.activeAuthor = '';
            this.activeGenre = '';
            
        }
    },
    created: function(){
        axios.get('https://flynn.boolean.careers/exercises/api/array/music')
        .then((response) => {
           this.albumInfos = response.data.response;
           for(let i = 0; i < this.albumInfos.length; i++){
                if(!(this.allGenres.includes(this.albumInfos[i].genre)))
                    this.allGenres.push(this.albumInfos[i].genre);
                if(!(this.allAuthors.includes(this.albumInfos[i].author)))
                    this.allAuthors.push(this.albumInfos[i].author);
            }
        })
    }
}
</script>

<style lang="scss" scoped>
    .background{
        background-color: #1E2D3B;
        min-height: calc(100vh - 70px);

        .search{
            width: 60%;
            margin: auto;
            display: flex;
            justify-content: space-evenly;
            padding: 20px 0;

            button{
                padding: 5px 10px;
                background-color: #2E3A46;
                border-radius: 10px;
                border: 1px solid white;
                color: white;
                cursor: pointer;
            }

            select{
                padding: 5px 10px;
                border: 1px solid white;
                border-radius: 10px;
                background-color: #2E3A46;
                color: white;
                min-width: 100px;
            }
        }

        .container{
            width: 70%;
            margin: auto;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;

            .hide{
                display: none;
            }

            .show{
                display: inline-block;
            }
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