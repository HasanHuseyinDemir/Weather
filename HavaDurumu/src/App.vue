<template>
<div id="app" :class="typeof weather.main!='undefined'&& weather.main.temp> 16 ?'warm':'cold'">
<main>
  <div class="search-box">
    <input @keypress="fetchWeather" type="text" name="" v-model="query" id="" class="search-bar" placeholder="Ara..."/>
  </div>
  <div class="weather-wrap" v-if="typeof weather.main!='undefined'">
    <div class="location-box">
      <div class="location">{{weather.name}},{{weather.sys.country}}</div>
    </div>
  <div class="weather-box">
    <div class="temp">{{Math.floor(weather.main.temp)}}°C</div>
    <div class="weather">{{weather.weather[0].main}}</div>
  </div>
  </div>
</main>
</div>
</template>

<script>
export default{
  name:"app",
  data(){
    return{
      api_key:"c0883dee00ab6415efdc1a5218002e26",
      url_base:"https://api.openweathermap.org/data/2.5/",
      query:"",
      weather:{}
    }
  },
  methods: {
    fetchWeather(e){
      if(e.key=="Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).
        then(res=>{
          return res.json();
        }).then(this.setResults)
      }
    },
    setResults(results){
      console.log(results);
      this.weather=results;
    }
  },
}
</script>
<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;

}
body{
  font-family: "montserrat",sans-serif;
}
#app{
  background-image:url(../img/cold.jpg);
  background-size: cover;
  background-position: bottom;
  transition :.4s;
}
main{
  min-height: 100vh ;
  padding:25px;
  background-image:linear-gradient(to bottom,rgba(0,0,0,0.25),rgba(0,0,0,0.75));
}
.search-box{
  width: 100%;
  margin-bottom:30px;
}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color:#313131;
  font-size:20px;

  appearance: none;
  border:none;
  outline: none;
  background: none;
  background-color: rgba(255,255,255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition :0.4s;

  box-shadow:0px 0px 8px rgba(0,0,0, 0.25);
}
.search-box .search-bar:focus{
  background-color: rgba(255,255,255, 0.75)  ;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  border-radius: 16px;
}
.location-box .location{
  color:white;
  font-size:32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0, 0.25);
}
.location-box .date{
  color:white;
  font-size:20px;
  font-weight: 300;
  font-style:italic;
  text-align: center; 
}
.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  padding:10px 25px;
  color:white;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255,255,255,0.25);
  border-radius:16px;
  margin:30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather{
  color:white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
#app.warm{
  background-image: url(../img/warm.jpg);
}
</style>