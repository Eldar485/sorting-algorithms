<template>
    <footer class="footer">
        <div class="footer__content">
            <div class="footer__logo" @click="scrollToTop">ET</div>
            <div class="footer__links">
                <a href="https://www.linkedin.com/in/eldar-tahtarov-8672a2268/"><v-nav-item class="footer__link" name="Linkedin"></v-nav-item></a>
                <a href="https://github.com/Eldar485"><v-nav-item class="footer__link" name="Github"></v-nav-item></a>
            </div>
        </div>
    </footer>
</template>

<script>

import VNavItem from "@/components/v-Nav-item";

export default {
    components: {VNavItem},
    methods: {
        scrollToTop() {
            window.scrollTo({
                top: 0,
                behavior: 'smooth'
            });
        }
    }
}
</script>

<style scoped lang="scss">
a {
    text-decoration: none;
}
.footer {
    width: 100%;
    background: #1c1d25;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;

    &__content {
        max-width: 25rem;
        text-align: center;
    }
    &__logo {
        color: #f3f3f3;
        cursor: pointer;
        font-size: 5rem;
        position: relative;
        transition: 0.4s ease;

        &:after {
            content: 'Top';
            transition: 0.4s ease-in-out;
            font-size: 1.2rem;
            position: absolute;
            top: 2rem;
            opacity: 0;
        }
        &:hover {
            &:after {
                opacity: 1;
                transform: translateX(1rem);
            }
        }
    }
    &__links {
        margin-top: 1rem;
        width: 12rem;
        display: flex;
        justify-content: space-between;
    }
    &__link {
        color: #afb1c2;
        z-index: 1;
        font-size: 1.3rem;
    }
}
</style>