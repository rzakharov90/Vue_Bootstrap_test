<template>
        <select :name="data.name" class="main-search__select" v-on:change="updateValue($event.target.value)">
            <option class="main-search__option" v-for="option in data.data" :value="option.value" :key="option.value">{{option.name}}</option>
        </select>
</template>

<script>
    export default {
        name: 'SelectVue',
        props: {
            data: {
                default: {}
            }
        },
        data() {
            return {}
        },
        computed: {

        },
        methods: {
            updateValue: function(value){
                console.log(value)
                this.$emit('updateValue', {value, name: this.data.name})
            }
        }
    }
</script>

<style scoped>
</style>