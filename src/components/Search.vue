<template>
    <form @submit.prevent="setHeroesUrl">
        <input id="searchName" type="text" placeholder="Pesquise seu personagem" v-model="searchValue"> 
        <!---@keyup="this.setHeroesUrl()" -->
        <button @click="setHeroesUrl">
            <i class="fa-solid fa-magnifying-glass"></i>
        </button>
    </form>
</template>

<script>
    export default {
        name: 'Search',
        props: [
            "apiUrl"
        ],
        data() {
            return {
                searchValue: ""
            }
        },
        methods: {
            setHeroesUrl() {
                if (this.searchValue !== '') {
                    this.$emit('setHeroesUrl', this.apiUrl + this.searchValue)
                    this.searchValue = ''
                }
                // let input = document.getElementById('searchName').value
                // input = input.toLowerCase()
                // let url = this.apiUrl

                // for (let i = 0; i < url.length; i++) {
                //     if (!url[i].innerHTML.toLowerCase()) {
                //         url[i].style.display = "none"
                //     } else {
                //         url[i].style.display = "list-item"
                //     }
                // }
            }
        }	
     }
</script>

<style lang="scss">
    @import '../assets/scss/variable.scss';
    @import '../assets/scss/styles/search.scss';
</style>