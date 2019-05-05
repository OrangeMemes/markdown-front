<template>
    <div class="controls">
        <div class="creation">
            <label>
                <input placeholder="Новая заметка" id="create-input" required v-model="inputValue">
            </label>
            <button @click="create">Создать</button>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    import qs from 'qs';


    export default {
        name: "CreateControls",
        data() {
            return {
                inputValue: ""
            }
        },
        methods: {
            create() {
                const requestBody = qs.stringify({
                    title: this.inputValue
                });

                const config = {
                    headers: {
                        'Content-Type': 'application/x-www-form-urlencoded'
                    }
                };

                axios.post('https://markdown-lypkin-back.herokuapp.com/documents', requestBody, config)
                    .then(response => {
                        this.inputValue = "";
                        this.$emit('refresh-list');
                        this.$emit('selected-changed', response.data)
                    })
            }
        }
    }
</script>

<style scoped>
    .controls {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
    }

    .creation {
        padding: 10px;
    }
</style>