  
<script>
import axios from 'axios';

export default {
    data() {
        return {
            cards: [],
        };
    },

    mounted() {
        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
            .then((response) => {
                this.cards = response.data.data;
            })
    },
};
</script>

<template>
    <main>
        <div class="container-main">
            <div class="select-container">
                <select name="">
                    <option value="0">Alien</option>
                    <option value="0">Alien</option>
                    <option value="0">Alien</option>
                </select>
            </div>
            <div class="container-cards">
                <div class="title-research flex">
                    <h4>Found 39 cards</h4>
                </div>
                <div class="container-singles flex">
                    <div class="singles " v-for="card in cards" :key="card.id">
                        <div class="single">
                            <h3>{{ card.name }}</h3>
                            <p>{{ card.type }}</p>
                            <!--<p>{{ card.desc }}</p>-->
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </main>
</template>
  

<style lang="scss" scoped>
@import "../assets/main.scss";
</style>
