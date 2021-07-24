# svelte-instagram-login

An Instagram Sign-in / Log-in Svelte

## Api guide

- [instagram api guide](https://developers.facebook.com/docs/instagram-api/)

## Install
```
  npm install -save svelte-instagram-login
```

## How to use
```js
    <script>
      import InstagramLogin from 'svelte-instagram-login';

      const handleSuccess = ({ detail: { data }}) => {
        console.log(data); // code or token
      }

      const handleFailure = ({ detail: { error, errorReason, errorDescription }}) => {
        // error code
      }
    </script>

    // custom
    <InstagramLogin 
      clientId="your_client_id" 
      redirectUrl="your_redirect_url" 
      on:success={handleSuccess}
      on:failure={handleFailure}
      customRender>
      <button>Custom instagram button</button>
    </InstagramLogin>

    // no custom
    <InstagramLogin 
      clientId="your_client_id" 
      redirectUrl="your_redirect_url" 
      on:success={handleSuccess}
      on:failure={handleFailure} />
```
## Events & value

- `clientId` (required) [string]
- `scope` (optional) [string] - default: `basic`
- `implicitAuth` (optional) [boolean] - default: `false`
- `customRender` (optional) [boolean] - default: `false`
- `redirectUrl` (optional) [boolean] - default: `window.location.href`
- `style` (optional) [string] - default: `style="border: 1px solid #ffffff"`
- `ref` (optional) [htmlelement] - default: null
- `on:success` [func]
- `on:failure` [func]

## License

MIT