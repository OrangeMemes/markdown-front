<template>
    <div class="documents-list">
        <div v-if="isLoading">loading</div>
        <div v-if="isErrored">error</div>
        <ul>
            <li v-for="doc in documents" v-bind:key="doc._id" v-bind:class="{ selected: doc._id === selectedId}" @click="clicked(doc)">
                {{doc.title}}
            </li>
        </ul>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: "DocumentsList",
        props: {
            selectedId: String
        },
        data() {
            return {
                isLoading: true,
                isErrored: false,
                documents: [],
            }
        },
        methods: {
            clicked: function (doc) {
                this.$emit('selected-changed', doc._id)
            },
            refreshList() {
                this.isLoading = true;
                this.isErrored = false;
                this.documents = [];

                axios.get('https://markdown-lypkin-back.herokuapp.com/documents')
                    .then(response => this.documents = response.data)
                    .catch(() => this.isErrored = true)
                    .finally(() => this.isLoading = false)
            }
        },
        created() {
           this.refreshList();
        }
    }
</script>

<style scoped>
.selected {
    background-color: aqua;
}
</style>