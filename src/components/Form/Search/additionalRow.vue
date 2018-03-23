<template>
   <div class="main-search__row">
       <div v-for="elem in data" class="main-search__elem-wrap">
            <formElement :data="elem" v-on:updateValue="updateValue"></formElement>
       </div>
    </div>
</template>

<script>
    import formElement from './formElement.vue'
export default {
  name: 'AdditionalRow',
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
    updateValue: function(value){
        this.$emit('updateValue', value)
    }
  },
    components: {
        formElement
    }
}

</script>

<style scoped>

</style>