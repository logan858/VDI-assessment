<template>
    <div class="categories">

        <select 
            class="cat-drop-down"
            @change="onChange($event)" 
            v-model="selection"
        >
          <option value="" disabled selected>Select a category...</option>
          <option v-bind:key="category.id" v-for="category in myData.categories" :value="category.id">
            {{category.category}}
          </option>
        </select>

        <div class="docues" v-if="isSelected">
            <Documents v-bind:selected-text="selection" :fetched-documents="fetchedDocuments"/>
        </div>

        <div class="controls" v-if="isSelected">
            <CrudControls/>
        </div>
    </div>
</template>

<script>
    import Documents from './Documents.vue'
    import CrudControls from './CrudControls.vue'
    import dummyData from '../../models/DummyDatabase'

    export default {
      name: 'Categories',
      components: { 
        Documents,
        CrudControls 
      },
      data() {
        return {
          isSelected: false,
          selection: "",
          fetchedDocuments: [
            {
              id:'1',
              category_id: '1',
              name: 'A',
            },
            {
              id:'2',
              category_id: '1',
              name: 'B',
            },
            {
              id:'3',
              category_id: '1',
              name: 'C',
            },
          ],
          myData: dummyData,
        }
      },
      methods: {
        async onChange(event) {
          console.log("TARGET: ", event.target.value)
          // let dummyData = await fetch('../../models/database.json')
          // console.log(dummyData)
          this.isSelected=true
          console.log(dummyData)
        },
        // fetchData(event) {
        //   console.log("fetching data!", event)
        // }
      }
    }
</script>

<style scoped>
    .categories {
      height: 100%;
      width: 100%;
    }
    .cat-drop-down {
      border: none;
      border-radius: 3px;
      width: 300px;
      max-width: 100%;
      height: 40px;
      outline: none;
      cursor: pointer;
      background: rgb(92, 92, 92);
      color: white;
    }
    .docues {
      margin-top: 20px;
      padding: 5px;
      background: rgba(0,0,0,0.2);
      border-radius: 3px;
      color: white;
      height: 75%;
      overflow-y: scroll;
    }
    .docues::-webkit-scrollbar {
      height: 0;
      width: 7px;
    }
    .docues::-webkit-scrollbar-thumb {
      background-color: rgb(168, 168, 168);
    }
</style>