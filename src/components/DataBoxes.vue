<template>
    <div class="grid lg:grid-cols-2 gap-4 max-w-screen-sm md:max-w-screen-md lg:max-w-screen-lg mx-auto">
        <div class="shadow-xl bg-indigo-100 p-10 text-center rounded-xl text-indigo-900">
            <h3 class="text-3xl font-bold mb-4">Cases</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{numberWithCommas(stats.NewConfirmed)}}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{numberWithCommas(stats.TotalConfirmed)}}
            </div>
        </div>

        <div class="shadow-xl bg-indigo-200 p-10 text-center rounded-xl text-indigo-900">
            <h3 class="text-3xl font-bold mb-4">Deaths</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">New:</span>
                {{numberWithCommas(stats.NewDeaths)}}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Total:</span>
                {{numberWithCommas(stats.TotalDeaths)}}
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'DataBoxes',
        props: ['stats'],
        methods: {
            numberWithCommas(x) {
                return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
            }
        }
    }
</script>