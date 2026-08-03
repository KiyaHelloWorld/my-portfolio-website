<script setup>
	import {ref} from "vue";
	import {Notyf} from "notyf";

	const notyf = new Notyf();

	const name = ref("");
	const email = ref("");
	const message = ref("");

	const isLoading = ref(false);

	const WEB3FORMS_ACCESS_KEY = "bb791158-1242-419a-8732-8ba382ad48d7";
	const subject = "A User Sent a message from your WebPortfolio";

	const submitForm = async () => {
		try{
			const response = await fetch("https://api.web3forms.com/submit", {
				method: "POST",
				headers: {
					"Content-Type" : "application/json",
					Accept: "application/json"
				},
				body: {
					access_key: WEB3FORMS_ACCESS_KEY,
					subject: subject,
					name: name.value,
					email: email.value,
					message: message.value
				}
			})

			const result = await response.json();

			if(result.success){
				isLoading.value = false
				notyf.success("Message Sent! ")
			}
		}
		catch(error){
			console.log(error);
			isLoading.value = false;
			notyf.error("Failed to send message");
		}
	}
</script>

<template>
<body class="space-grotesk">
	<div class="container" style="max-width: 560px;">
		<div class="py-5">
			<h1 class="mb-2">Get in touch</h1>
			<p class="text-muted mb-4">Have a project in mind or a role to fill? Send a message and I'll reply within a day or two.</p>

			<form action="https://api.web3forms.com/submit" method="POST">
	            	<input type="hidden" name="access_key" value="4e0dba34-036a-4c1a-847d-2a3245797145">
				<div class="mb-3">
					<label for="name" class="form-label">Name</label>
					<input type="text" class="form-control" id="name" name="name" placeholder="Jane Doe" required>
				</div>

				<div class="mb-3">
					<label for="email" class="form-label">Email</label>
					<input type="email" class="form-control" id="email" name="email" placeholder="JaneDoe@gmail.com" required>
				</div>

				<div class="mb-4">
					<label for="message" class="form-label">Message</label>
					<textarea class="form-control" id="message" name="message" rows="5" placeholder="What are you building, and what do you need help with?" name = "messsage" required></textarea>
				</div>

				<button type="submit" class="btn btn-primary">Send message</button>
			</form>
		</div>
	</div>
</body>
</template>