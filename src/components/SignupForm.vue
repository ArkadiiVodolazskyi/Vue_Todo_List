<template>
	<form @submit.prevent="handleSubmit">
		<label>Email:</label>
		<input
			type="email"
			required
			v-model="email"
		>

		<label>Password:</label>
		<input
			type="password"
			required
			v-model="password"
		>
		<div v-if="passwordError" class="error">{{ passwordError }}</div>

		<label>Role:</label>
		<select v-model="selected">
			<option
				v-for="jobOption in jobOptions"
				:value="jobOption.value"
				:key="jobOption.value"
			>
				{{ jobOption.text }}
			</option>
		</select>

		<label>Skills (Enter):</label>
		<input type="text" v-model="tempSkill" @keyup="addSkill">
		<div v-for="skill in skills" :key="skill" class="pill">
			<span @click="deleteSkill(skill)">
				{{ skill }}
			</span>
		</div>

		<div class="terms">
			<input type="checkbox" required v-model="terms">
			<label>Accept the terms and conditions</label>
		</div>

		<div class="submit">
			<button >Create an account</button>
		</div>
	</form>
	<p>Email: {{ email }}</p>
	<p>Password: {{ password }}</p>
	<p>Selected: {{ selected }}</p>
	<p>Terms accepted: {{ terms }}</p>
	<p>passwordError: {{ passwordError }}</p>
</template>

<script>
export default {
	data() {
		return {
			email: '',
			password: '',
			jobOptions: [
				{ text: 'Один', value: 'Один' },
				{ text: 'Два', value: 'Два' },
				{ text: 'Три', value: 'Три' }
			],
			selected: '',
			terms: false,
			names: [],
			tempSkill: '',
			skills: [],
			passwordError: ''
		}
	},
	created() {
		this.selected = this.jobOptions[0].value;
	},
	methods: {
		addSkill(e) {
			if (e.key === ',' && this.tempSkill) {
				if (!this.skills.includes(this.tempSkill)) {
					this.skills.push(this.tempSkill.slice(0, -1));
				}
				this.tempSkill = '';
			}
		},
		deleteSkill(skill) {
			this.skills = this.skills.filter((item) => {
				return skill !== item;
			});
		},
		handleSubmit() {
			this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long.';

			if (!this.passwordError) {
        console.log('email: ', this.email)
        console.log('password: ', this.password)
        console.log('role: ', this.selected)
        console.log('skills: ', this.skills)
        console.log('terms accepted: ', this.terms)
			}
		}
	}
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }
	.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }
	button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
  }
  .submit {
    text-align: center;
  }
  .error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  }
</style>