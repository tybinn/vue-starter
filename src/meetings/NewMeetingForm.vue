<template>
    <form @submit.prevent="addNewMeeting()">
        <h3>Dodaj nowe spotkanie</h3>
        <label>Nazwa</label>
        <input type="text" v-model="newMeeting.name">
        <label>Opis</label>
        <textarea v-model="newMeeting.description"></textarea>
        <button>Dodaj</button>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                newMeeting: {
                    name: '',
                    description: '',
                    participants: [],
                }
            };
        },
        methods: {
            addNewMeeting() {
                this.$emit('added',  Object.assign({}, this.newMeeting));
                this.newMeeting.name = '';
                this.newMeeting.description = '';
                this.newMeeting.participants = [];
            }
        }
    }
</script>