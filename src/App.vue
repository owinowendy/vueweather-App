<template>
  <div id="app" >
   <main >
    <img src="./assets/background.pjg" >
    <div class="search-box">
      <input type="text" class="search-box" placeholder="Search..">
      
    </div>
   </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data (){
    return {
      api_key:'71a20bcec7a998223da537a3f0bbe66b'
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
  padding: 0px;
  
}
body{
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}




</style>
