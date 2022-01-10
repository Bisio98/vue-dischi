<template>
    <div class="single_album" :class="hide" >
        <img :src="details.poster" alt="">
        <h2>{{ details.title.toUpperCase() }}</h2>
        <h3>{{ details.author }}</h3>
        <h4>{{ details.year }}</h4>
    </div>
</template>

<script>


export default {
    name: 'Album',
    props: {
        details: Object
    }
}
</script>

<style lang="scss" scoped>
    .single_album{
        text-align: center;
        background-color: #2E3A46;
        padding: 20px;
        margin: 15px 20px;
        width: calc(100% / 6);

        img{
            width: 95%;
        }

        h2{
            color: white;
        }

        h3,h4{
            color: #6B7A7D;
            margin-top: 10px;
        }
    }
</style>