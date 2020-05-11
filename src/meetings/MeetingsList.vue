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
				<ol>
					<li v-for="item in participants" :key="item.id">{{ item }}</li>
				</ol>
			</td>
			<button @click="addParticipants(username)" style="float: right; ">ZAPISZ SIĘ</button>
			<button style="float: right; padding-left:20px;">USUŃ PUSTE SPOTKANIE</button>
        </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        props: ['meetings', 'username'],
		data() {
            return {
                participants: []
            }
        },
        methods: {
            addParticipants(username) {
                this.participants.push(username);
            }
        }
		
    }
</script>
