<template>
<div id="app">
  <div class="header">
    <router-link to="/">
      <div class="logo">
        <img src="/ordinary.png">
      </div>
    </router-link>
    <div class="title">
      <h1> Opinions.com</h1>
    </div>
    <div class="posts">
      <router-link to="/post"><em>Add your opinion here!</em></router-link>
    </div>
  </div>
  <div class="content">
    <router-view />
  </div>
  <div class="footer">
    <p><router-link to="/admin">Admin Only!</router-link>
    +
    <a href="https://github.com/jpmlf/proj4">Git Hub</a>
    + 
    <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">Ratio</a>
    </p>
  </div>
</div>
</template>

<style>
html {
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
  font-size: 16px;
  background: #F8F0FB;
  padding: 0px;
  margin: 0px;
}

/* Header */
.header {
  display: flex;
  padding: 10px 100px 0px 100px;
  background-color: #211A1D;
  color: #E34A6F;
}

.title {
  margin-top: 5px;
}

.title h1 {
  font-size: 30px;
}

.content {
  padding: 20px 100px;
  min-height: 500px;
}

/* Footer */
.footer {
  height: 50px;
  padding: 20px 100px 0px 100px;
  font-size: 12px;
}

.footer a {
  color: #000;
}

h1 {
  font-size: 20px;
}

h2 {
  font-size: 14px;
}
img {
  height: 90px;
}
.posts {
  display: block;
  text-align: right
}
.posts a:link { color: #F8F0FB; text-decoration: none}
.posts a:visited { color: #F8F0FB; text-decoration: none}
.posts a:hover { color: #4267B2; text-decoration: underline}
.posts a:active { color: #F8F0FB; text-decoration: none}
</style>
