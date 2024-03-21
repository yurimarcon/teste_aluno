<script setup>
import {ref} from 'vue';

const number = ref(0);
</script>
<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
        <div class="container-fluid">
            <router-link class="navbar-brand" to="/">             
                <img src="https://cdn-icons-png.flaticon.com/512/188/188987.png" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">
                PokeVite
            </router-link>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                <li class="nav-item">
                    <router-link class="nav-link" to="/">Home</router-link>
                </li>
                <li class="nav-item">
                    <router-link class="nav-link" to="/about">About</router-link>
                </li>
                </ul>
            </div>
        </div>
    </nav>

    <!--Content-->
    <section class="main">
        <router-view>

        </router-view>
    </section>
    <footer class="bg-primary text-center text-light">
        {{ new Date().getFullYear()  }}
    </footer>
</template>

<style>
    body{
        min-height: 100vh;
        background: rgb(61,234,236);
        background: linear-gradient(0deg, rgba(61,234,236,1) 0%, rgba(0,95,102,1) 100%);
    }
    footer{
        position: fixed;
        bottom: 0;
        width: 100%;
        display: flex;
        text-align: center;
        justify-content: center;
        align-items: center;
        height: 40px;
    }
</style>