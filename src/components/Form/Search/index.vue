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
                }
            }
        },
        methods: {
            updateAdditionalRowValue: function({value, name}){
                this.AddRowData[name] = value;
                // ручное обновление значений зависимых элементов форм
                if(AddData[this.category][name].childs && AddData[this.category][name].childs.length) {
                    AddData[this.category][name].childs.forEach(el => {
                        if (this.AddRowData[el]) {
                            this.AddRowData[this.category][el] = '';
                        }
                    })
                }
            },
            getAdditionalData: function(AddData){

                const addData = Object.assign({}, AddData);
                let data = {};
                for (let name in addData) {
                    let property = addData[name];
                    data[name] = Object.assign({}, property);
                    data[name].value = this.AddRowData[name];
                    if (property.parent) {
                        let parentValue = this.AddRowData[property.parent];
                        data[name].data = property.data[parentValue];
                    }
                }
                return data;
            },
            getInitialAdditionalData: function(AddData) {
                for (let name in AddData) {
                    this.AddRowData[name] = AddData[name].value || '';
                }
            }
        },
        computed: {
            additionalRow: function() {
                return this.additionalRowData[this.category];
            },
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
                if (!AddData[this.category]) {
                    return false;
                }
                return this.getAdditionalData(AddData[this.category]);

            }
            
        },
        created: function(){
            this.getInitialAdditionalData(AddData[this.category]);
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