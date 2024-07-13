<script>
	import { auth } from '../../firebase';
	import { createUserWithEmailAndPassword } from 'firebase/auth';

	let form = {
		email: '',
		password: ''
	};

	const onChange = (e) => {
		form = { ...form, [e.target.name]: e.target.value };
	};

	const handleRegister = async () => {
		try {
			await createUserWithEmailAndPassword(auth, form.email, form.password);
			window.location.href = '/login';
		} catch (error) {
			alert(error.message);
		}
	};
</script>

<div class="container">
	<div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
		<h1 class="text-3xl font-semibold">Register</h1>
	</div>
	<form on:submit|preventDefault={handleRegister}>
		<div class="mb-4">
			<label>Email</label>
			<input
				class="mt-1 px-4 py-2 border border-gray-300 rounded-md block w-full"
				type="email"
				name="email"
				bind:value={form.email}
				on:input={onChange}
			/>
		</div>
		<div class="mb-4">
			<label>Password</label>
			<input
				class="mt-1 px-4 py-2 border border-gray-300 rounded-md block w-full"
				type="password"
				name="password"
				bind:value={form.password}
				on:input={onChange}
			/>
		</div>
		<button class="button" type="button" on:click={handleRegister}> Register </button>
	</form>
</div>

<svelte:head>
	<title>Register</title>
</svelte:head>

<style>
	.container {
		max-width: 560px;
		margin: 2rem auto;
	}
	.button {
		background-color: #16a34a;
		color: white;
		border-radius: 0.5rem;
		padding: 0.5rem 1rem;
		width: 100%;
		transition: background-color 0.2s;
	}
	.button:hover {
		background-color: rgba(22, 163, 74, 0.8);
	}
</style>
