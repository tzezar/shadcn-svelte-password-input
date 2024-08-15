<script lang="ts">
	import type { HTMLInputAttributes } from 'svelte/elements';
	import type { InputEvents } from './index.js';
	import { cn } from '$lib/utils.js';

	type $$Props = HTMLInputAttributes;
	type $$Events = InputEvents;

	let className: $$Props['class'] = undefined;
	export let value: $$Props['value'] = undefined;
	export { className as class };

	// Workaround for https://github.com/sveltejs/svelte/issues/9305
	// Fixed in Svelte 5, but not backported to 4.x.
	export let readonly: $$Props['readonly'] = undefined;

	let showPassword = false;
	function togglePasswordVisibility() {
		showPassword = !showPassword;
	}
</script>

<div class="relative flex items-center">
	<input
		class={cn(
			'flex h-9 w-full rounded-md border border-input bg-transparent px-3 py-1 text-sm shadow-sm transition-colors file:border-0 file:bg-transparent file:text-sm file:font-medium placeholder:text-muted-foreground focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:cursor-not-allowed disabled:opacity-50',
			className
		)}
		on:input={(e) => (value = e.currentTarget.value)}
		{value}
		{readonly}
		on:blur
		on:change
		on:click
		on:focus
		on:focusin
		on:focusout
		on:keydown
		on:keypress
		on:keyup
		on:mouseover
		on:mouseenter
		on:mouseleave
		on:mousemove
		on:paste
		on:input
		on:wheel|passive
		{...$$restProps}
		type={showPassword ? 'text' : 'password'}
		placeholder="Enter your password"
	/>
	<button
		class="absolute right-2 cursor-pointer text-foreground hover:text-foreground/65"
		on:click={togglePasswordVisibility}
	>
		{#if showPassword}
			<svg
				xmlns="http://www.w3.org/2000/svg"
				width="1.3em"
				height="1.3em"
				viewBox="0 0 15 15"
				{...$$props}
				><path
					fill="currentColor"
					fill-rule="evenodd"
					d="M7.5 11c-2.697 0-4.97-1.378-6.404-3.5C2.53 5.378 4.803 4 7.5 4s4.97 1.378 6.404 3.5C12.47 9.622 10.197 11 7.5 11m0-8C4.308 3 1.656 4.706.076 7.235a.5.5 0 0 0 0 .53C1.656 10.294 4.308 12 7.5 12s5.844-1.706 7.424-4.235a.5.5 0 0 0 0-.53C13.344 4.706 10.692 3 7.5 3m0 6.5a2 2 0 1 0 0-4a2 2 0 0 0 0 4"
					clip-rule="evenodd"
				/></svg
			>
		{:else}
			<svg
				xmlns="http://www.w3.org/2000/svg"
				width="1.3em"
				height="1.3em"
				viewBox="0 0 15 15"
				{...$$props}
				><path
					fill="currentColor"
					fill-rule="evenodd"
					d="M13.354 2.354a.5.5 0 0 0-.708-.708L10.683 3.61A8.5 8.5 0 0 0 7.5 3C4.308 3 1.656 4.706.076 7.235a.5.5 0 0 0 0 .53c.827 1.323 1.947 2.421 3.285 3.167l-1.715 1.714a.5.5 0 0 0 .708.708l1.963-1.964c.976.393 2.045.61 3.183.61c3.192 0 5.844-1.706 7.424-4.235a.5.5 0 0 0 0-.53c-.827-1.323-1.947-2.421-3.285-3.167zm-3.45 2.035A7.5 7.5 0 0 0 7.5 4C4.803 4 2.53 5.378 1.096 7.5c.777 1.15 1.8 2.081 3.004 2.693zM5.096 10.61L10.9 4.807c1.204.612 2.227 1.543 3.004 2.693C12.47 9.622 10.197 11 7.5 11a7.5 7.5 0 0 1-2.404-.389"
					clip-rule="evenodd"
				/></svg
			>
		{/if}
	</button>
</div>
