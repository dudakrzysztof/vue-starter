<template>
    <div v-if="item_length">
		<button @click="enter()">{{ buttonLabelToDisplay }}</button>
		<div v-if=clickStatus>
			<new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
		</div>
        <h2>Zaplanowane zajęcia ({{ item_length }})</h2>
        <meetings-list :meetings="meetings"></meetings-list>
    </div>
	<div v-else>
		<h4>Brak zaplanowanych spotkań</h4>
		<button @click="enter()">{{ buttonLabelToDisplay }}</button>
		<div v-if=clickStatus>
			<new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
		</div>
        <meetings-list :meetings="meetings"></meetings-list>
	</div>
</template>

<script>
    import NewMeetingForm from "./NewMeetingForm";
    import MeetingsList from "./MeetingsList";

    export default {
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
			enter(){
				this.clickStatus = true;
			}
        }
    }
</script>
