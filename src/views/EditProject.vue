<template>
	<h2>Edit Project # {{ projectId }}</h2>
	<form @submit.prevent="handleSubmit">
		<label>Title:</label>
		<input type="text" required v-model="title">
		<label>Details:</label>
		<textarea required v-model="details"></textarea>
		<button>Save</button>
	</form>
	<p class="message" :class="{ active: showMessage }">Project Saved!</p>
</template>

<script>
export default {
	props: ['id'],
	data() {
		return {
			projectId: null,
			title: '',
			details: '',
			uri: 'http://localhost:3000/projects/' + this.id,
			showMessage: false
		}
	},
	mounted() {
		fetch(this.uri)
		.then(res => res.json())
		.then(data => {
			this.projectId = data.id;
			this.title = data.title;
			this.details = data.details;
		})
		.catch(err => console.log(err));
	},
	methods: {
		handleSubmit() {
			let d = new Date();
			d = `${d.getDate()}.${d.getMonth() + 1}.${d.getFullYear()} at ${d.getHours()}:${d.getMinutes()}`;
			fetch(this.uri, {
				method: 'PATCH',
				headers: { 'Content-Type': 'application/json' },
				body: JSON.stringify({
					title: this.title,
					details: this.details,
					dateChanged: d
				})
			})
			.then(() => {
				this.showMessage = true;
				setTimeout(() => {
					this.showMessage = false;
				}, 2000);
			})
			.then(() => {
				this.$router.push('/');
			})
			.catch(err => console.log(err));
		}
	}
}
</script>

<style>

</style>