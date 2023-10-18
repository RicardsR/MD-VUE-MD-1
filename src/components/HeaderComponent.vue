<template>
    <div>
        <header class="header" :style="{ backgroundColor: headerBackgroundColor }">
            <div class="header-logo">
                <img class="header-logo-img" src="@/assets/logo_white.svg" alt="Logo" />
                <h1>KRAKEN.FM</h1>
            </div>
            <div class="header-user">
                <div class="user-info" v-if="isLoggedIn">
                    <img class="avatar" :style="{ borderColor: avatarColor }" :src="logo" alt="User avatar" />
                    <span class="username">{{ full_name }}</span>
                    <div class="header-devider"></div>
                </div>
                <button @click="toggleLogin" v-if="!isLoggedIn" class="button">LOGIN</button>
                <button @click="toggleLogin" v-if="isLoggedIn" class="button logout">LOGOUT</button>
            </div>
        </header>
    </div>
</template>

<script>
function getRandomVibrantColor() {
    const hue = Math.floor(Math.random() * 360);
    const saturation = 70 + Math.floor(Math.random() * 30);
    const lightness = 50 + Math.floor(Math.random() * 10);

    return `hsl(${hue}, ${saturation}%, ${lightness}%)`;
}

export default {
    data() {
        return {
            user: {
                name: "Ričards",
                surname: "Reinsons",
                code: "IT21016",
            },
            isLoggedIn: false,
            headerBackgroundColor: '#45404B',
            avatarColor: getRandomVibrantColor(),
        };
    },
    computed: {
        full_name() {
            return `${this.user.name} ${this.user.surname}`;
        },
        logo() {
            return require("@/assets/user-logo.png");
        },
    },
    methods: {
        toggleLogin() {
            if (this.isLoggedIn) {
                const confirmLogout = window.confirm("Do you want to log out?");
                if (confirmLogout) {
                    this.logout();
                }
            } else {
                const confirmLogin = window.confirm("Do you want to log in?");
                if (confirmLogin) {
                    this.login();
                    this.avatarColor = getRandomVibrantColor();
                }
            }
        },
        login() {
            this.isLoggedIn = true;
            this.headerBackgroundColor = '#8645E8';
            this.$emit("login");
        },
        logout() {
            this.isLoggedIn = false;
            this.headerBackgroundColor = '#45404B';
            this.$emit("logout");
        },
    },
};
</script>