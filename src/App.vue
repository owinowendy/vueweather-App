<template>
  <div id="app" :class="typeof weather.main !='undefined' && weather.main.temp >16 ? 'warm':''">
   <main >
    
    <div class="search-box">
      <input type="text" class="search-box" placeholder="Search.."
      v-model="query"
     @keypress="fetchweather" />
      {{ query }}
      
    </div>
    <div class="weather-wrap" v-if="typeof weather.main !='undefined'">
      <div class="location-box">
        <div class="location">{{weather.name  }},{{ weather.sys.country }}</div>
        <div class="date">{{ dateBuilder() }}</div>
      </div>
<div class="weather-box">
  <div class="temp">{{ Math.round(weather.main.temp) }}&#176;c</div>
  <div class="weather">{{ weather.weather[0].main}}</div>
</div>
    </div>
   </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data (){
    return {
      posts: [],

      api_key:'592e2f769463caaf970a079efc46fad9',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{},
      error:null
    }
},
created() {
    this.getData()
},
methods: {
    async getData() {
      try {
        let response = await fetch("http://jsonplaceholder.typicode.com/posts")
        this.posts = await response.json()
      } catch (error) {
        console.log(error)
      }
    },
    fetchweather(e) {
    if (e.key == "Enter")
    {
      fetch (`${this.url_base}weather?q=${this.query}$units=metric$APPID=${this.api_key}`)
      .then(res => {return res.json();

      }).then(this.setResults);
    }

   axios.get(`https://api.openweathermap.org/data/2.5/weather?appid=${this.api_key}&q=${this.query}`)
        .then(response => {
          // Process the weather data
          this.weather = response.data;
        })
        .catch(error => {
          // Handle errors
          this.error = 'Error fetching weather data.';
          console.error('Error fetching weather data:', error);
        });
  },
    setResults(results){
      this.weather=results;
    },
    dateBuilder(){
    let d= new Date();
    let months=["January", "February","March","April","May","June","July","August","September","October","November",
  "December"];
  let days=["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Sartuday"];

  let day = days[d.getDate()];
  let date = d.getDate();
  let month = months[d.getMonth()];
  let year = d.getFullYear();
  return `${day} ${date}${month}${year}`;
  }
  },
  
}

</script>

<style scoped>

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
#app.warm{
  background-image: url('./assets/warm.jpg.jpg');
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
