<script>
	import { onMount, createEventDispatcher } from 'svelte';

  export let clientId = '';
	export let buttonText = 'Login with Instagram';
	export let scope = 'basic';
	export let implicitAuth = false;
	export let customRender = false;
  export let redirectUrl = ''
  export let style = '';
  export let ref = null;

  const dispatch = createEventDispatcher();

	const getQuery = (value) => {
		var pairs = location.search.slice(1).split('&');
    
    var result = {};
    pairs.forEach(function(pair) {
        pair = pair.split('=');
        result[pair[0]] = decodeURIComponent(pair[1] || '');
    });
    return JSON.parse(JSON.stringify(result))[value];
	}

	onMount(() => {
    if (implicitAuth) {
      const matches = window.location.hash.match(/=(.*)/)
      if (matches) {
        dispatch('success', { data: matches[1] });
      }
    } else if (window.location.search.includes('code')) {
      dispatch('success', { data: getQuery('code') })
    } else if (window.location.search.includes('error')) {
      dispatch('failure', { 
        error: getQuery('error'),
        errorReason: getQuery('error_reason'),
        errorDescription: getQuery('error_description')
      });
    }
	})

	const handleClick = () => {
    const responseType = implicitAuth ? 'token' : 'code';
    const callbackUrl = redirectUrl || window.location.href;
    window.location.href = `https://api.instagram.com/oauth/authorize/?app_id=${clientId}&redirect_uri=${callbackUrl}&scope=${scope}&response_type=${responseType}`;
	}
</script>
{#if customRender}
	<span on:click={handleClick} bind:this={ref}>
		<slot />
	</span>
{:else}
  <span on:click={handleClick} bind:this={ref}>
    <button style={`
      ${style}
      display: inline-block;
      background: linear-gradient(#6559ca, #bc318f 30%, #e33f5f 50%, #f77638 70%, #fec66d 100%);
      color: #fff;
      width: 200px;
      padding-top: 10px;
      padding-bottom: 10px;
      border-radius: 2px;
      border: 1px solid transparent;
      font-size: 16px;
      font-weight: bold;
    `} type="button">{buttonText}</button>
  </span>
{/if}