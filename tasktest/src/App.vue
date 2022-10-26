<template>
  <div id="app" :class="typeof weather1.main!='undefined'&& weather1.main.temp>16 ? 'warm':''
   "> 
    {{weather1}}
      <main>
          <div class="search-box">
              <input type="text" class="search-bar" placeholder="please search city" v-model="query" @keypress="fetchweather">
  
          </div>
          <div class="weather-wrap" v-if="typeof weather1.main!='undefined'" >
              <div class="location-box">
                  <div class="location">{{weather1.name}},{{weather1.sys.country}}
                    <br>Sunrise :{{weather1.sys.sunrise}}<br>sunset:{{weather1.sys.sunset}}<br>
                 visibility:   {{weather1.visibility}}</div>
                  <div class="date">{{dateBuilder()}}</div>
              </div>
              <div class="weather-box">
                  <div class="temp">{{Math.round(weather1.data.main.temp)}}°C</div><br>
                  
                  <div class="feels">Feels like:{{weather1.main.feels_like}}</div>
                  <div class="weather">{{weather1.weather[0].main}}</div>
              </div>
              
          </div>
      </main>
  </div>
  
  </template>
  
  <script>
    import axios from 'axios';
  export default {
      name: 'App',
      data() {
          return {
              api_key:  'f340b124adccb91f8876276eba3a98a4',
              url_base:'https://api.openweathermap.org/data/2.5/',
              query: '',
              weather1: {},
              
              
          }
  
      },
      methods: {
        fetchweather(e){
            if(e.key=="Enter"){
                console.log("Fetchweather function is working");
                
        let result =  axios.get(`${this.url_base}weather?q=${this.query}&units=matric&APPID=${this.api_key}`);
         result
  .then(res =>{
    console.log(this.weather1=res);
  });

  
//   .catch(error => console.error('(1) Inside error:', error))

//   return result
        // console.log("API Data", result);
        // this.weather1 = result;
          }
    }
},
          dateBuilder(){
            let d=new Date();
            let months=["January","February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let days=["Sunday","Monday","Tuesday","Wednesday","thursday","Friday","Saturday"];
            let day=days[d.getDay()];
            let date=d.getDate();
            let month=months[d.getMonth()];
            let year=d.getFullYear();
            return `${day} ${date} ${month} ${year}`;
          }
  
        }
    
  
  </script>
  
  <style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }
  
  body {
      font-family: 'moutserrat', sans-serif;
  }
  
  #app {
      background-image: url('./assets/cold.jpeg');
      background-size:cover;
      background-position:center;
      transition:0.7s;
  }
  #app.warm{
    background-image: url('./assets/warm.jpg');
  }
  
  
  main {
      min-height:100vh;
      padding: 70px;
      background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  }
  
  .search-box {
      width: 100%;
      margin-top: 40px;
      
  
  }
  
  .search-box .search-bar {
      display: block;
      width: 100%;
      padding: 15px;
      color: #313131;
      font-size: 20px;
      box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
      border-radius: 8px 8px 8px 8px;
      transition: 0.7s;
    
  }
  
  .search-box .search-bar :focus {
      box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.75);
      border-radius: 0px 16px 0px 16px;
  }
  
  .location-box .location {
      color: #FFF;
      font-size: 50px;
      font-weight: 900;
      font-style: italic;
      text-align: center;
  }
  
  .location-box .date{
      color: #FFF;
      font-size: 30px;
      font-weight: 900;
      font-style: italic;
      text-align: center;
  }
  
  .weather-box {
      text-align: center;
  }
  
  .weather-box .temp {   
      display: inline-block;
      padding: 20px 30px;
      color: #FFF;
      font-size: 102px;
      font-weight: 900;
      text-shadow: 3px 5px rgba(0, 0, 0, 0.25);
      background-color: rgba(225, 225, 225, 0.25);
      border-radius: 15px;
      margin: 30px 0px;
      box-shadow: rgba(0, 0, 0, 0.25);
  
  }
  .weather-box .feels {   
      display: inline-block;
      padding: 20px 30px;
      color: #FFF;
      font-size: 102px;
      font-weight: 900;
      text-shadow: 3px 5px rgba(0, 0, 0, 0.25);
      background-color: rgba(225, 225, 225, 0.25);
      border-radius: 15px;
      margin: 30px 0px;
      box-shadow: rgba(0, 0, 0, 0.25);
  
  }
  
  .weather-box .weather {
      color: #FFF;
      font-size: 102px;
      font-weight: 900;
      font-style: italic;
      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }
  </style>
  