<template>
    <div class="container">
        <Search></Search>
    </div>
<!--  <div class="hello">
    <b-container class="cmn-gap">
        <b-navbar toggleable="md" type="dark" variant="info" sticky=true>
            <b-navbar-brand href="#">Лого</b-navbar-brand>
            <b-collapse is-nav id="nav_collapse">
                <b-navbar-nav class="ml-auto">
                    <b-nav-item active>Пиломатериалы</b-nav-item>
                    <b-nav-item>Цемент</b-nav-item>
                    <b-nav-item>Плитка</b-nav-item>
                </b-navbar-nav>
            </b-collapse>
        </b-navbar>
    </b-container>
    <b-container class="cmn-gap">
        <b-row align-v="center" align-h="between">
            <b-col cols="12" sm="3" class="col">Логотип</b-col>
            <b-col class="col" cols="12" sm="7">
                 <b-nav fill >
                    <b-nav-item active>Пиломатериалы</b-nav-item>
                    <b-nav-item>Цемент</b-nav-item>
                    <b-nav-item>Плитка</b-nav-item>
                    <b-nav-item disabled>Песок</b-nav-item>
                  </b-nav>
            </b-col>
        </b-row>
    </b-container>
    <b-container class="cmn-gap">
        <b-row align-v="start" align-h="between">
            <b-col cols="12" sm="4" class="col">Первый</b-col>
            <b-col cols="12" sm="3" class="col">Второй</b-col>
            <b-col cols="12" sm="4" align-self="end" class="col">Третий</b-col>
        </b-row>
    </b-container>
      
<b-container>
    <b-form-row no-gutters>
        <b-col cols="3">
            <b-form-select v-model="category" class="mb-3">
              <option :value="null">Please select an option</option>
              <option value="a">Option A</option>
              <option value="b" disabled>Option B (disabled)</option>
              <optgroup label="Grouped Options">
                <option :value="{'C':'3PO'}">Option with object value</option>
                <option :value="{'R':'2D2'}">Another option with object value</option>
              </optgroup>
            </b-form-select>
        
        </b-col>
        <b-col cols="3">
            
        </b-col>
        <b-col cols="3">
            <b-form-select v-model="city" class="mb-3">
              <option :value="null">Please select an option</option>
              <option value="a">Option A</option>
              <option value="b" disabled>Option B (disabled)</option>
              <optgroup label="Grouped Options">
                <option :value="{'C':'3PO'}">Option with object value</option>
                <option :value="{'R':'2D2'}">Another option with object value</option>
              </optgroup>
            </b-form-select>
        
        </b-col>
    
    
    </b-form-row>
      
      
  </b-container>  
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <Form></Form>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
      <br>
  </div>-->
</template>

<script>
import Form from '@/components/Form/Form.vue'
import Search from '@/components/Form/Search.vue'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
        category: null,
        city: null,
    }
  },
  components: {
    Form, Search
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .cmn-gap {
        margin-bottom: 40px;
    }
    .col {
        border: 4px solid red;
        padding: 15px;
    }
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
