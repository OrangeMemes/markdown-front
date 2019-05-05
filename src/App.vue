<template>
    <div id="app">
        <CreateControls @selected-changed="onSelectedIdChanged" @refresh-list="refreshList"></CreateControls>
        <DocumentsList :selectedId="selectedId" @selected-changed="onSelectedIdChanged" ref="list"></DocumentsList>
        <MarkdownDisplay :selectedId="selectedId" @selected-changed="onSelectedIdChanged" @refresh-list="refreshList"></MarkdownDisplay>
    </div>
</template>

<script>
    import DocumentsList from "@/components/DocumentsList";
    import MarkdownDisplay from "@/components/MarkdownDisplay";
    import CreateControls from "@/components/CreateControls";

    export default {
        name: 'app',
        components: {
            MarkdownDisplay,
            DocumentsList,
            CreateControls
        },
        data() {
            return {
                selectedId: "",
            }
        },
        methods: {
            onSelectedIdChanged(selectedId) {
                this.selectedId = selectedId;
            },

            refreshList() {
                this.$refs.list.refreshList();
            }
        }
    }

</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
