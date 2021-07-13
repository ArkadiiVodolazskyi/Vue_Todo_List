<template>
	<div class="project" :class="{ completed: project.complete }">
		<div class="actions">
			<h3 @click="toggleShowDetails">{{ project.title }}</h3>
			<div class="icons">
				<span class="material-icons">edit</span>
				<span @click="deleteProject" class="material-icons">delete</span>
				<span @click="toggleComplete" class="material-icons">done</span>
			</div>
		</div>
		<div v-show="showDetails" class="details">
			<p>{{ project.details }}</p>
		</div>
	</div>
</template>

<script>
export default {
	props: ['project'],
	data() {
		return {
			showDetails: false,
			uri: 'http://localhost:3000/projects/' + this.project.id
		}
	},
	methods: {
		toggleShowDetails() {
			this.showDetails = !this.showDetails;
		},
		deleteProject() {
			fetch(this.uri, { method: 'DELETE' })
			.then(() => this.$emit('delete', this.project.id))
			.catch(err => console.log(err));
		},
		toggleComplete() {
			let d = new Date();
			d = `${d.getDate()}.${d.getMonth() + 1}.${d.getFullYear()} at ${d.getHours()}:${d.getMinutes()}`;
			fetch(this.uri, {
				method: 'PATCH',
				headers: { 'Content-Type': 'application/json' },
				body: JSON.stringify({ complete: !this.project.complete, dateChanged: d })
			}).then(() => this.$emit('complete'))
			.catch(err => console.log(err));
		}
	}
}
</script>

<style scoped lang="scss">
.project {
	transform: scale(0);
	opacity: 0;
	animation: zoomIn 0.2s forwards linear;
	margin: 20px auto;
	background: white;
	padding: 10px 20px;
	border-radius: 4px;
	box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
	border-left: 5px solid #e90074;
	transition: all 0.3s ease;
	&.completed {
		border-color: darken(green, 5%);
	}
}
h3 {
	cursor: pointer;
	user-select: none;
}
.actions {
	display: flex;
	justify-content: space-between;
	align-items: center;
}
.material-icons {
	font-size: 24px;
	margin-left: 10px;
	cursor: pointer;
	transition: all 0.3s ease;
	color: #bbb;
	&:hover {
		color: #e90074;
	}
}
</style>