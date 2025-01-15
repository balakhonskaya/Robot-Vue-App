<template>
  <header>
    <nav>
      <ul>
        <li class="nav-item">
          <router-link :to="{name: 'Home'}" class="nav-link">
          <img class="logo" src="./assets/build-a-bot-logo.png" alt="logo" />Build-a-robot
        </router-link>
        </li>
        <li class="nav-item">
          <router-link :to="{name: 'Build'}" class="nav-link">
          Build
        </router-link>
        </li>
        <li class="nav-item">
          <router-link :to="{name: 'Search'}" class="nav-link">
          Search
        </router-link>
        </li>
      </ul>
    </nav>
  </header>
  <main>
    <!--<HomePage msg="Welcome to Your Vue.js App"/>-->
    <router-view/>
  </main>
</template>

<script sertup>
//  import HomePage from './home/HomePage.vue';
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

body {
  background: linear-gradient(to bottom, #555, #999);
  background-attachment: fixed;
}
main {
  margin: 0 auto;
  padding: 30px;
  background-color: white;
  width: 1400px;
  min-height: 300px;
}

header {
  background-color: #999;
  width: 1460px;
  margin: 0 auto;
}

ul {
  /*padding: 3px;*/
  display: flex;
}

.nav-link {
  text-decoration: none;
  color: inherit;
}

.nav-item {
  display: flex;
  flex-direction: row;
  align-content: center;
  align-items: center;
  font-size: 22px;
  border-right: 1px solid #bbb;
}

.logo {
  vertical-align: middle;
  height: 30px;
  margin: 0 10px 10px 0;
}

body {
  background: linear-gradient(to bottom, #555, #999);
  background-attachment: fixed;
}
main {
  margin: 0 auto;
  padding: 30px;
  background-color: white;
  width: 1400px;
  min-height: 300px;
}

header {
  background-color: #999;
  width: 1460px;
  margin: 0 auto;
}

ul {
  padding: 3px;
  display: flex;
}

.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1px solid #bbb;
}

.logo {
  vertical-align: middle;
  height: 30px;
  margin: 0 10px 10px 0;
}

.router-link-active {
  color: white;
}
</style>
