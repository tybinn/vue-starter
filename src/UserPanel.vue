<template>
    <div>
        <h2>Witaj {{ username }}</h2>
        <a @click="$emit('logout')">Wyloguj</a>
        <br>
    </div>
</template>

<script>
    import MeetingsPage from "./meetings/MeetingsPage.vue";

    export default {
        components: { MeetingsPage },
        props: ['username'],
        methods: {
            addNewMeeting(meeting) {
                this.meetings.push("nowe spotkanie");
            }
        }
    }
</script>
