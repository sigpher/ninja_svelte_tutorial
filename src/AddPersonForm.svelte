<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    let name;
    let beltColour;
    let age;
    let skills = [];

    const handleSubmit = () => {
        const person = {
            name,
            beltColour,
            age,
            skills,
            id: Math.random(),
        };
        dispatch("addPerson", person);
    };
</script>
<form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="name" bind:value={name} /><br />
    <input type="number" placeholder="age" bind:value={age} /><br />
    
    <label>Skills:</label>
    <input type="checkbox" bind:group={skills} value="fighting" /> fighting
    <input type="checkbox" bind:group={skills} value="sneaking" /> sneaking
    <input type="checkbox" bind:group={skills} value="running" /> running
    <br />

    <label>Belt colour:</label>
    <select name="" id="" bind:value={beltColour}>
        <option value="black">black</option>
        <option value="orange">orange</option>
        <option value="brown">brown</option>
        <option value="white">white</option>
    </select>
    <br />
    <button>Add Person</button>
</form>

<style></style>
