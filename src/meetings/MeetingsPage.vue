<template>
    <div>
        <h2>Zajęcia</h2>
        <new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
        <meetings-list :authenticatedUsername="authenticatedUsername" :meetings="meetings" @join="joinMeeting($event)"
                       @leave="leaveMeeting($event)"
                       @remove="removeMeeting($event)" />
    </div>
</template>

<script>
    import NewMeetingForm from "./NewMeetingForm";
    import MeetingsList from "./MeetingsList";

    export default {
        components: {NewMeetingForm, MeetingsList},
        name: "MeetingPage.vue",
        props: ['authenticatedUsername'],
        data() {
            return {
                meetings: [],
                addingMeeting: false
            };
        },
        methods: {
            addNewMeeting(meeting) {
                this.meetings.push(meeting);
                this.addingMeeting = false;
            },

            joinMeeting(meetingName) {
                for (let i = 0; i < this.meetings.length; i++) {
                    if (this.meetings[i].name === meetingName) {
                        this.meetings[i].participants.push(this.authenticatedUsername);
                    }
                }
            },
            leaveMeeting(meetingName) {
                for (let i = 0; i < this.meetings.length; i++) {
                    if (this.meetings[i].name === meetingName) {
                        this.meetings[i].participants.splice(this.meetings[i].participants.indexOf(this.meetings[i]), 1);
                    }
                }
            },
            removeMeeting(meetingName) {
                for (let i = 0; i < this.meetings.length; i++) {
                    if (this.meetings[i].name === meetingName) {
                        this.meetings.splice(i, 1);
                    }
                }
            }
        }
    }
</script>
