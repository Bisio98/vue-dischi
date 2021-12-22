<template>
    <header>
        <img src="https://loghi-famosi.com/wp-content/uploads/2020/09/Logo-della-Spotify.png" alt="Spotify logo">
    </header>
</template>

<script>
export default {
    name:'Header'
}
</script>

<style lang="scss" scoped>
    header{
        background-color: #2E3A46;
        height: 70px;
        display: flex;
        align-items: center;

        img{
            height: 50px;
            width: auto;
            
        }
    }
</style>