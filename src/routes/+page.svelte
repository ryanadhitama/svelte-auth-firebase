<script>
	import { writable } from 'svelte/store';
	import { auth } from '../firebase';
	import { onMount } from 'svelte';

	const user = writable(null);

	const handleLogout = () => {
		auth.signOut();
	};

	onMount(() => {
		const unsubscribe = auth.onAuthStateChanged((authUser) => {
			if (authUser) {
				user.set(authUser);
			} else {
				user.set(null);
			}
		});

		return () => unsubscribe();
	});
</script>

<div class="container mx-auto mt-8 max-w-[560px]">
	<div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
		<h1 class="text-3xl font-semibold">Private Page</h1>
	</div>
	{#if $user}
		<div>
			<p>Hi, {$user.email}</p>
			<button
				class="mt-4 bg-red-600 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200 w-full"
				type="button"
				on:click={handleLogout}
			>
				Logout
			</button>
		</div>
	{:else}
		<div>
			<button
				class="mt-4 bg-blue-600 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200 w-full"
				type="button"
				on:click={() => (window.location.href = '/login')}
			>
				Login
			</button>
			<button
				class="mt-4 bg-red-600 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200 w-full"
				type="button"
				on:click={() => (window.location.href = '/register')}
			>
				Register
			</button>
		</div>
	{/if}
</div>

<svelte:head>
	<title>Home Page</title>
</svelte:head>

<style>
	.container {
		max-width: 560px;
		margin: 2rem auto;
	}
</style>
