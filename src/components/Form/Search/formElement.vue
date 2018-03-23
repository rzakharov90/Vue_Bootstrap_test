<template>
    <component v-bind:is="type" :data="data" v-on:updateValue="updateValue"></component>
</template>

<script>
    import SelectVue from './Elements/SelectVue.vue';
    
    const types = {
        select: 'SelectVue'
    }
    export default {
        name: 'formElement',
        props: {
            data: {
                default: {}
            }
        },
        data() {
            return {
            }
        },
        computed: {
            type: function(){
                return types[this.data.type];
            }
        },
        methods: {
            updateValue: function(value){
                console.log(value)
                this.$emit('updateValue', value)
            }
        },
        components: {
            SelectVue,
        }
    }
</script>

<style scoped>
</style>