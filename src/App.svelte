<script>
	import Modal from "./Modal.svelte";
	import AddPersonForm from "./AddPersonForm.svelte";

	let people = [
		{ name: "yoshi", beltColour: "black", age: 25, id: 1 },
		{ name: "mario", beltColour: "orange", age: 45, id: 2 },
		{ name: "luigi", beltColour: "brown", age: 35, id: 3 },
	];

	const handleClick = (id) => {
		people = people.filter((p) => p.id != id);
	};

	let showModal = false;
	const toggleModal = () => {
		showModal = !showModal;
	};

	const addPerson = (e) => {
		const person = e.detail;
		if (person.name & person.age & person.skills) {
			people = [person, ...people];
			showModal = false;
		}else{
			alert("you must filled the form")
		}
	};
</script>

<Modal {showModal} on:click={toggleModal}>
	<h3>Add a new person</h3>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>

<main>
	<button on:click={toggleModal}>Open Modal</button>
	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltcolour === "black"}
				<p><strong>MASTER NINJA</strong></p>
			{/if}
			<p>{person.age} year old, {person.beltColour}</p>
			<button on:click={() => handleClick(person.id)}>delete</button>
		</div>
	{:else}
		<p>There are no people to show</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
