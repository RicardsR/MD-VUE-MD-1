<template>
    <div class="nav-buttons">
        <button class="nav-button triangle-inactive" :class="{ triangle: isHomeActive, active: isHomeActive }" @click="showHome">HOME</button>
        <button class="nav-button triangle-inactive" :class="{ triangle: isAboutMeActive, active: isAboutMeActive }" @click="showAboutMe">ABOUT ME</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isHomeActive: false,
            isAboutMeActive: false,
        };
    },
    created() {
        const isFirstLoad = localStorage.getItem('isFirstLoad');

        if (isFirstLoad === null) {
            this.isHomeActive = true;
            this.isAboutMeActive = false;
            localStorage.setItem('isFirstLoad', 'true');
        } else {
            const lastActiveButton = localStorage.getItem('lastActiveButton');
            if (lastActiveButton === 'home') {
                this.isHomeActive = true;
                this.isAboutMeActive = false;
            } else if (lastActiveButton === 'aboutMe') {
                this.isHomeActive = false;
                this.isAboutMeActive = true;
            }
        }
    },
    methods: {
        showHome() {
            this.isHomeActive = true;
            this.isAboutMeActive = false;
            this.$emit("change-component", "home");
            localStorage.setItem('lastActiveButton', 'home');
        },
        showAboutMe() {
            this.isHomeActive = false;
            this.isAboutMeActive = true;
            this.$emit("change-component", "aboutMe");
            localStorage.setItem('lastActiveButton', 'aboutMe');
        },
    },
};
</script>

<style scoped>
.active {
    background-color: #8645E8;
    color: #fff;
}
</style>
