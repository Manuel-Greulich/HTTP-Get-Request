<template>
    <div id="app">
        <h1>Todos</h1>
        <div class="lds-ring" v-if="loading == true">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
        <button v-else v-on:click="loadTodos">laden....</button>
        <hr />
        <ul>
            <li v-for="item in items" v-bind:key="item.id">
                {{ item.title }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "App",

    data: () => ({
        loading: false,
        items: [],
    }),

    methods: {
        async loadTodos() {
            this.loading = true;
            let apiUrl = "https://jsonplaceholder.typicode.com/todos";
            let response = await this.axios.get(apiUrl);
            this.items = response.data;
            this.loading = false;

            console.log(response);
        },
    },
};
</script>

<style>
.lds-ring {
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;
}
.lds-ring div {
    box-sizing: border-box;
    display: block;
    position: absolute;
    width: 64px;
    height: 64px;
    margin: 8px;
    border: 8px solid #fff;
    border-radius: 50%;
    animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    border-color: #000 transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
    animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
    animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
    animation-delay: -0.15s;
}
@keyframes lds-ring {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>
