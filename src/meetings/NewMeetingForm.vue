<template>
	
    <form @submit.prevent="addNewMeeting()">
        <h3>Dodaj nowe spotkanie</h3>
        <label>Nazwa</label>
        <input type="text" v-model="newMeeting.name">
        <label>Opis</label>
        <textarea v-model="newMeeting.description"></textarea>
        <button v-if="newMeeting.name">Dodaj</button>
		<h6 v-else style="color:red">Spotkanie musi miec nazwę</h6>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                newMeeting: {participants: []}
            };
        },
        methods: {
            addNewMeeting() {
                this.$emit('added', this.newMeeting);
                this.newMeeting = {participants: []};
            }
        }
    }
</script>
