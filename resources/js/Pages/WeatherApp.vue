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
                            <div class="text-6xl font-semibold"> C</div>
                            <div>Feels like C</div>
                        </div>

                        <div class="mx-5">
                            <div class="font-semibold"></div>
                            <div></div>
                        </div>
                    </div>

                    <div></div>
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
                location: {
                    name: 'Bath, uk',
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
                    console.log(data)
                })
            }
        }
    }
</script>
