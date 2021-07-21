<script>
	import InstagramLogin from '../../src/index.svelte';

	const handleSuccess = () => {

	}
</script>

<InstagramLogin 
	clientId="your_client_id" 
	redirectUrl="your_redirect_url" 
	on:success={handleSuccess}
	customRender>
	<button>Custom instagram button</button>
</InstagramLogin>

<InstagramLogin />