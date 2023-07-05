<template>
  <div class="app">
    <nav>
      <ul>
        <li>
          <router-link to="/location" class="nav-link" :class="{ active: $route.path === '/location' }">Location</router-link>
        </li>
        <li>
          <router-link to="/stopwatch" class="nav-link" :class="{ active: $route.path === '/stopwatch' }">Stopwatch</router-link>
        </li>
        <li>
          <router-link to="/weather" class="nav-link" :class="{ active: $route.path === '/weather' }">Weather</router-link>
        </li>
        <li>
          <router-link to="/tictactoe" class="nav-link" :class="{ active: $route.path === '/tictactoe' }">Tic Tac Toe</router-link>
        </li>
        <li>
          <router-link to="/photo" class="nav-link" :class="{ active: $route.path === '/photo' }">Photo</router-link>
        </li>
      </ul>
    </nav>
    <div class="content">
      <router-view></router-view>
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&family=Quicksand&family=Ubuntu+Condensed&display=swap");

.app {
  font-family: "Quicksand", sans-serif;
  display: grid;
  justify-items: center;
  background: linear-gradient(to bottom right, #ed0000, #110def);
}

nav {
  background-color: #f2f2f2;
  padding: 10px;
  display: flex;
  justify-content: center;
}

nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
}

nav ul li {
  margin-right: 10px;
}

nav ul li a {
  text-decoration: none;
  color: #333;
  padding: 5px;
  transition: all 0.3s ease;
}

nav ul li a:hover {
  transform: scale(1.1);
  color: #555;
  background-color: pink;
}

nav ul li a:active {
  color: #777;
  transform: scale(0.9);
  transition: transform 0.2s ease;
}

.content {
  display: flex;
  flex-direction: column;
}

.nav-link {
  border: none;
  border-radius: 5px;
  transition: color 0.3s ease, transform 0.3s ease;
}

.nav-link:hover {
  color: #fff;
  background: linear-gradient(to bottom right, #ed0000, #110def);
  transform: scale(1.1);
}

.nav-link:active {
  color: rgb(0, 0, 0);
  transform: scale(1.1);
}

.active {
  color: #fff;
  transform: scale(0.95);
  background: linear-gradient(to bottom right, #ed0000, #110def);
}
</style>
