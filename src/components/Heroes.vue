<template>
    <div class="container" id="home">
        <Search 
            :apiUrl="apiUrl"
            @setHeroesUrl="setHeroesUrl"
        />
        <List
            :apiUrl="apiUrl"
            @setHeroesUrl="setHeroesUrl"
        />
        <Modal 
            v-if="showModal" 
            :apiUrl="apiUrl"
            @closeModal="closeModal"
        />
    </div>
</template>

<script>
    import Search from './Search.vue'
    import List from './ListHeroes.vue'
    import Modal from './ModalHeroes.vue'   

    export default {
        name: 'Heroes',
        components: {
            Search,
            List,
            Modal
        },
        data() {
            return {
                apiUrl: 'https://cdn.jsdelivr.net/gh/akabab/superhero-api@0.3.0/api/',
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