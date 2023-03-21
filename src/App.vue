c<template>
  <div id="app" >
   <main >
    
    <div class="search-box">
      <input type="text" class="search-box" placeholder="Search.."
      v-model="query"
     @keypress="fetchweather" />
      {{ query }}
      
    </div>
    <div class="weather-wrap">
      <div class="location-box">
        <div class="location">Northhampton,UK </div>
        <div class="date">Friday 17 March 2023</div>
      </div>
<div class="weather-box">
  <div class="temp">9</div>
  <div class="weather">Rain</div>
</div>
    </div>
   </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data (){
    return {
      api_key:'824acb4150fa4b34582f27164f6639c0',
      url_base:'https://api.openweathermap.org/data/3.0/',
      query:'',
      weather:{}
      

    }
    
  },
  method:{
fetchweather(e) {
  if (e.key == "Enter")
  {
    fetch (`${this.api_base}weather? q=${this.query}$units=metric$APPID=${this.api_key}`)
    .then(res => {return res.json();

    }).then(this.setResults);
  }
},
setResults(results){
  this.weather=results;
}
  }

}
</script>

<style>

body{
  font-family:'Times New Roman', Times, serif;
  font-weight: bold;

}
#app {
 
  background-image: url('./assets/back.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  
}

 main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient( to bottom ,rgba(0,0,0,0.25), rgba(0,0,0,0.75) );
 }

 .search-box{
  width: 200px;
  margin-bottom: 30px;
  min-height: 5vh;
 }
 .search-box .search-box {
display: block;
width: 100pc;
padding: 15px;
color: #313131;
font-size: 20px;
appearance: none;
border: none;
outline: none;
background: none;
background-color: rgba(255,255,255,0.5);
border-radius: 0px 16px 0px 16px;
transition: 0.4s;
box-shadow: 0px 8px 0px;
 }
 .search-box .search-box:focus {
  background-color:rgba(255,255,255,0.75) ;
  box-shadow: 0px 16px 0px;
 }
 
 .location-box .location  {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);

 }
.location-box .date  {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style:italic;
  
}
.weather-box {
  text-align: center;
}
.weather-box .temp  {
display: inline-block;
padding: 10px 25px;
color: #FFF;
font-size: 102px;
font-weight: 900;


text-shadow: 3px 6px rgba(0,0,0,0.25);
background-color: rgba(255,255,255,0.25);
border-radius: 16px;
margin: 30px 0px;

box-shadow: 3px 6px rgba(0,0,0,0.25);

}
.weather {
  color: #FFF;
  font-size: 32px;
  font-size: 48px; 
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  font-style: italic;
  font-weight: 700;
}
</style>
