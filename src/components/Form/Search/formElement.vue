<template>
        <select name="data.name" class="main-search__select"  v-bind="data.name">
            <option class="main-search__option" v-for="option in data.data" :value="option.value">{{option.name}}</option>
        </select>
</template>

<script>
export default {
  name: 'formElement',
  props: {
    data: {
      default: {}
    }
  },
  data () {
    return {
      
    }
  },
    computed: {
        
    },
  methods: {
    
  }
}

</script>

<style scoped>

</style>