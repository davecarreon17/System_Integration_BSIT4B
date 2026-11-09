<template>
  <v-app class="weather-bg">
    <v-main class="d-flex align-center justify-center pa-4">
      <v-container max-width="600">
        <!-- Search Bar -->
        <v-row class="mb-4">
          <v-col cols="12">
            <v-text-field
              v-model="searchQuery"
              @keyup.enter="searchLocation"
              placeholder="Search city (e.g. Manila, Pampanga, Tokyo)..."
              prepend-inner-icon="mdi-magnify"
              variant="outlined"
              density="comfortable"
              bg-color="rgba(255, 255, 255, 0.1)"
              hide-details
              rounded="pill"
              class="glass-input"
              :loading="loading"
            ></v-text-field>
          </v-col>
        </v-row>

        <!-- Error Alert kung sakaling may mali -->
        <v-alert
          v-if="errorMessage"
          type="error"
          variant="tonal"
          class="mb-4 text-white"
          closable
          @click:close="errorMessage = ''"
        >
          {{ errorMessage }}
        </v-alert>

        <!-- Main Weather Card -->
        <v-card class="glass-card pa-6 text-white mb-6" elevation="10" rounded="xl">
          <div class="d-flex justify-space-between align-start">
            <div>
              <h2 class="text-h4 font-weight-bold">{{ locationName }}</h2>
              <p class="text-subtitle-1 text-grey-lighten-2">{{ countryName }}</p>
            </div>
            <v-chip variant="flat" color="rgba(255, 255, 255, 0.2)" class="text-white">
              Today
            </v-chip>
          </div>

          <div class="d-flex align-center justify-space-between my-6">
            <div>
              <h1 class="text-h1 font-weight-thin">{{ currentWeather.temp }}°C</h1>
              <p class="text-h6 text-grey-lighten-1">{{ currentWeather.condition }}</p>
            </div>
            <div>
              <v-icon :icon="currentWeather.icon" size="100" class="text-yellow-lighten-2"></v-icon>
            </div>
          </div>

          <v-divider class="border-opacity-25 my-4"></v-divider>

          <!-- Weather Details Grid -->
          <v-row>
            <v-col cols="4" class="text-center">
              <v-icon icon="mdi-water-percent" size="24" class="mb-1"></v-icon>
              <div class="text-caption text-grey-lighten-2">Humidity</div>
              <div class="text-body-1 font-weight-bold">{{ currentWeather.humidity }}%</div>
            </v-col>
            <v-col cols="4" class="text-center">
              <v-icon icon="mdi-weather-windy" size="24" class="mb-1"></v-icon>
              <div class="text-caption text-grey-lighten-2">Wind Speed</div>
              <div class="text-body-1 font-weight-bold">{{ currentWeather.windSpeed }} km/h</div>
            </v-col>
            <v-col cols="4" class="text-center">
              <v-icon icon="mdi-speedometer" size="24" class="mb-1"></v-icon>
              <div class="text-caption text-grey-lighten-2">Pressure</div>
              <div class="text-body-1 font-weight-bold">{{ currentWeather.pressure }} hPa</div>
            </v-col>
          </v-row>
        </v-card>

        <!-- 3-Day Forecast Section -->
        <h3 class="text-white text-subtitle-1 font-weight-bold mb-3">3-Day Forecast</h3>
        <v-row>
          <v-col cols="4" v-for="(day, index) in forecast" :key="index">
            <v-card class="glass-card pa-4 text-white text-center" elevation="4" rounded="lg">
              <div class="text-body-2 font-weight-medium mb-2">{{ day.day }}</div>
              <v-icon :icon="day.icon" size="36" class="mb-2 text-yellow-lighten-2"></v-icon>
              <div class="text-h6 font-weight-bold">{{ day.temp }}°C</div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const searchQuery = ref('San Fernando')
const locationName = ref('San Fernando')
const countryName = ref('Philippines')
const loading = ref(false)
const errorMessage = ref('')

const currentWeather = ref({
  temp: 0,
  condition: 'Loading...',
  icon: 'mdi-weather-partly-cloudy',
  humidity: 0,
  windSpeed: 0,
  pressure: 1012,
})

const forecast = ref([])

