<template>
    <div class="nav__item">{{ name }}</div>
</template>

<script>
export default {
    props: {
        name: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped lang="scss">
.nav__item {
    text-decoration: none;
    cursor: pointer;
    color: #afb1c2;
    transition: 0.4s;
    position: relative;

    &:before {
        content: '';
        bottom: 0;
        right: 0;
        position: absolute;
        width: 0;
        height: 3px;
        background-color: #62f9d6;
        transition: 0.4s;
    }

    &:hover {
        color: #ffffff;

        &:before {
            width: 100%;
            transition: 0.4s;
            left: 0;
        }
    }

    &:after {
        content: '';
        z-index: -1;
        bottom: 0;
        right: 0;
        position: absolute;
        width: 0;
        height: 3px;
        background-color: #c74b4c;
        transition: 0.4s 0.3s;
    }

    &:hover {
        color: #ffffff;

        &:after {
            width: 100%;
            transition: 0.4s;
            left: 0;
        }
    }
}
</style>