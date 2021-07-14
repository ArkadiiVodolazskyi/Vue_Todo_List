<template>
	<h2>Add Project</h2>
	<form @submit.prevent="handleSubmit">
		<label>Title:</label>
		<input type="text" required v-model="title">
		<label>Details:</label>
		<textarea required v-model="details"></textarea>
		<button>Add Project</button>
	</form>
	<p class="message" :class="{ active: showMessage }">New Project Added!</p>
</template>

<script>
export default {
	data() {
		return {
			title: '',
			details: '',
			showMessage: false
		}
	},
	methods: {
		handleSubmit() {
			const newProject = {
				title: this.title,
				details: this.details,
				complete: false
			}

			fetch('http://localhost:3000/projects/', {
				method: 'POST',
				headers: { 'Content-Type': 'application/json' },
				body: JSON.stringify(newProject)
			}).then(() => {
				this.showMessage = true;
				setTimeout(() => {
					this.showMessage = false;
				}, 2000);
				this.title = '';
				this.details = '';
			})
			.catch(err => console.log(err));
		}
	}
}
</script>

<style lang="scss">
form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
		transition: all 0.2s linear;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    box-sizing: border-box;
    height: 100px;
		resize: none;
		width: 100%;
		transition: all 0.2s linear;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
		cursor: pointer;
		transition: all 0.2s linear;
    background-color: #00ce89;
		&:hover {
			background-color: darken($color: #00ce89, $amount: 10%);
		}
  }
	.message {
		margin-top: 1rem;
		text-align: center;
		padding: 10px;
		color: white;
		border-radius: 6px;
    background-color: green;
		transition: all 0.5s linear;
		opacity: 0;
		visibility: hidden;
		&.active {
			opacity: 1;
			visibility: visible;
		}
	}
</style>