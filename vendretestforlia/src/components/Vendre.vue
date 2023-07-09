<script setup>
import { ref, watchEffect } from 'vue';
import axios from 'axios';

const vendreData = ref(null);
const errorMessage = ref("");
const currentPage = ref(1);

const getData = async (page) => {
    try {
        const { data } = await axios(`https://reqres.in/api/users?page=${page}`);
        vendreData.value = data.data;
        console.log(data.data);
    } catch (err) {
        errorMessage.value = err;
        console.log(err);
    }
};

watchEffect(() => {
    getData(currentPage.value);
});


const changePage1 = () => currentPage.value = 1
const changePage2 = () => currentPage.value = 2

console.log(currentPage.value, "ee")

</script>

<template>
    <div class="container">
        <li v-for="user in vendreData" :key="user.id">
            <div class="card">
                <img :src="user.avatar" />
                <section class="card-info">
                    <h6>{{ user.first_name }}<span class="lastname">{{ user.last_name }}</span></h6>
                    <a :href="'mailto:' + user.email">Contact</a>
                </section>
            </div>
        </li>
        <section class="button-container">
            <button @click="changePage1">1</button>
            <button @click="changePage2">2</button>
        </section>
    </div>
</template>
<style scoped>
.container {
    margin: 10em 0em 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.lastname {
    margin-left: 5px;
}

img {
    border-radius: 50%;
}

li {
    list-style: none;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0.3em;
}

.card {
    padding: 1em;
    border: 1px solid gainsboro;
    border-radius: 3px;
    background-color: #ecbbbb;

}

.card-info {
    text-align: center;
}

a:hover {
    opacity: 0.7;
    transition: 0.4s ease-in-out;
}

a {
    text-decoration: none;
    color: #fff;
}

button {
    cursor: pointer;
    padding: 0.5em;
    background: oldlace;
    border-radius: 3px;
    color: black;
}

.button-container {
    top: 0;
    margin-top: 1em;
    position: absolute;
}

@media (min-width: 768px) {
    .card {
        flex-direction: row;
        align-items: flex-start;
    }

    .card img {
        margin-right: 10px;
    }

    .lastname {
        display: inline;
        margin-left: 5px;
    }


}
</style>
