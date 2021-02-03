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
                            <div class="text-6xl font-semibold">{{ currentTemp.actual }} C</div>
                            <div>Feels like {{ currentTemp.feels_like }} C</div>
                        </div>

                        <div class="mx-5">
                            <div class="font-semibold"></div>
                            <div>{{ location.name }}</div>
                        </div>
                    </div>

                    <div
                        v-for="item in current.currentWeather"
                        :key="item"
                    >
                        <img v-bind:src="'http://openweathermap.org/img/wn/' + item.icon + '@2x.png'" alt="">
                    </div>

                </div>

                <div class="future-weather text-sm bg-gray-800 px-6 py-8 overflow-hidden">
                    <div 
                        v-for="(day, index) in daily"
                        :key="index"
                        class="flex items-center"
                        :class="{ 'mt-8' : index > 0 }" 
                        v-if="index < 5" 
                    >
                        <div class="w-1/6 text-lg text-gray-200">{{ toDayOfWeek(day.dt) }}</div>
                        <div 
                            v-for="item in day.weather"
                            :key="item"
                            class="w-4/6 px-4 flex items-center"
                        >
                            <img v-bind:src="'http://openweathermap.org/img/wn/' + item.icon + '.png'" alt="">

                            <div class="ml-3">{{ item.description }}</div>
                        </div>
                        <div class="w-1/6 text-right">
                            <div>{{ Math.round(day.temp.max) }} C</div>
                            <div>{{ Math.round(day.temp.min) }} C</div>
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
                currentTemp: {
                    actual: '',
                    feels_like: '',
                },

                current: {
                    currentWeather: [],
                },
                

                daily: [],

                location: {
                    name: 'Bath, UK',
                    lat: 51.3779,
                    lon: -2.3591,
                }
            }
        },

        methods: {
            fetchData() {
                fetch(`/weather?lat=${this.location.lat}&lon=${this.location.lon}`)
                .then(response => response.json())
                .then(data => {
                    this.currentTemp.actual = Math.round(data.current.temp)
                    this.currentTemp.feels_like = Math.round(data.current.feels_like)

                    this.current.currentWeather = data.current.weather

                    this.daily = data.daily                    
                    console.log(this.current.currentWeather)
                })
            },
            toDayOfWeek(timestamp) {
                const newDate = new Date(timestamp*1000)
                const days = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT']

                return days[newDate.getDay()]
            }
        },
    }
</script>
