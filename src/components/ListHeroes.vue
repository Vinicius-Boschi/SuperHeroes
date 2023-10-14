<template>
    <div class="list">
        <div class="list__content">
            <img class="list__img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3d/DC_Comics_logo.svg/2048px-DC_Comics_logo.svg.png" alt="logo dc">
            <p>Bem vindo ao mundo da DC Comics.</p>
            <h2>Escolha seu personagem</h2>
        </div>
        <ul>
            <li class="list__li" v-for="(heroe, index) in heroes" :key="index" @click="setHeroesUrl(heroe.url)">
                <img class="list__image" id="image" :src="heroe.images.sm" :alt="heroe.name" :data-id='heroe.id'>
                <h3 class="list__title">{{ heroe.name }}</h3>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'ListHeroes',
        props: [
            "apiUrl"
        ],
        data() {
            return {
                heroes: [],
                currentUrl: "",
                complementUrl: "all.json"
            }
        },
        methods: {
            fetchRequision() {
                let req = new Request(this.currentUrl + this.complementUrl)
                fetch(req)
                    .then((resp) => {
                        return resp.json()
                    }) 
                    .then((characters) => {
                        characters.forEach(heroe => {
                            this.heroes.push(heroe)
                        })
                    })
                    .catch((error) => {
                        console.log(error)
                    })
            },
            setHeroesUrl(url) {
                this.$emit("setHeroesUrl", url)
            }
        },
        created() {
            this.currentUrl = this.apiUrl
            this.fetchRequision()
        }
    }
</script>

<style lang="scss">
    @import "../assets/scss/variable.scss";
    @import "../assets/scss/styles/list.scss";
</style>