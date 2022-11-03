<template>
    <div class="modal">
        <div class="modal__content" v-if="showModal">
            <div class="modal__image" v-if="heroe">
                <h1> {{ heroe.id}} - {{ heroe.name }}</h1>
            </div>
        </div>
        <h1 class="modal__error" v-else>Nenhuma informação encontrada</h1>
        <button class="modal__close" @click="closeModal">Fechar</button>
    </div>
</template>

<script>
    export default {
        name: 'ModalHeroes',
        props: [
            "apiUrl"
        ],
        data() {
            return {
                showModal: false,
                heroes: {},
                heroesUrl: ""
            }
        },
        methods: {
            fetchRequision() {
                document.querySelectorAll('[data-id]').forEach((el) => {
                    el.addEventListener('click', (e) => {
                        this.id = e.target.dataset.id
                        this.complementUrl = '/id/' + this.id + '.json'
                        let req = new Request(this.heroesUrl + this.complementUrl)
                        fetch(req)
                            .then((resp) => {
                                return resp.json()
                            }) 
                            .then((heroe) => {
                                this.heroes = heroe
                                this.showModal = true
                            })
                            .catch((error) => {
                                console.log(error)
                            })
                    })
                    
                })
            },
            closeModal() {
                this.$emit('closeModal')
            }
        },
        created() {
            this.heroesUrl = this.apiUrl
            this.fetchRequision()
        }
    }
</script>

<style lang="scss">
    @import "../assets/variable.scss";

    .modal {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        position: fixed;
        top: 0;
        left: 0;
        padding: 65px 10px 10px;
        width: 100%;
        height: 100vh;
        background: $black-two;    
        overflow: scroll;

        &__content {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            width: 100%;
            height: 54vw;
            position: relative;
            max-width: 510px;   
            background-color: $white;
            border-radius: 5px;
            box-shadow: 0 15px 30px $black, 0 10px 10px $black;   
        }

        &__error {
            color: $white;
            font-size: 1.5rem;
            font-weight: 600;
            text-align: center;
            margin-top: 2rem;
        }
    }
</style>