<template>
    <div class="container" id="home">
        <List
            :imageUrl="imageUrl"
            :apiUrl="apiUrl"
            @setHeroesUrl="setHeroesUrl"
        />
        <Modal 
            v-if="showModal"
            :imageUrl="imageUrl"
            :heroesUrl="heroesUrl"
            @closeModal="closeModal"
        />
    </div>
</template>

<script>
    import List from './ListHeroes.vue'
    import Modal from './ModalHeroes.vue'   

    export default {
        name: 'Heroes',
        components: {
            List,
            Modal
        },
        data() {
            return {
                imageUrl: '',
                apiUrl: `https://gateway.marvel.com/v1/public/characters?ts=1667235187378&apikey=176701f1c86ddc91378ff7d420752043&hash=6bf268a166c762eed06299c83acea443`,
                heroesUrl: '',
                showModal: false
            }
        },
        methods: {
            setHeroesUrl(url) {
                this.heroesUrl = url
                this.showModal = true
            },
            closeModal() {
                this.heroesUrl = ''
                this.showModal = false
            }
        }
    }
</script>