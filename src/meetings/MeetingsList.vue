<template>
    <table v-if="meetings.length > 0">
        <thead>
        <tr>
            <th>Nazwa spotkania</th>
            <th>Opis</th>
            <th>Uczestnicy</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="meeting in meetings" :key="meeting.name">
            <td>{{ meeting.name }}</td>
            <td>{{ meeting.description }}</td>
            <td>
				<ul>
					<li v-for="username in meeting.participants" :key="username">{{ username }}</li>
				</ul>
			</td>
			<button v-if="meeting.participants.indexOf(username) < 0" @click="joinMeeting(meeting)" style="float: right; margin-right: 8px;">ZAPISZ SIĘ</button>
			<button v-else @click="leaveMeeting(meeting)" style="float: right;" >WYPISZ SIĘ</button>
			
			<button v-if="meeting.participants.length === 0" @click = "removeMeeting(meeting)" style="float: right; margin-right: 8px;">USUŃ PUSTE SPOTKANIE</button>
        </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        props: ['meetings', 'username'],
		methods: {
			joinMeeting(meeting) {
				this.$emit('joinMeeting', meeting)
			},
			removeMeeting(meeting) {
				this.$emit('removeMeeting', meeting);
			},
            leaveMeeting(meeting) {
                this.$emit('leaveMeeting', meeting)
            }
		}
        }
		

</script>
