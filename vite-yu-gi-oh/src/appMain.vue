<script>
import { vShow } from 'vue';
import { store } from './store/store';
import axios from 'axios';

export default {
    name: 'appMain',
    data() {
        return {
            store,
            tipoScelto: ''
        }
    },
    methods: {
        getCardImageUrl() {
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
                .then(r => {
                    store.carte.push(r.data.data)
                    this.getCardImageArchetipo()
                })
                .catch(e => console.log(e))
        },
        getCardImageArchetipo() {
            for (let i = 0; i < store.carte[0].length; i++) {
                const archetipo = store.carte[0][i].archetype;
                if (archetipo !== undefined && (!store.archetipi.includes(archetipo))) {
                    this.store.archetipi.push(archetipo)
                }
            }
            console.log(store.archetipi)
        },
        changeSelect(valore) {
            this.tipoScelto = valore
            console.log(this.tipoScelto)
        }
    },
    mounted() {
        this.getCardImageUrl()
    },
}
</script>

<template>
    <div class="container">
        <div>
            <select name="archetype" v-model="this.tipoScelto" id="">
                <option v-for="archetipo in store.archetipi" @change="changeSelect(archetipo)" :value="archetipo" selected>
                    {{ archetipo }}
                </option>
            </select>
        </div>
        <div class="cards_container">
            <div class="" v-for="(carta, i) in store.carte[0]" v-show="carta.archetype == this.tipoScelto">
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
