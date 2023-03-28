  


<script>
import axios from 'axios';

export default {
    data() {
        return {
            cards: [],
            archetypes: [],
            selectedArchetype: ''
        };
    },

    mounted() {
        this.fetchCards();
        this.fetchArchetypes();
        axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
            .then(response => {
                this.archetypes = response.data.data;
            })
    },

    watch: {
        selectedArchetype: function (newVal, oldVal) {
            this.$emit('archetype-selected', newVal);
        },
    },

    methods: {
        fetchCards() {
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
                .then((response) => {
                    this.cards = response.data.data;
                });
        },

        fetchArchetypes() {
            axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
                .then((response) => {
                    this.archetypes = response.data.data;
                });
        },

        onSelectArchetype() {
            this.$emit('filter-cards', this.selectedArchetype);
        }
    },

    computed: {
        filteredCards() {
            if (this.selectedArchetype) {
                return this.cards.filter(card => card.archetype === this.selectedArchetype);
            }
            return this.cards;

        }
    }
};
</script>

<!--<template>
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
                            <p>{{ card.type }}</p>-->
                            <!--<p>{{ card.desc }}</p>-->
                        <!--</div>
                    </div>
                </div>
            </div>
        </div>

    </main>
</template>-->

<template>
    <main>
        <div class="container-main">

            <div class="select-container">
                <select v-model="selectedArchetype" @change="onSelectArchetype">
                    <option value="">Tutti gli archetipi</option>
                    <option value="1">Alien</option>
                    <option v-for="archetype in archetypes" :key="archetype.name" :value="archetype.name">
                        {{ archetype.name }}
                    </option>
                </select>
            </div>


            <div class="container-cards">
                <div class="title-research flex">
                    <h4>Found {{ filteredCards.length }} cards</h4>
                </div>
                <div class="container-singles flex">
                    <div class="singles " v-for="card in filteredCards" :key="card.id">
                        <div class="single">
                            <h3>{{ card.name }}</h3>
                            <p>{{ card.type }}</p>
                            <p>{{ card.archetype }}</p>
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

