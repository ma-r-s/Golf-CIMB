<script>
	import LoadScreen from './LoadScreen.svelte';
	import Main from './main/Main.svelte';
	let loading = true;
	let commandList = ['roslaunch rosbridge_server rosbridge_websocket.launch', ''];
</script>

{#if loading}
	<LoadScreen {commandList} bind:loading />
{:else}
	<Main />
{/if}
