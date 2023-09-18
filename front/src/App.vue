<template>
    <img alt="Vue logo" src="./assets/logo.png">
    <todos-list></todos-list>
</template>

<script>
const { io } = require("socket.io-client");
const socket = io(process.env.VUE_APP_SOCKET_DOMAIN);

import TodosList from './components/TodosList.vue';

export default {
    name: 'App',
    components: {
        TodosList
    },
    mounted() {
        socket.on('connect', () => {
            console.log(`Connect SocketId: ${socket.id}`);
        });

        socket.on("disconnect", () => {
            console.log(`Disconnect SocketId: ${socket.id}`);
        });
    },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
