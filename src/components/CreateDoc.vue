<template>
    <div class="add-doc">
        <span v-on:click="showAdd" v-if="showAddTracker">
            Add Document
        </span>
        <span class="add-doc-input" v-else>
            <input 
                type="text" 
                v-on:keyup.enter="submitAdd($event)" 
                autofocus
            />
        </span>
    </div>
</template>

<script>

export default {
    name: "CreateDoc",
    props: ["idLength", "categoryId"],
    data() {
        return {
            showAddTracker: true
        }
    },
    methods: {
        showAdd: function () {
            this.showAddTracker = !this.showAddTracker
        },
        submitAdd: function(event) {
            if (event.target.value != "") {
                event.target.blur()
                this.showAddTracker = !this.showAddTracker
                this.$emit("submit-add", event.target.value, this.categoryId, this.idLength)
            }
        }
    }
}
</script>

<style scoped>
    .add-doc {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        color: white;
    }
    .add-doc span {
        border-radius: 3px;
        margin: 5px;
        padding: 5px;
        cursor: pointer;
        background: rgba(0,0,0,0.3);
    }
</style>
