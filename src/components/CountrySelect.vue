<template>
    <select @change="onChange()" v-model="selected" class="block w-full border p-3 rounded-xl max-w-screen-sm md:max-w-screen-md lg:max-w-screen-lg mx-auto mb-6">
        <option value="0">Select Country</option>
        <option v-for="country in countries" :value="country.ID">{{country.Country}}</option>
    </select>
</template>

<script>
    export default {
        name: 'CountrySelect',
        props: ['countries'],
        data() {
            return {
                selected: 0
            }
        },
        methods: {
            onChange() {
                const country = this.countries.find((item) => item.ID === this.selected)
                this.$emit('get-country', country)
            }
        }
    }
</script>