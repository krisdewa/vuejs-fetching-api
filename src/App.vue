<template>
  <div>
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">VUE.JS Fetching Data API </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarCollapse"
          aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarCollapse">
          <ul class="navbar-nav me-auto mb-2 mb-md-0">
            <li class="nav-item">
              <router-link :to="{ name: 'home' }" class="nav-link" aria-current="page">HOME</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{ name: 'posts.index' }" class="nav-link">POSTS</router-link>
            </li>
          </ul>
          <!-- <form class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button class="btn btn-success" type="submit">Search</button>
          </form> -->
        </div>
      </div>
    </nav>

    <!-- render vue router -->
    <router-view></router-view>

  </div>
</template>

<script>

export default {
  name: 'App'
}
</script>

<style>
body {
  background-color: lightgray !important;
}

.mt-custom {
  margin-top: 110px;
}
</style>