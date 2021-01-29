<template>
    <div id="app" class="flex justify-center pt-16">
        <div class="text-white mb-8">
            <div class="places-input text-gray-800">
                <input type="text" class="w-full">
            </div>

            <div class="weather-container font-sans w-128 max-w-lg rounded-lg overflow-hidden bg-gray-900 shadow-lg mt-4">
                <div class="current-weather flex items-center justify-between px-6 py-8">
                    <div class="flex item-center">
                        <div>
                            <div class="text-6xl font-semibold">{{ currentWeather.temp }} C</div>
                            <div>Feels like {{ currentWeather.feels_like }} C</div>
                        </div>

                        <div class="mx-5">
                            <div class="font-semibold">{{ currentWeather.description }}</div>
                            <div>{{ location.city }}</div>
                        </div>
                    </div>

                    <div>{{ currentWeather.icon }}</div>
                </div>

                <div class="future-weather text-sm bg-gray-800 px-6 py-8 overflow-hidden">
                    <div class="flex items-center">
                        <div class="w-1/6 text-lg text-gray-200">MON</div>
                        <div class="w-4/6 px-4 flex items-center">
                            <div>Icon</div>

                            <div class="ml-3">More rain</div>
                        </div>
                        <div class="w-1/6 text-right">
                            <div>5 C</div>
                            <div>-2 C</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            this.fetchData()
        },

        data() {
            return {
                currentWeather: {
                    temp: '',
                    feels_like: '',
                    description: '',
                    icon: '',
                },

                location: {
                    city: 'Bath',
                    country: 'uk',
                }
            }
        },

        methods: {
            fetchData() {
                fetch(`/weather?city=${this.location.city}&country=${this.location.country}`)
                .then(response => response.json())
                .then(data => {
                    console.log(data)
                    this.currentWeather.temp = Math.round(data.main.temp)
                    this.currentWeather.feels_like = Math.round(data.main.feels_like)
                    this.currentWeather.description = data.weather.main
                    this.currentWeather.icon = data.weather.icon
                })
            }
        }
    }
</script>
