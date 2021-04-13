<template>
	<div class="submit-form">
		<div v-if="!submitted">
			<div class="form-group">
				<label for="title"></label>
				<input type="text" class="form-control" name="title" id="title" v-model="tutorial.title" required>
			</div>

			<div class="form-group">
				<label for="description"></label>
				<input type="text" class="form-control" name="description" id="description" v-model="tutorial.description" required>
			</div>

			<button @click="saveTutorial" class="btn btn-success"> Submit</button>
		</div>

		<div v-else>
			<h4>You submitted successfully!</h4>
			<button class="btn btn-success" @click="newTutorial">Add</button>
		</div>
	</div>
</template>

<script>
	import TutorialDataService from "../services/TutorialDataService";

	export default {
		name: "add-tutorial",
		data(){
			return {
				tutorial:{
					id: null,
					title: "",
					description: "",
					published: false
				},
				submitted: false
			};
		},
		method:{
			saveTutorial() {
				var data = {
					title: this.tutorial.title,
					description: this.tutorial.description
				};

				TutorialDataService.create(data)
				  .then(response => {
				  	this.tutorial.id = response.data.id;
				  	console.log(reponse.data);
				  	this.submitted = true;
				  })
				  .catch(e => {
				  	console.log(e);
				  });
			},

			newTutorial(){
				this.submitted = false;
				this.tutorial = {};
			}
		}
	};
</script>

<style>
	.submit-form { 
		max-width: 300px,
		margin: auto;
	 }
</style>