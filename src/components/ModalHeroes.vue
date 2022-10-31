<template>
    <div class="modal">
        <div class="modal-content" v-if="showModal">
            <div class="modal-image" v-if="heroe">
                <img :src="imageUrl + heroesMarvel.thumbnail.path + '.jpg'" :alt="heroesMarvel.name">
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Modal',
        props: [
            "imageUrl",
            "heroesUrl"
        ],
        data() {
            return {
                showModal: false,
                heroe: {}
            }
        },
        methods: {
            fetchRequision() {
                let req = new Request(this.heroesUrl)
                fetch(req)
                    .then((resp) => {
                        return resp.json()
                    })
                    .then((data) => {
                        this.heroe = data
                        this.showModal = true
                    })
                    .catch((error) => {
                        console.log(error)
                    })
            },
            closeModal() {
                this.$emit('closeModal')
            }
        },
        created() {
            this.fetchRequision()
        }
    }
</script>

<style lang="scss">
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
        background: rgba(0, 0, 0, 0.395);    
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
            background-color: #FFFFFF;
            border-radius: 5px;
            box-shadow: 0 15px 30px #000, 0 10px 10px #000;   
        }
    }
</style>