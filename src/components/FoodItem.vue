<template>
    <div>
        <h2 v-bind:style="[favoriteFood ? { color: 'rgb(200 30 90)' } : { color: 'rgb(0 0 0)' }]">{{ foodName }}</h2>
        <p>{{ desc }}</p>
        <p id="red" v-on:click="countClick">Click me! {{ clicks }} times</p>
        <button id="btnStyle" v-on:click="toggleFavorite">Favorite</button>
    </div>
</template>
<script>
export default {
    props: [
        'foodName', 'desc', 'isFavorite',
    ],
    data() {
        return {
            favoriteFood: this.isFavorite,
            clicks: 0
        }
    },

    methods: {
        countClick() {
            this.clicks++;
        },
        toggleFavorite() {
            this.favoriteFood = !this.favoriteFood
            console.log(this.favoriteFood)
        }
    }
}
</script>

<style scoped>
div {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 2px grey;
    border-radius: 8px;
    background-color: rgb(230, 238, 212);
    padding: 10px;
    margin: 15px;
    cursor: pointer;
    box-shadow: 0 5px 10px rgb(118, 116, 116);
}
#red {
    color: red;
    font-weight: bold;
}
#btnStyle {
    padding: 10px;
    background-color: rgb(20, 67, 21);
    color: bisque;
    font-weight: bold;
       border-radius: 5px;
    border: none;
}
</style>