<template>
    <footer class="footer">
        <div class="footer__content">
            <div class="footer__content--left">
                <img class="footer__logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3d/DC_Comics_logo.svg/2048px-DC_Comics_logo.svg.png" alt="logo dc">
                <p class="footer__text">Projeto feito usando a api da <a href="https://www.superheroapi.com/" target="_blank">DC Comics.</a></p>
            </div>
        </div>
    </footer>
</template>

<script>
    export default {
        name: 'Footer'
    }
</script>

<style lang="scss">
    @import '../assets/scss/variable.scss';
    @import "../assets/scss/styles/footer.scss";
</style>