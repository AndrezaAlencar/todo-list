<template>
    <div class="todoListContainer">
      <div class="heading">
        <h2 id="title">Todo List</h2>
          <add-item-form
          v-on:return="getList()"
          />
      </div>
      <list-view 
        :items="items" 
        v-on:reloadlist="getList()"
       />
    </div>
</template>

  <script>
    
    import addItemForm from "./addItemForm";
    import listView from "./listView";

    import axios from "axios";

        

    export default {
      components:{
        addItemForm,
        listView
      },

      data: function (){
        return {
          items: []
        }
      },

      methods: {
        getList() {
          axios.get('api/items')
          .then( response => {
            this.items = response.data
          })
          .catch( error => {
            console.log(error);
          } )
        }
      },
      created() {
        this.getList()
      }
    }
  </script>

  <style scoped>
    .todoListContainer {
     width: 25%;
     margin: auto;
    }

    .heading {
      background: #e6e6ee;
      padding: 10px;
      
    }
  
    #title {
      text-align: center;
      
    }
</style>
