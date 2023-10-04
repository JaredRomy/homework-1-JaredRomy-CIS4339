<template>
    <form v-cloak id="main">
        <h1>Facilities</h1>
        <ul>
            <li v-for="facility in facilities" :key="facility.name"
                @click="toggleActive(facility)" 
                :class="{ active: facility.active }">
                {{ facility.name }} <span>{{ formatCurrency(facility.price) }}</span>
            </li>
        </ul>
        <div class="total">
            Total: <span>{{ formatCurrency(total()) }}</span>
        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue';

// Data
const facilities = ref([
    { name: 'Ballroom', price: 5000, active: true },
    { name: 'Backyard', price: 400, active: false },
    { name: 'Wellness Area', price: 250, active: false },
    { name: 'Restaurant', price: 220, active: false },
]);

// Methods
const toggleActive = (facility) => {
    facility.active = !facility.active;
};

const total = () => {
    return facilities.value.reduce((sum, facility) => {
        return facility.active ? sum + facility.price : sum;
    }, 0);
};

const formatCurrency = (value) => {
    return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(value);
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@700&family=Shadows+Into+Light');

[v-cloak] {
  display: none;
}

*{
    margin:0;
    padding:0;
}

body{
    font:15px/1.3 'Open Sans', sans-serif;
    color: #5e5b64;
    text-align:center;
}

a, a:visited {
    outline:none;
    color:#389dc1;
}

a:hover{
    text-decoration:none;
}

section, footer, header, aside, nav{
    display: block;
}

form{
    background-color: #8931EF;
    border-radius: 2px;
    box-shadow: 0 1px 1px #ccc;
    width: 400px;
    padding: 35px 60px;
    margin: 50px auto;
}

form h1{
    color:#fff;
    font-size:64px;
    font-family:'Cookie', cursive;
    font-weight: normal;
    line-height:1;
    text-shadow:0 3px 0 rgba(0,0,0,0.1);
}

form ul{
    list-style:none;
    color:#fff;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    margin:20px 0 15px;
}

form ul li{
    padding:20px 30px;
    background-color:#a5949a;
    margin-bottom:8px;
    box-shadow:0 1px 1px rgba(0,0,0,0.1);
    cursor:pointer;
}

form ul li span{
    float:right;
}

form ul li.active{
    background-color:#87E911;
}

div.total{
    border-top:1px solid rgba(255,255,255,0.5);
    padding:15px 30px;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    color:#fff;
}

div.total span{
    float:right;
}
</style>
