<template>
  <v-app class="weather-dashboard-bg theme-sunny">
    <!-- Top Static Navigation Bar -->
    <v-app-bar color="transparent" flat class="px-md-8 px-2 pt-2">
      <div class="d-flex align-center">
        <v-avatar color="primary" size="40" class="mr-3 elevation-4">
          <v-icon icon="mdi-weather-partly-cloudy" color="white"></v-icon>
        </v-avatar>
        <span class="text-h6 font-weight-bold text-white tracking-wide">ClimaPulse</span>
      </div>

      <v-spacer></v-spacer>

      <!-- Static Search Bar -->
      <v-text-field
        placeholder="Search city..."
        prepend-inner-icon="mdi-magnify"
        variant="solo"
        density="compact"
        hide-details
        rounded="pill"
        class="glass-input d-none d-sm-flex"
        style="max-width: 380px;"
        readonly
      ></v-text-field>

      <v-spacer></v-spacer>

      <!-- Static Unit Switcher & Theme Icon -->
      <div class="d-flex align-center gap-2">
        <v-btn-toggle
          model-value="C"
          rounded="pill"
          density="compact"
          color="white"
          class="glass-toggle mr-2"
        >
          <v-btn value="C" size="small" class="text-caption font-weight-bold">°C</v-btn>
          <v-btn value="F" size="small" class="text-caption font-weight-bold">°F</v-btn>
        </v-btn-toggle>

        <v-btn icon="mdi-palette" variant="text" color="white"></v-btn>
      </div>
    </v-app-bar>

    <v-main class="px-md-8 px-4 py-6">
      <v-container fluid class="max-width-xl">
        <v-row>
          <!-- Left Column: Weather Hero & Highlights -->
          <v-col cols="12" lg="8">
            <!-- Hero Card -->
            <v-card class="glass-card main-hero pa-6 pa-md-8 mb-6" rounded="xl" flat>
              <v-row align="center">
                <v-col cols="12" sm="7">
                  <div class="d-flex align-center mb-2">
                    <v-icon icon="mdi-map-marker" color="red-accent-2" class="mr-1"></v-icon>
                    <span class="text-h5 font-weight-bold text-white">San Fernando, Philippines</span>
                  </div>
                  <p class="text-subtitle-2 text-grey-lighten-2 mb-6">Monday, October 19, 2026</p>

                  <div class="d-flex align-baseline">
                    <span class="text-h1 font-weight-bold text-white mr-2">32°</span>
                    <span class="text-h5 text-grey-lighten-1">C</span>
                  </div>

                  <div class="text-h6 text-white font-weight-medium mt-1">
                    Sunny with Clear Skies
                  </div>
                  <div class="text-body-2 text-grey-lighten-2">
                    Feels like 36° · High 34° · Low 25°
                  </div>
                </v-col>

                <v-col cols="12" sm="5" class="text-center">
                  <v-icon
                    icon="mdi-weather-sunny"
                    size="160"
                    color="amber-lighten-2"
                    class="weather-hero-icon"
                  ></v-icon>
                </v-col>
              </v-row>
            </v-card>

            <!-- Static Highlights Grid -->
            <div class="text-h6 text-white font-weight-bold mb-3">Today's Highlights</div>
            <v-row class="mb-6">
              <v-col cols="6" sm="3">
                <v-card class="glass-card pa-4 text-center h-100" rounded="lg" flat>
                  <v-icon icon="mdi-weather-windy" color="cyan-lighten-3" size="28" class="mb-2"></v-icon>
                  <div class="text-caption text-grey-lighten-2">Wind Speed</div>
                  <div class="text-subtitle-1 font-weight-bold text-white mt-1">12 km/h</div>
                  <div class="text-caption text-grey-lighten-3 opacity-70">NW direction</div>
                </v-card>
              </v-col>

              <v-col cols="6" sm="3">
                <v-card class="glass-card pa-4 text-center h-100" rounded="lg" flat>
                  <v-icon icon="mdi-water-percent" color="blue-lighten-3" size="28" class="mb-2"></v-icon>
                  <div class="text-caption text-grey-lighten-2">Humidity</div>
                  <div class="text-subtitle-1 font-weight-bold text-white mt-1">78%</div>
                  <div class="text-caption text-grey-lighten-3 opacity-70">Dew point: 24°C</div>
                </v-card>
              </v-col>

              <v-col cols="6" sm="3">
                <v-card class="glass-card pa-4 text-center h-100" rounded="lg" flat>
                  <v-icon icon="mdi-white-balance-sunny" color="amber-lighten-2" size="28" class="mb-2"></v-icon>
                  <div class="text-caption text-grey-lighten-2">UV Index</div>
                  <div class="text-subtitle-1 font-weight-bold text-white mt-1">8 High</div>
                  <div class="text-caption text-grey-lighten-3 opacity-70">Very High Risk</div>
                </v-card>
              </v-col>

              <v-col cols="6" sm="3">
                <v-card class="glass-card pa-4 text-center h-100" rounded="lg" flat>
                  <v-icon icon="mdi-leaf" color="green-lighten-2" size="28" class="mb-2"></v-icon>
                  <div class="text-caption text-grey-lighten-2">Air Quality (AQI)</div>
                  <div class="text-subtitle-1 font-weight-bold text-white mt-1">42 Good</div>
                  <div class="text-caption text-grey-lighten-3 opacity-70">PM2.5: 10 µg/m³</div>
                </v-card>
              </v-col>
            </v-row>

            <!-- Static Hourly Forecast -->
            <div class="d-flex align-center justify-space-between mb-3">
              <span class="text-h6 text-white font-weight-bold">24-Hour Forecast</span>
              <span class="text-caption text-grey-lighten-2">Local Time</span>
            </div>
            <v-card class="glass-card pa-4 mb-6" rounded="xl" flat>
              <div class="d-flex flex-row overflow-x-auto gap-3 pb-2 no-scrollbar">
                <div class="hourly-item text-center pa-3 rounded-lg flex-shrink-0">
                  <div class="text-caption text-grey-lighten-2 mb-2">Now</div>
                  <v-icon icon="mdi-weather-sunny" color="amber-lighten-2" size="28" class="my-1"></v-icon>
                  <div class="text-body-1 font-weight-bold text-white mt-1">32°</div>
                  <div class="text-caption text-blue-lighten-3 mt-1"><v-icon icon="mdi-water" size="10"></v-icon> 0%</div>
                </div>

                <div class="hourly-item text-center pa-3 rounded-lg flex-shrink-0">
                  <div class="text-caption text-grey-lighten-2 mb-2">10 AM</div>
                  <v-icon icon="mdi-weather-sunny" color="amber-lighten-2" size="28" class="my-1"></v-icon>
                  <div class="text-body-1 font-weight-bold text-white mt-1">33°</div>
                  <div class="text-caption text-blue-lighten-3 mt-1"><v-icon icon="mdi-water" size="10"></v-icon> 5%</div>
                </div>

                <div class="hourly-item text-center pa-3 rounded-lg flex-shrink-0">
                  <div class="text-caption text-grey-lighten-2 mb-2">11 AM</div>
                  <v-icon icon="mdi-weather-partly-cloudy" color="light-blue-lighten-3" size="28" class="my-1"></v-icon>
                  <div class="text-body-1 font-weight-bold text-white mt-1">34°</div>
                  <div class="text-caption text-blue-lighten-3 mt-1"><v-icon icon="mdi-water" size="10"></v-icon> 10%</div>
                </div>

                <div class="hourly-item text-center pa-3 rounded-lg flex-shrink-0">
                  <div class="text-caption text-grey-lighten-2 mb-2">12 PM</div>
                  <v-icon icon="mdi-weather-partly-cloudy" color="light-blue-lighten-3" size="28" class="my-1"></v-icon>
                  <div class="text-body-1 font-weight-bold text-white mt-1">32°</div>
                  <div class="text-caption text-blue-lighten-3 mt-1"><v-icon icon="mdi-water" size="10"></v-icon> 20%</div>
                </div>

                <div class="hourly-item text-center pa-3 rounded-lg flex-shrink-0">
                  <div class="text-caption text-grey-lighten-2 mb-2">1 PM</div>
                  <v-icon icon="mdi-weather-pouring" color="blue-lighten-2" size="28" class="my-1"></v-icon>
                  <div class="text-body-1 font-weight-bold text-white mt-1">29°</div>
                  <div class="text-caption text-blue-lighten-3 mt-1"><v-icon icon="mdi-water" size="10"></v-icon> 80%</div>
                </div>
              </div>
            </v-card>
          </v-col>

          <!-- Right Column: 7-Day Forecast & Saved Locations -->
          <v-col cols="12" lg="4">
            <!-- Static 7-Day Forecast -->
            <div class="text-h6 text-white font-weight-bold mb-3">7-Day Forecast</div>
            <v-card class="glass-card pa-4 mb-6" rounded="xl" flat>
              <v-list class="bg-transparent pa-0">
                <v-list-item class="px-2 py-2">
                  <div class="d-flex align-center justify-space-between w-100 text-white">
                    <span class="font-weight-medium" style="width: 80px;">Mon Today</span>
                    <div class="d-flex align-center" style="width: 120px;">
                      <v-icon icon="mdi-weather-sunny" color="amber-lighten-2" class="mr-2" size="22"></v-icon>
                      <span class="text-caption text-grey-lighten-2 text-truncate">Sunny</span>
                    </div>
                    <div class="text-right">
                      <span class="font-weight-bold">34°</span>
                      <span class="text-grey-lighten-2 text-caption ml-1">25°</span>
                    </div>
                  </div>
                </v-list-item>

                <v-list-item class="px-2 py-2">
                  <div class="d-flex align-center justify-space-between w-100 text-white">
                    <span class="font-weight-medium" style="width: 80px;">Tue</span>
                    <div class="d-flex align-center" style="width: 120px;">
                      <v-icon icon="mdi-weather-partly-cloudy" color="light-blue-lighten-3" class="mr-2" size="22"></v-icon>
                      <span class="text-caption text-grey-lighten-2 text-truncate">Partly Cloudy</span>
                    </div>
                    <div class="text-right">
                      <span class="font-weight-bold">33°</span>
                      <span class="text-grey-lighten-2 text-caption ml-1">24°</span>
                    </div>
                  </div>
                </v-list-item>

                <v-list-item class="px-2 py-2">
                  <div class="d-flex align-center justify-space-between w-100 text-white">
                    <span class="font-weight-medium" style="width: 80px;">Wed</span>
                    <div class="d-flex align-center" style="width: 120px;">
                      <v-icon icon="mdi-weather-pouring" color="blue-lighten-2" class="mr-2" size="22"></v-icon>
                      <span class="text-caption text-grey-lighten-2 text-truncate">Heavy Rain</span>
                    </div>
                    <div class="text-right">
                      <span class="font-weight-bold">28°</span>
                      <span class="text-grey-lighten-2 text-caption ml-1">23°</span>
                    </div>
                  </div>
                </v-list-item>
              </v-list>
            </v-card>

            <!-- Static Saved Locations -->
            <div class="text-h6 text-white font-weight-bold mb-3">Other Locations</div>
            <v-card class="glass-card pa-4 mb-2" rounded="lg" flat>
              <div class="d-flex align-center justify-space-between text-white">
                <div>
                  <div class="text-subtitle-1 font-weight-bold">Tokyo</div>
                  <div class="text-caption text-grey-lighten-2">Japan · Clear Sky</div>
                </div>
                <div class="d-flex align-center">
                  <v-icon icon="mdi-weather-night" color="indigo-lighten-3" size="32" class="mr-3"></v-icon>
                  <span class="text-h5 font-weight-bold">18°</span>
                </div>
              </div>
            </v-card>

            <v-card class="glass-card pa-4 mb-2" rounded="lg" flat>
              <div class="d-flex align-center justify-space-between text-white">
                <div>
                  <div class="text-subtitle-1 font-weight-bold">London</div>
                  <div class="text-caption text-grey-lighten-2">UK · Drizzle</div>
                </div>
                <div class="d-flex align-center">
                  <v-icon icon="mdi-weather-rainy" color="blue-lighten-3" size="32" class="mr-3"></v-icon>
                  <span class="text-h5 font-weight-bold">14°</span>
                </div>
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>


<script setup lang="ts">
//@ts-nocheck

</script>


<style scoped>
.weather-dashboard-bg {
  font-family: 'Plus Jakarta Sans', sans-serif;
  min-height: 100vh;
}

.theme-sunny {
  background: linear-gradient(135deg, #1e3c72 0%, #2a5298 50%, #6dd5ed 100%);
}

.glass-card {
  background: rgba(255, 255, 255, 0.12) !important;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.18) !important;
  box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.2);
}

.glass-input :deep(.v-field) {
  background: rgba(255, 255, 255, 0.15) !important;
  backdrop-filter: blur(10px);
  color: white !important;
  border-radius: 50px;
}

.glass-toggle {
  background: rgba(255, 255, 255, 0.15) !important;
  backdrop-filter: blur(8px);
}

.hourly-item {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.12);
  min-width: 80px;
}

.weather-hero-icon {
  filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.3));
}

.max-width-xl {
  max-width: 1400px;
}

.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.no-scrollbar::-webkit-scrollbar {
  display: none;
}

.gap-2 {
  gap: 8px;
}

.gap-3 {
  gap: 12px;
}
</style>