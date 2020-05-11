<template>
    <div v-if="item_length">
		<button @click="enter()">{{ buttonLabelToDisplay }}</button>
		<div v-if=clickStatus>
			<new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
		</div>
        <h2>Zaplanowane zajęcia ({{ item_length }})</h2>
        <meetings-list :meetings="meetings" :username="username" @joinMeeting="addParticipant($event)" @removeMeeting="removeMeeting($event)"
			@leaveMeeting="removeParticipiant($event)"></meetings-list>
    </div>
	<div v-else>
		<h4>Brak zaplanowanych spotkań</h4>
		<button @click="enter()">{{ buttonLabelToDisplay }}</button>
		<div v-if=clickStatus>
			<new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
		</div>
        <meetings-list :meetings="meetings" :username="username"></meetings-list>
	</div>
</template>

<script>
    import NewMeetingForm from "./NewMeetingForm";
    import MeetingsList from "./MeetingsList";

    export default {
		
		props: ["username"],
        components: {NewMeetingForm, MeetingsList},
		
        data() {
            return {
                meetings: [],
				
				clickStatus: false
            };
        },
		computed: {
        item_length: function () {
            return this.meetings.length;
        },
		buttonLabelToDisplay() {
            return this.buttonLabel || 'DODAJ NOWE SPOTKANIE';
        }
    },
        methods: {
            addNewMeeting(meeting) {
                this.meetings.push(meeting);
				this.clickStatus = false;
            },
			
			addParticipant(meeting){
				meeting.participants.push(this.user);
			},
			
			removeParticipiant(meeting){
				meeting.participants.splice(meeting.participants.indexOf(this.user), 1)
			},
			
			removeMeeting(meeting){
				this.meetings.splice(this.meetings.indexOf(meeting), 1);
			},
			
			enter(){
				this.clickStatus = true;
			}
        }
    }
</script>
