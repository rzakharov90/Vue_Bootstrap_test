<template>
    <form v-bind:class="{ error: !isValid }" class="main-search">
        <div class="main-search__row">
            <div class="main-search__elem-wrap">
                <select name="category" class="main-search__select" v-model="category">
                    <option class="main-search__option" v-for="elem in mainRowData.category.data" :value="elem.value">{{elem.name}}</option>
                </select>
            </div>
            <div class="main-search__elem-wrap">
                <input type="text" name="term" :placeholder="mainRowData.term.placeholder"  class="main-search__input"  v-model="term"/>
            </div>
            <div class="main-search__elem-wrap main-search__elem-wrap_submit">
                <button type="submit" class="main-search__submit">Найти</button>
            </div>
        </div>
        <div v-if="additionalRowData">
            <additionalRow :data="additionalRowData" v-on:updateValue="updateAdditionalRowValue"></additionalRow>
        </div>
    </form>
</template>


<script>
    import additionalRow from './additionalRow.vue';

    const Data = {
        category: {
            value: 'auto',
            data: [
                {
                    value: '',
                    name: 'Любая категория'
                },
                {
                    value: 'auto',
                    name: 'Автомобили'
                },
                {
                    value: 'beton',
                    name: 'Бетон'
                },
                {
                    value: 'pesok',
                    name: 'Песок'
                },
            ]
        },
        term: {
            placeholder: 'Поиск',
            value: ''
        }
    }
    
    const AddData = {
        auto: {
            brand: {
                type: 'select',
                name: 'brand',
                childs: ['model'],
                value: 'ford',
                placeholder: 'Выберите бренд',
                data: [{
                    value: 'vaz',
                    name: 'vaz'
                }, {
                    value: 'ford',
                    name: 'ford'
                }, {
                    value: 'bmw',
                    name: 'bmw'
                },{
                    value: 'opel',
                    name: 'opel'
                }, ]
            },
            model: {
                type: 'select',
                parent: 'brand',
                name: 'model',
                placeholder: 'Выберите марку',
                value: '',
                data: {
                    vaz: [{
                        value: 10,
                        name: '10'
                    }, {
                        value: 12,
                        name: '12'
                    }, {
                        value: 13,
                        name: '13'
                    }, {
                        value: 14,
                        name: '14'
                    }],
                    ford: [{
                        value: 'focus',
                        name: 'focus'
                    }, {
                        value: 'transit',
                        name: 'transit'
                    }, {
                        value: 'mondeo',
                        name: 'mondeo'
                    }],
                    bmw: [{
                        value: 'bfocus',
                        name: 'bfocus'
                    }, {
                        value: 'btransit',
                        name: 'btransit'
                    }, {
                        value: 'bmondeo',
                        name: 'bmondeo'
                    }]
                }
            },
            price_from: {
                type: 'input',
                name: 'price_from',
                placeholder: 'Цена от',
                value: 123123
            }
        },
        beton: {
            brand: {
                type: 'select',
                name: 'brand',
                childs: ['model'],
                value: 'bmw',
                placeholder: 'Выберите бренд',
                data: [{
                    value: 'vaz',
                    name: 'betonvaz'
                }, {
                    value: 'ford',
                    name: 'betonford'
                }, {
                    value: 'bmw',
                    name: 'betonbmw'
                },{
                    value: 'opel',
                    name: 'betonopel'
                }, ]
            },
            model: {
                type: 'select',
                parent: 'brand',
                name: 'model',
                placeholder: 'Выберите марку',
                value: '',
                data: {
                    vaz: [{
                        value: 10,
                        name: 'beton10'
                    }, {
                        value: 12,
                        name: 'beton12'
                    }, {
                        value: 13,
                        name: 'beton13'
                    }, {
                        value: 14,
                        name: 'beton14'
                    }],
                    ford: [{
                        value: 'focus',
                        name: 'betonfocus'
                    }, {
                        value: 'transit',
                        name: 'betontransit'
                    }, {
                        value: 'mondeo',
                        name: 'betonmondeo'
                    }],
                    bmw: [{
                        value: 'bfocus',
                        name: 'betonbfocus'
                    }, {
                        value: 'btransit',
                        name: 'betonbtransit'
                    }, {
                        value: 'bmondeo',
                        name: 'betonbmondeo'
                    }]
                }
            },
            price_from: {
                type: 'input',
                name: 'price_from',
                placeholder: 'betonЦена от',
                value: 123123
            },
            price_to: {
                type: 'input',
                name: 'price_to',
                placeholder: 'betonЦена до',
                value: 123123
            }
        }
    }


    export default {
        name: 'Search',
        props: {},
        data() {
            return {
                term: Data.term.value,
                category: Data.category.value,
                mainRowData: Data,
                AddRowData: {
                    auto: {
                        brand: null,
                        model: null,
                        price_from: null
                    },
                    beton: {
                        brand: null,
                        model: null,
                        price_from: null,
                        price_to: null,
                    }
                }
            }
        },
        methods: {
            updateAdditionalRowValue: function({value, name}){
                console.log('updateAdditionalRowValue', {value, name})
                this.AddRowData[this.category][name] = value;
                // ручное обновление значений зависимых элементов форм
                if(AddData[this.category][name].childs && AddData[this.category][name].childs.length) {
                    AddData[this.category][name].childs.forEach(el => {
                        if (this.AddRowData[this.category][el]) {
                            this.AddRowData[this.category][el] = '';
                        }
                    })
                }
            },
            getAdditionalData: function(AddData){
                console.log('getAdditionalData', AddData)
                const addData = Object.assign({}, AddData);
                let data = {};
                for (let name in addData) {
                    let property = addData[name];
                    data[name] = Object.assign({}, property);
                    data[name].value = this.AddRowData[this.category][name];
                    if (property.parent) {
                        let parentValue = this.AddRowData[this.category][property.parent];
                        data[name].data = property.data[parentValue];
                    }
                }
                return data;
            },
            getInitialAdditionalData: function(AddData) {
                console.log('getInitialAdditionalData', AddData);
                for (let name in this.AddRowData) {
                    for (let name2 in this.AddRowData[name]) {
                        this.AddRowData[name][name2] = AddData[name][name2].value || '';
                    }
                }
            },
            
        },
        computed: {
            isValid: function() {
                let valid = true
                for (let item in this.value) {
                    if (!this.value[item].isValid) {
                        valid = false
                    }
                }
                return valid
            },
            additionalRowData: function(){
                console.log('additionalRowData')
                if (!AddData[this.category]) {
                    return false;
                }
                return this.getAdditionalData(AddData[this.category]);

            },
            finallyData: function(){
                let data = Object.assign({}, {category: this.category, term: this.term});
                if (this.AddRowData[this.category]) {
                   data = Object.assign(data, this.AddRowData[this.category]);
                }
                return data;
            }
            
        },
        created: function(){
            this.getInitialAdditionalData(AddData);
        },
        components: {
            additionalRow
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
    .main-search__row_flex-wrap {
        flex-wrap: wrap;
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

    .main-search__option {
        padding: 5px;
    }

    .main-search__input {
        width: 100%;
        padding: 5px 10px;
        font-size: 16px;
        height: 100%;
    }

    .main-search__submit {
        ;
        padding: 5px 10px;
        font-size: 16px;
        height: 100%;
        background: violet;
        color: white;
        border: none;
        cursor: pointer;
    }
</style>