<template>
    <form v-bind:class="{ error: !isValid }" class="main-search">
        <div class="main-search__row">
            <div class="main-search__elem-wrap">
                <select name="category" class="main-search__select" v-model="category">
                    <option class="main-search__option">Любая категория</option>
                    <option class="main-search__option" value="wood">Автомобили</option>
                    <option class="main-search__option">Бетон</option>
                    <option class="main-search__option">Песок</option>
                </select>
            </div>
            <div class="main-search__elem-wrap">
                <input type="text" name="term" placeholder="Поиск"  class="main-search__input"  v-model="term"/>
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

    var Data = {
        wood: {
            brand: {
                type: 'select',
                name: 'brand',
                data: [{
                    value: 'vaz',
                    name: 'vaz'
                }, {
                    value: 'ford',
                    name: 'ford'
                }, {
                    value: 'bmw',
                    name: 'bmw'
                }, ]
            },
            model: {
                type: 'select',
                parent: 'brand',
                name: 'model',
                placeholder: 'Выберите марку',
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
            }
        }
    }


    export default {
        name: 'Search',
        props: {},
        data() {
            return {
                term: '',
                category: '',
                brand: 'vaz',
                model: '',
//                additionalRowData: {
//                    wood: {
//                        brand: {
//                            type: 'select',
//                            name: 'brand',
//                            data: [{
//                                value: 'vaz',
//                                name: 'vaz'
//                            }, {
//                                value: 'ford',
//                                name: 'ford'
//                            }, {
//                                value: 'bmw',
//                                name: 'bmw'
//                            }, ]
//                        },
//                        model: {
//                            type: 'select',
//                            parent: 'brand',
//                            name: 'model',
//                            data: {
//                                vaz: [{
//                                    value: 10,
//                                    label: 10
//                                }, {
//                                    value: 12,
//                                    label: 12
//                                }, {
//                                    value: 13,
//                                    label: 13
//                                }, {
//                                    value: 14,
//                                    label: 14
//                                }],
//                                ford: [{
//                                    value: 'focus',
//                                    label: 'focus'
//                                }, {
//                                    value: 'transit',
//                                    label: 'transit'
//                                }, {
//                                    value: 'mondeo',
//                                    label: 'mondeo'
//                                }]
//                            }
//                        }
//                    }
//                }
            }
        },
        methods: {
            onValueChange: function(data) {
                console.log(data)
                this.value[data.name] = data
            },
            updateAdditionalRowValue: function({value, name}){
                this[name] = value;
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
                if (!Data[this.category]) {
                    return false;
                }
                let finData = {},
                    data = Data[this.category];
                
                for (let name in data){
                    let d = data[name];
                    
                    finData[name] = {};
                    finData[name].name = d.name;
                    finData[name].parent = d.parent;
                    finData[name].placeholder = d.placeholder;
                    finData[name].type = d.type;
                    
                    if (d.parent) {
                        let parent = d.parent;
                        let parentValue = this[parent];
                        finData[name].data = d.data[parentValue];
                    } else {
                        finData[name].data =  d.data;
                    }
                    
                }
                return finData;
                
            }
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