<script>
	import { browser } from '$app/env';
	import Efebia from '$lib/components/Efebia.svelte';
</script>

{#if browser}
	<Efebia />
{/if}
<slot />