// Tagapag-convert ng WMO Weather Codes galing sa API patungo sa Vuetify Icons at Descriptions
const getWeatherDetails = (code) => {
  switch (code) {
    case 0:
      return { condition: 'Clear Sky', icon: 'mdi-weather-sunny' }
    case 1:
    case 2:
    case 3:
      return { condition: 'Partly Cloudy', icon: 'mdi-weather-partly-cloudy' }
    case 45:
    case 48:
      return { condition: 'Foggy', icon: 'mdi-weather-fog' }
    case 51:
    case 53:
    case 55:
    case 56:
    case 57:
      return { condition: 'Drizzle', icon: 'mdi-weather-rainy' }
    case 61:
    case 63:
    case 65:
    case 66:
    case 67:
      return { condition: 'Rainy', icon: 'mdi-weather-pouring' }
    case 71:
    case 73:
    case 75:
    case 77:
      return { condition: 'Snowy', icon: 'mdi-weather-snowy' }
    case 95:
    case 96:
    case 99:
      return { condition: 'Thunderstorm', icon: 'mdi-weather-lightning' }
    default:
      return { condition: 'Fair', icon: 'mdi-weather-sunny' }
  }
}

// Function para kunin ang pangalan ng araw (e.g. Mon, Tue)
const getDayName = (dateString) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('en-US', { weekday: 'short' })
}

// Function para hanapin ang lat/long ng city at kumuha ng weather data
const searchLocation = async () => {
  if (!searchQuery.value.trim()) return
  loading.value = true
  errorMessage.value = ''

  try {
    // 1. Geocoding API para makuha ang Latitude at Longitude ng lungsod
    const geoRes = await fetch(`https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(searchQuery.value)}&count=1`)
    const geoData = await geoRes.json()

    if (!geoData.results || geoData.results.length === 0) {
      errorMessage.value = 'Location not found. Please try another city.'
      loading.value = false
      return
    }

    const { latitude, longitude, name, country } = geoData.results[0]
    locationName.value = name
    countryName.value = country || ''

    // 2. Weather API gamit ang nakuha na Lat/Long
    const weatherRes = await fetch(
      `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,relative_humidity_2m,weather_code,wind_speed_10m,surface_pressure&daily=weather_code,temperature_2m_max&timezone=auto`
    )
    const weatherData = await weatherRes.json()

    // I-update ang Current Weather
    const current = weatherData.current
    const details = getWeatherDetails(current.weather_code)
    currentWeather.value = {
      temp: Math.round(current.temperature_2m),
      condition: details.condition,
      icon: details.icon,
      humidity: current.relative_humidity_2m,
      windSpeed: current.wind_speed_10m,
      pressure: current.surface_pressure || 1012,
    }

    // I-update ang 3-Day Forecast (Kunin ang sunod na 3 araw mula index 1 hanggang 3)
    const daily = weatherData.daily
    const tempForecast = []
    for (let i = 1; i <= 3; i++) {
      if (daily.time[i]) {
        const dayDetails = getWeatherDetails(daily.weather_code[i])
        tempForecast.push({
          day: getDayName(daily.time[i]),
          icon: dayDetails.icon,
          temp: Math.round(daily.temperature_2m_max[i]),
        })
      }
    }
    forecast.value = tempForecast

  } catch (err) {
    console.error(err)
    errorMessage.value = 'Failed to fetch weather data. Please check your internet connection.'
  } finally {
    loading.value = false
  }
}

// Auto-load ang weather ng San Fernando pagka-open ng page
onMounted(() => {
  searchLocation()
})
</script>

<style scoped>
.weather-bg {
  background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
  min-height: 100vh;
}

.glass-card {
  background: rgba(255, 255, 255, 0.1) !important;
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.glass-input :deep(.v-field) {
  background: rgba(255, 255, 255, 0.1) !important;
  backdrop-filter: blur(10px);
  border-radius: 28px !important;
  color: white !important;
}

.glass-input :deep(input::placeholder) {
  color: rgba(255, 255, 255, 0.7) !important;
  opacity: 1;
}

.glass-input :deep(.v-field__outline) {
  border-color: rgba(255, 255, 255, 0.3) !important;
}

.glass-input :deep(input) {
  color: white !important;
}
</style>