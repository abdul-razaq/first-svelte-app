<script>
	import ContactCard from './ContactCard.svelte';

	let name = 'Nivans';
	let age = 25;
	let jobTitle = "Web Developer";
	let description;
	let userImage;
	let formState = 'empty';

	let createdContacts = [];

	$: upperCaseName = name.toUpperCase();
	// whenever name changes, this if statement re-runs. It watches for name
	$: if (name === 'AbdulRazaq') {
		alert('Aha! Here you are AbdulRazaq');
	}

	function changeAge() {
		if (age === 40) alert('you are now an adult!');
		age += 1;
	}

	function changeName() {
		const names = ['Aisha', 'Habib', 'Muhammad', 'AbdulRazaq', 'Ishaaq', 'Muthmoinah', 'AbdulMalik', 'Ganiyat'];
		name = names[Math.floor(Math.random() * names.length)];
	}

	function nameInput(event) {
		name = event.target.value;
	}

	function displayContactCard() {
		if (name.trim().length === 0 || jobTitle.trim().length === 0 || description.trim().length === 0 || userImage.trim().length === 0) {
			formState = 'invalid';
			return;
		}
		formState = 'done';
		createdContacts = [
			...createdContacts,
			{
				id: Math.random(),
				name,
				jobTitle,
				description,
				userImage,
			}
		]
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {upperCaseName}! my age is {age}.</h1>
<button on:click="{changeAge}">Change Age</button>
<button on:click="{changeName}">Change Name</button>
<!-- <input type="text" value="{name}" on:input="{nameInput}" /> -->
<input type="text" bind:value="{name}"/>
<input type="text" bind:value="{jobTitle}"/>
<input type="text" bind:value="{userImage}"/>
<textarea name="description" id="" cols="40" rows="5" bind:value="{description}"></textarea>
<button on:click="{displayContactCard}">Display Contact Card</button>

{#if formState === 'invalid'}
<p>Invalid input.</p>
{:else}
<p>Please provide some data and hit the button!</p>
{/if}

{#each createdContacts as contact, index (contact.id)}
	<h1># {index + 1}</h1>
	<ContactCard userName="{contact.name}" jobTitle="{contact.jobTitle}" description={contact.description} userImage="{contact.userImage}"/>
{:else}
	<p>Please start adding some contacts, we found none.</p>
{/each}
