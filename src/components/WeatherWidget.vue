<template>
  <div>
    <h2>Weather Widget</h2>

    <div class="input-container">
      <label for="city" class="label">Enter Location:</label>
      <input type="text" id="city" v-model="city" placeholder="Enter country/city name" class="input-field" />
      <button @click="getWeather" class="get-weather-btn">Get Weather</button>
    </div>

    <div v-if="weather" class="weather-info">
      <h3>{{ weather.name }}</h3>
      <p>Temperature: {{ weather.main.temp }}°C</p>
      <p>Weather: {{ weather.weather[0].description }}</p>
    </div>

    <p v-if="error" class="error-message">{{ error }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      city: "",
      weather: null,
      error: "",
    };
  },
  methods: {
    async getWeather() {
      if (this.city === "") {
        this.error = "Harap masukkan nama kota atau negara.";
        this.weather = null;
        return;
      }

      try {
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=b7bfca7b27a3485144fea086c50d09dc&units=metric`);
        this.weather = response.data;
        this.error = "";
      } catch (error) {
        console.error(error);
        this.weather = null;
        this.error = "Lokasi tidak ditemukan.";
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&family=Quicksand&family=Ubuntu+Condensed&display=swap");

.input-container {
  font-family: "Quicksand", sans-serif;
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.label {
  font-size: 18px;
  margin-bottom: 10px;
}

.input-field::placeholder {
  color: #999;
}

.input-field {
  padding: 10px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  width: 300px;
  margin-bottom: 10px;
  transition: box-shadow 0.3s ease;
}
.input-field:focus {
  outline: none;
  box-shadow: 0 0 5px #666365;
}

.input-field:focus::placeholder {
  color: #5c575b;
}

.input-container label {
  margin-right: 10px;
}

.input-container input {
  padding: 15px;
  margin-right: 10px;
  border-radius: 10px;
}

.get-weather-btn {
  padding: 10px 20px;
  text-align: center;
  background-color: #2196f3;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-family: "Quicksand", sans-serif;
  font-size: 14px;
  cursor: pointer;
  transition: transform 0.3s ease, background-color 0.3s ease;
}

.get-weather-btn:hover {
  background-color: #0c7cd5;
  transform: scale(1.1);
}

.get-weather-btn:active {
  background-color: #4b474a;
  transform: scale(0.9);
}

.weather-info {
  border: 1px solid #ccc;
  padding: 20px;
  margin-top: 5px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #f5f5f5;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h2 {
  font-family: "Quicksand", sans-serif;
  text-align: center;
}

.weather-info h3 {
  color: #333;
  font-size: 24px;
  margin-bottom: 10px;
}

.weather-info p {
  color: #666;
}

.error-message {
  color: black;
  margin-top: 10px;
}
</style>
