<script>
import { store } from './store/store';
import axios from 'axios';

export default {
    name: 'appMain',
    data() {
        return {
            store,
        }
    },
    methods: {
        getCardImageUrl() {
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
                .then(r => { store.carte.push(r.data.data) })
                .catch(e => console.log(e))

        }
    },
    beforeMount() {
        this.getCardImageUrl()
    },
    mounted() {
        console.log(store)
    }
}
</script>

<template>
    <div class="container">
        <div class="cards_container">
            <div class="" v-for="(carta, i) in store.carte[0]">
                <img :src="carta.card_images[0].image_url" alt="">
                <h4>{{ carta.name }}</h4>
                <p>{{ carta.archetype }}</p>
                <span></span>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.container {
    background-color: rgba(255, 255, 255, 0.505);
    padding: 2rem;
    max-width: 1000px;
    margin: 0 auto;
    margin-top: 3rem;
    border-radius: 30px;
}

.cards_container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    text-align: center;

    div {
        width: calc(100% / 5);

        h4 {
            color: white;
            padding: 1rem;
        }

        p {
            color: rgb(0, 0, 0);
        }
    }

    img {
        padding-top: 1rem;
        width: 150px;
    }
}
</style>
