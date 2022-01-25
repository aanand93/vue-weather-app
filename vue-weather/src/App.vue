<template>
 <div id="app">
     <main>
         <div class="welcome">
             Check the weather!
         </div>
         <div class="search-box">
                <input 
                type="text" 
                class="search-bar" 
                placeholder="Type your location below (zip code or city or state)..." 
                v-model="query"
                @keypress="fetchWeather"
                />
         </div>
         <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
             <div class="location-box">
                 <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
                 <div class="date">{{ dateBuilder() }}</div>
             </div>
             <div class="weather-box">
                 <div class="temp">{{ Math.round(weather.main.temp) }}°F</div>
                 <div class="weather">{{ weather.weather[0].main }}</div>
             </div>
         </div>
     </main>
 </div>
</template>

<script>


export default {
  name: 'App',
  data	()	{
        return	{
            /* Create an .env file and add store your secret api key from openweathermap.com as VUE_APP_MY_ENV_VARIABLE */
            api_key: `${process.env.VUE_APP_MY_ENV_VARIABLE}`,
            url_base: "https://api.openweathermap.org/data/2.5/",
            query: '',
            weather: {}
        }
    },
    methods: {
        fetchWeather (e) {
            if (e.key == "Enter") {
                fetch(`${this.url_base}weather?q=${this.query}&units=imperial&appid=${this.api_key}`)
                .then(res => {
                    return res.json();
                }).then(this.setResults);
            }
        },
        setResults (results) {
            this.weather = results;
        },
        dateBuilder () {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Satday", "Sunday"];

            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();

            return `${day}, ${month} ${date}, ${year}`
        }
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
    font-family: sans-serif;
}

#app {
    background-image: url(https://images.unsplash.com/photo-1605721911519-3dfeb3be25e7?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1035&q=80);
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
}

main {
    min-height: 100vh;
    padding: 25px;

    background-image: linear-gradient(to bottom,rgba(0,0,0, 0.24),rgba(0,0,0, 0.75))
}

.welcome {
    color: white;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.5);
    padding: 0 0 20px 0;
}

.search-box {
    width: 100%;
    margin-bottom: 30px;
}

.search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;

    color: #313131;
    font-size: 20px;

    appearance: none;
    border: none;
    outline: none;
    background: none;

    box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
}

.search-box .search-bar:focus {
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.75);
    border-radius: 16px 0px 16px 0px;
}

.location-box .location {
    color: white;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.5);

}

.location-box .date {
    color: white;
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
}
.weather-box {
    text-align: center;
}
.weather-box .temp {
    display: inline-block;
    padding: 10px 25px;
    color: white;
    font-size: 102px;
    font-weight: 900;

    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.25);
    border-radius: 16px;
    margin: 30px 0px;

    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
    color: white;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
