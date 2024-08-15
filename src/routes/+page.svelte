<script lang="ts">
	import PasswordInput from '$lib/components/ui/password-input/password-input.svelte';
	import { mode } from 'mode-watcher';
	import logoBlack from '$lib/assets/tzezar-logo-black.png';
	import logoWhite from '$lib/assets/tzezar-logo-white.png';

	import Highlight from 'svelte-highlight';
	import typescript from 'svelte-highlight/languages/typescript';
	import atomOneDark from 'svelte-highlight/styles/atom-one-dark';
	import Button from '$lib/components/ui/button/button.svelte';

	let value = '';

	let codeHighlight = `<script>
    import PasswordInput from '$lib/components/ui/password-input/password-input.svelte';
    let value = '';
<\/script>

<PasswordInput name="pswd" bind:value />`;

	function handleSubmit(event: SubmitEvent) {
		event.preventDefault(); // Prevent the form from submitting
		const formData = new FormData(event.target as HTMLFormElement); // Get form data
		// Convert form data to an object for easy logging
		const data: { [key: string]: any } = {};
		formData.forEach((value, key) => {
			data[key] = value;
		});

		alert(`Your super secret password is: ${data.pswd}`); // Log the form data as an object
	}
</script>

<svelte:head>
	{@html atomOneDark}
</svelte:head>

<div class="flex flex-col gap-4">
	<div class="flex flex-row gap-4">
		{#if $mode == 'dark'}
			<img src={logoWhite} alt="" srcset="" class="h-[64px]" />
		{:else}
			<img src={logoBlack} alt="" srcset="" class="h-[64px]" />
		{/if}
		<h1 class="scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl">
			shadcn-svelte password-input
		</h1>
	</div>
	<h2
		class="mt-10 scroll-m-20 border-b pb-2 text-3xl font-semibold tracking-tight transition-colors first:mt-0"
	>
		Showcase
	</h2>
	<div class="flex w-fit p-4">
		<form on:submit={handleSubmit} class='flex flex-row gap-4'>
			<PasswordInput name="pswd" bind:value />
			<Button type="submit">Submit</Button>
		</form>
	</div>

	

	<div class="flex flex-col gap-4">
		<h2
			class="mt-10 scroll-m-20 border-b pb-2 text-3xl font-semibold tracking-tight transition-colors first:mt-0"
		>
			Usage
		</h2>

		<p>
			1. Copy component from <a
				class="font-medium text-primary underline underline-offset-4"
				href="https://github.com/tzezar/shadcn-svelte-password-input/tree/main/src/lib/components/ui/password-input"
				>GITHUB REPOSITORY</a
			> and paste it into your components folder.
		</p>
		<p>2. Use the component in your Svelte file as shown below:</p>
		<Highlight language={typescript} code={codeHighlight} />
	</div>

	<p class="pb-6 italic">
		If you find the project interesting feel free to give a star on <a
			class="font-medium text-primary underline underline-offset-4"
			href="https://github.com/tzezar/shadcn-svelte-transfer-list">github</a
		>. Thanks! ❤️
	</p>
</div>
