<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="container">
        <nav class="navbar navbar-expand-lg">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">
                    <img src="@/assets/logo.png" width="34" height="34"/>
                    Todo
                </a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                    <RouterLink class="nav-link active" aria-current="page" to="/">Home</RouterLink>
                    </li>
                    <li class="nav-item">
                    <RouterLink class="nav-link" to="/about">About</RouterLink>
                    </li>
                </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<style lang="scss" scoped>

</style>