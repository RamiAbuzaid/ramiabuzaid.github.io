<script setup>
import { ref, watchEffect } from 'vue'
import axios from 'axios';


let vendreData = ref(null);
let errorMessage = ref("");


const getData = async () => {
    try {
        const { data } = await axios(`https://reqres.in/api/users`)
        vendreData.value = data.data;
        console.log(data.data);
    } catch (err) {
        errorMessage.value = err
        console.log(err)
    }
}

watchEffect(() => {
    getData();
})



</script>

<template>
    <div class="container">
        <li v-for="user in vendreData">
            <div class="card">
                <img :src="user.avatar" />
                <section class="card-info">
                    <h6>{{ user.first_name }}<span class="lastname">{{ user.last_name }}</span></h6>
                    <a href="mailto:user.email">Contact</a>
                </section>
            </div>
        </li>
    </div>
</template>

<style scoped>
.container {
    margin: 10em 0;
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
