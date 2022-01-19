<template>
  <nav class="main-nav">
      <ul>
            <li>
                <router-link :to="{name: 'Home'}">All Projects</router-link>
            </li>
            <li>
                <router-link :to="{name: 'AddProject'}">Add Project</router-link>
            </li>
      </ul>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
    .main-nav {
        text-align: center;
        margin: 40px auto;
    }
    .main-nav ul{
        display: flex;
        justify-content: center;
        list-style: none;
    }
    .main-nav a,
    .main-nav li {
        display: inline-block;
        text-decoration: none;
        margin: 0 10px;
        color: #999;
        font-size: 18px;
    }
    a.router-link-active {
        border-bottom: 2px solid #00ce89;
        padding-bottom: 4px;
    }
</style>