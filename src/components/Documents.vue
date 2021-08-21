<template>
    <div class="documents">
        <div class="document-items">
            <span v-bind:key="filteredDocument.id" v-for="(filteredDocument, index) in filteredDocuments">
                <span id="doc-title" v-if="this.isEdit[index].edit">
                    <input 
                        type="text" 
                        v-on:keyup.enter="submitEdit($event, filteredDocument.id)"
                        :placeholder="filteredDocument.name"
                    />
                </span>
                <span id="doc-title" v-else>
                    {{ filteredDocument.name }}
                </span>
                <span class="doc-controls" v-on:click="deleteDoc(filteredDocument.id)">
                    x
                </span>
                 <span class="doc-controls" v-on:click="editDoc(filteredDocument.id)">
                    -
                </span>
            </span>
        </div>
    </div>
</template>


<script>
    export default {
        name: "Documents",
        props: [ 'selectedText', 'filteredDocuments', 'isEdit' ],
        methods: {
            deleteDoc: function (id) {
                let objInd = this.isEdit.findIndex(x => x.id == id)
                this.$emit('delete-doc', id, objInd)
            }, 
            editDoc: function (id) {
                let objInd = this.isEdit.findIndex(x => x.id == id)
                this.$emit('show-edit', objInd)
            },
            submitEdit: function (event, id) {
                event.target.blur()
                let objInd = this.isEdit.findIndex(x => x.id == id)
                this.$emit('edit-doc', id, event.target.value, objInd)
            }
        },
    }
</script>


<style scoped>
    .documents {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .document-items {
        margin: 20px;
        width: 75%;
        display: flex;
        flex-direction: column;
    }
    .document-items span {
        border-radius: 3px;
        margin: 5px;
        padding: 5px;
        background: rgba(0,0,0,0.3);
    }
    #doc-title {
        float:left;
        background: none;
    }
    .doc-controls {
        cursor: pointer;
        float: right;
    }
</style>