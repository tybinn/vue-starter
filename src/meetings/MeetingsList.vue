<template>
    <table v-if="meetings.length > 0">
        <thead>
        <tr>
            <th>Nazwa spotkania</th>
            <th>Opis</th>
            <th>Uczestnicy</th>
            <th></th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="meeting in meetings" :key="meeting.name">
            <td>{{ meeting.name }}</td>
            <td>{{ meeting.description }}</td>
            <td >
                <ul v-for="participant in meeting.participants">
                    <li> {{participant}}</li>
                </ul>
            </td>
            <td>
                <button @click="join(meeting.name)" v-if="!userJoined(meeting.participants)">Zapisz się</button>
                <button @click="leave(meeting.name)" v-if="userJoined(meeting.participants)">Wypisz się</button> &nbsp;
                <button @click="remove(meeting.name)" v-if="meeting.participants.length===0">Usuń spotkanie</button>
            </td>
        </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        props: ['meetings', 'authenticatedUsername'],
        methods: {
            join(meetingName){
                this.$emit('join', meetingName);
            },
            leave(meetingName) {
                this.$emit('leave', meetingName);
            },
            remove(meetingName) {
                this.$emit("remove", meetingName);
            },
            userJoined(participants) {
                if (participants == null || participants.length === 0) return false;
                return participants.includes(this.authenticatedUsername);
            }
        }
    }
</script>