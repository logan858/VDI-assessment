<template>
    <div class="documents">
        <div class="document-title">
            {{ selectedText }}
        </div>

        <div class="document-items">
            <span>Technology and Intellectual Property</span>
            <span>Vendor Contracts</span>
            <span>Lease Contracts</span>
            <span v-bind:key="fetchedDocument.id" v-for="fetchedDocument in fetchedDocuments">
                {{fetchedDocument.name}}
            </span>
            
        </div>
    </div>
</template>


<script>

    export default {
        name: "Documents",
        props: [ 'selectedText', 'fetchedDocuments' ],
        data() {
            return {
                selDocument: "",
            }
        }
    }
</script>


<style scoped>
    .documents {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .document-title {
        margin-top: 10px;
        font-size: 18px;
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
</style>