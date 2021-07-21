<script>
	import InstagramLogin from '../../src/index.svelte';

	const handleSuccess = ({ detail: { data }}) => {
		console.log(data); // code or token
	}

	const handleFailure = ({ detail: { error, errorReason, errorDescription }}) => {
		// error code
	}
</script>

<!-- custom -->
<InstagramLogin 
	clientId="your_client_id" 
	redirectUrl="your_redirect_url" 
	on:success={handleSuccess}
	on:failure={handleFailure}
	customRender>
	<button>Custom instagram button</button>
</InstagramLogin>

<!-- no custom -->
<InstagramLogin 
	clientId="your_client_id" 
	redirectUrl="your_redirect_url" 
	on:success={handleSuccess}
	on:failure={handleFailure} />