<template>
    <form v-bind:class="{ error: !isValid }" class="main-search">
        <div class="main-search__row">
            <div class="main-search__elem-wrap">
                <select name="category" class="main-search__select">
                    <option>Любая категория</option>
                    <option>Пиломатериалы</option>
                    <option>Бетон</option>
                    <option>Песок</option>
                </select>
            </div>
            <div class="main-search__elem-wrap">
                <input type="text" name="term" placeholder="Поиск"  class="main-search__input"/>
            </div>
            <div class="main-search__elem-wrap main-search__elem-wrap_submit">
                <button type="submit" class="main-search__submit">Найти</button>
            </div>
        </div>
    </form>
</template>


<script>
export default {
  name: 'Search',
  props: {
  },
  data () {
    return {
      value: {
        tel: {
          value: '',
          isValid: true
        },
        mail: {
          value: '',
          isValid: true,
          name: 'mail'
        },
        name: {
          value: '',
          isValid: true,
          name: 'name',
          minLength: 10
        }
      }
    }
  },
  methods: {
    onValueChange: function (data) {
      console.log(data)
      this.value[data.name] = data
    }
  },
  computed: {
    isValid: function () {
      let valid = true
      for (let item in this.value) {
        if (!this.value[item].isValid) {
          valid = false
        }
      }
      return valid
    }
  },
  components: {
  }
}
</script>

<style>
    .main-search__row {
        display: flex;
        justify-content: space-between;
        align-items: stretch;
        border: 2px solid #ccc;
    }
    .main-search__elem-wrap {
        flex-grow: 1;
        border: 1px solid #ccc;
    }
    .main-search__elem-wrap_submit {
        flex-grow: 0;
    }
    .main-search__select {
        width: 100%;
        padding: 5px 10px;
        font-size: 16px;
        height: 100%;
        border: none;
    }
    .main-search__input {
        width: 100%;
        padding: 5px 10px;
        font-size: 16px;
        height: 100%;
    }
    .main-search__submit {;
        padding: 5px 10px;
        font-size: 16px;
        height: 100%;
        background: violet;
        color: white;
        border: none;
        cursor: pointer;
    }
</style>