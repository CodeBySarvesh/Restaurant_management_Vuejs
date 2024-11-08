<template>
  <router-view />
</template>

<script>

export default {
  name: 'App',
 
 
}
</script>

<style>
body{
  padding:0;
  margin: 0;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}

.logo {
  height: 125px;
}

.register input, .login input, .add input,.update input{
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid rgb(36, 38, 39);
}

.register button,.login button,.add button,.update button {
  width: 300px;
  height: 40px;
  border: 1px solid rgb(36, 38, 39);
  color: black;
  background-color: skyblue;
  cursor: pointer;
}
</style>
