<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <font-awesome-icon 
            icon="plus-square"
            @click="addItem()"
            :class=" [ item.name ? 'active' : 'inactive', 'plus']"
            v-on:return="$emit('')"
        />
    </div>
</template>

<script>
import axios from 'axios';
// import mutate from 'swrv';

    export default{
        props:['items'],
        // const :{ data, error, isValidating, mutate } = useSWRV(key, fetcher, options),
        data: function(){
            return{
                item: {
                    name:""
                }
            }
        },
        methods: {
            addItem(){
                if( this.item.name == ''){
                    return;
                }

                axios.post('api/item/store', {
                    item: this.item
                })
                .then( response => {
                 
                })
                .catch( error => {
                    console. log( error );
                })
            }
        }
    }
</script>

<style scoped>
    .addItem {
       display: flex;
       justify-content: center;
       align-items: center; 
    }
    input {
        background: #f7f7f7;
        border: 0px;
        outline: none;
        padding: 5px;
        margin-right: 10px;
        width: 50%;
    }
    .plus {
        font-size: 20px;
    }
    .active {
        color: #00ce25;
    }

    .inactive{
        color: #9999;
      
    }

</style>