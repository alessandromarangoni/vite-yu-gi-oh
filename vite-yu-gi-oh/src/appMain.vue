<script>
import { store } from './store/store';
import axios from 'axios';

export default {
    name: 'appMain',
    store: store,
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
        <div class="cards">
            <div>
                <img src="" alt="">
                <span>{{}}</span>
                <span>{{ }}</span>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.container {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}

.cards {
    height: 100px;
    width: 100px;
    background-color: aqua;
}
</style>
