<script>
	import Modal from './Modal.svelte';
	let firstName = "Vincent";
	let lastName = "Kim";
	
	/*
		To output the result of beltColour right here,
		Delete "color: {beltColor}".
	*/
	let beltColour = "black";
	/* 
	    The Reactive-Value.
	    - 1. Use a template string to concatenate firstName and lastName
		regularly.
		
		- 2. Reactive-Statement is watching whatever values we use
		inside it. In this case, 'beltColour'.
	*/
	$: fullName = `${firstName} ${lastName}`;
	// Run this code-blocks statement everytime.
	$: {
		console.log(beltColour);
		console.log(fullName);
	}
	/*
	  1. Make sure you have to convert file-form
		 as 'png' not 'jpg'.
	  
	  2. You should save your file into public file-directory,
	     not to create a new one in file-directory named 'src'.
	*/
	let imgSrc = "images.png";
	const handleClick_colour = () => {
		beltColour = 'orange';
	};
	
	const handleInput = (e) => {
		// Update on Screen in Real-Time.
		beltColour = e.target.value;
	};
	
	let people = [
		{name: 'Vincent', beltColour: 'black', age: 19, id: 1},
		{name: 'Stuart', beltColour: 'orange', age: 16, id: 2},
		{name: 'Ralph', beltColour: 'brown', age: 18, id: 3}
	];
	/* 
	  Relating to 'filter' function.
	  1. Delete the person from people. 
	  2. Pass data through into this function.
	  3. 'Filter' is just a regular JavaScript method and it
	  filters through the array so we can remove certain items out.
	  4. 'Fliter' take a callback-function right here.
	  5. Takes each person as we cycle through the array,
	  and fires a callback function for each person,
	  and we take person in here, '()'.
	  5. If we return true, then it keeps that person in the array,
	  otherwise if we return false, then it removes that person
	  from the array.
	  6. Check if that is not equal to the ID because if they're not 
	  equal then we want to keep that person in the array.
	*/
	const handleClick = (e, id) => {
		people = people.filter((person) => person.id != id);
		console.log(e);
	};
	
	// But it display 'num' when I change it's value.
	/*
		- 1. If I change this value as '25',
		it just prints out 'Greater than 20'.
		- 2. And if I change this value as '15',
		it prints out 'Greater than 5'.
		- 3. Otherwise if I change this value as '5',
		it prints out 'Not greater than 5'.
	*/
	let num = 5;
</script>

<Modal />
<main>
	<!-- Output full-name here. -->
	<p style="color: {beltColour}">{fullName} - has {beltColour} belt</p>
	<button on:click={handleClick}>Update belt colour</button>

	<!-- Two way bounding, 'handleInput' and 'beltColour'. -->
	<!-- <input type="text" on:input={handleInput} value={beltColour}> -->

	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
	<!-- 
		One way bounding, but it controlls all of things 
		by using 'beltColour'. 
	-->
	<input type="text" bind:value={beltColour}>

	<!-- svelte-ignore a11y-missing-attribute -->
	<img src={imgSrc}>

	<!-- 
		1. Almost like a for-each Loop. 
		2. Applying a unique key to each element inside our array
		and pass that unique key-property to the loop.
		3. (person.id) of '()' is a parentheses.

		Now we didn't access to variable 'person',
		so it cannot delete as you want.
	-->
	{#each people as person (person.id)}
	<div>
		<h4>{person.name}</h4>
		{#if person.beltColour == 'black'}
			<p><strong>Vincent has been appeared!!</strong></p>
		{/if}
		<p>{person.age} years old, {person.beltColour} belt.</p>

		<!-- 
			- 1. Invokes data. 
			- 2. Use the inline-function right here.
			- 3. This is not getting automatically invoked because
			it sits inside a function which is not yet invoked until
			we click on this (button).
			- 4. Display how we can pass through an argument
			to a click handler or any other kind of handler function
			where an event occurs we wrap it inside an inline-function
			which is not automatically invoked when the code runs.

			- 5. Take in the event-object inside of '()' parameter,
			and then pass it in as an argument into this handle
			click-function we could take it here then as a parameter. 
		-->
		<!-- It's up to you inputing event-handle, 'e'. -->
		<button on:click={(e) => 
			// Now we can see the ID.
			handleClick(e, person.id)
		}>delete</button>
	</div>
	<!-- 
		1. Adding inside each-block another keyword and
		it's going to be colon else inside here.
		2. Comment out all of list-contents in variable 'people' and
		save it, then you can see, 'There are no people to show.'.
	-->
	{:else}
	<p>There are no people to show...</p>
	{/each}
</main>

{#if num > 20}
	<p>Greater than 20</p>
{:else if num > 5}
	<p>Greater than 5</p>
{:else}
	<p>Not greater than 5</p> 
{/if}