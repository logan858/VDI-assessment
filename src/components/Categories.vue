<template>
    <div class="categories">

        <select 
            class="cat-drop-down"
            @change="onChange($event)" 
            v-model="selection"
        >
          <option value="" disabled selected>Select a category...</option>
          <option v-bind:key="category.id" v-for="category in categories" :value="category.id">
            {{category.category}}
          </option>
        </select>

        <div class="docues" v-if="isSelected">
            <div class="document-title">
              {{ selectedName }}
            </div>
            <Documents 
              v-if="filteredDocuments"
              v-bind:selected-text="selection" 
              :filtered-documents="filteredDocuments" 
              :is-edit="isEdit"
              v-on:delete-doc="deleteDoc"
              v-on:edit-doc="editDoc"
              v-on:show-edit="showEdit"
            />
        </div>

        <div class="controls" v-if="isSelected">
            <CreateDoc 
              v-bind:id-length="idLength" 
              :category-id="selection"
              v-on:submit-add="submitAdd"
            />
        </div>
    </div>
</template>

<script>
    import Documents from './Documents.vue'
    import CreateDoc from './CreateDoc.vue'
    import dummyData, { documents } from '../../models/DummyDatabase'

    export default {
      name: 'Categories',
      components: { 
        Documents,
        CreateDoc 
      },
      data() {
        return {
          isSelected: false,
          selection: "",
          selectedName: "",
          categories: dummyData.categories,
          documents: dummyData.documents,
          idLength: dummyData.documents.length,
          filteredDocuments: [],
          isEdit: []
        }
      },
      methods: {
        async onChange(event) {
          this.selection = event.target.value
          this.isSelected = true
          this.selectedName = this.categories[parseInt(event.target.value, 10) - 1].category 
          this.filteredDocuments = this.documents.filter(x => x.category_id == this.selection)
          this.isEdit = this.filteredDocuments.map(function(x) {
                return { 
                    id: [x.id],
                    edit: false
                }
            })
          this.idLength = documents.length
        },
        deleteDoc: function (id, objInd) {
          let ind = this.documents.findIndex(x => x.id === id)
          this.documents.splice(ind, 1)
          let ind2 = this.filteredDocuments.findIndex(x => x.id === id)
          this.filteredDocuments.splice(ind2, 1)
          this.isEdit.splice(objInd, 1)
        },
        showEdit: function(ind) {
          this.isEdit[ind].edit = !this.isEdit[ind].edit
        },
        editDoc: function (id, name, objInd) {
          let ind = this.documents.findIndex(x => x.id === id)
          documents[ind].name = name
          let ind2 = this.filteredDocuments.findIndex(x => x.id === id)
          this.filteredDocuments[ind2].name = name
          this.isEdit[objInd].edit = !this.isEdit[objInd].edit
        },
        submitAdd: function (name, catId, idLng) {
          let newDoc = {
            "id": idLng,
            "category_id": catId,
            "name": name,
            "created_at": new Date(Date.now()),
            "updated_at": new Date(Date.now())
          }
          this.documents.push(newDoc)
          this.filteredDocuments.push(newDoc)
          this.isEdit.push({
            id: idLng,
            edit: false
          })
          this.idLength = documents.length
        }
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
    .documents {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .document-title {
        margin-top: 10px;
        font-size: 18px;
    }
</style>