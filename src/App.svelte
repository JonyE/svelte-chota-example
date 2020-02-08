<script>
  import 'chota';
  import SignIn from './components/SignIn.svelte';
  import SignUp from './components/SignUp.svelte';

  let page = 'signIn';

  const callbackFunction = event => {
    page = event.detail;
  };

  $: Container = page === 'signIn' ? SignIn : SignUp;
</script>

<style>
  .container{
    width: 100%;
    height: 100%;
  }
</style>

<div class="container">
  <svelte:component this={Container} on:switchPage={callbackFunction} />
</div>

