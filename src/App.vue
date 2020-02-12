<template>
  <div id="app">
    <h1>weather app</h1>
    <form>
      <label for="city">City :</label>
      <input class="details" type="text" name="city" v-model="info.city">
      <label for="country">Country :</label>
      <input class="details" type="text" name="country" v-model="info.country">
      <input type="button" value="Submit" @click="add">
      <!-- <button type="submit" @click="add">Submit</button> -->
    </form>
    <div>
      <h3>{{ info.city }}, {{ info.country }}</h3>
      <p>{{ objects.temp }}°Celcius. Temperature from {{ objects.temp_min }} to {{ objects.temp_max }}, 
        pressure {{ objects.pressure }}hpa
      </p>
    </div>
    
  </div>
</template>


<script>
import axios from 'axios'

export default {
  name: 'App',

data() {
  return {
    info: {
      city: "",
      country: ""
    },
    objects: []
  }
},
methods: {
  add() {
    const details = {
        city: this.info.city,
        country: this.info.country
      };
    console.log(details);
    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${details.city},${details.country}&units=metric&appid=e2aedc30ba38e228fe0980f201104a00`)
    .then(res => {
      // console.log(res.data.main);
      this.objects=res.data.main
      console.log(this.objects)
    })
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
  color: #26292c;
  margin-top: 60px;
}
.details {
  background-color: transparent;
  border-bottom-color: 2px solid rgb(71, 133, 71);
  padding: 4px;
  border-radius: 0   
}
body {
  background-image: url("./assets/Weather.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;  
  background-size: cover;
}
</style>
