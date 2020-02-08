<script>
  import { createForm } from 'svelte-forms-lib';
  import { object, string } from 'yup';
  import { createEventDispatcher } from 'svelte';
  import { Field, Input, Button } from 'svelte-chota';

  const dispatch = createEventDispatcher();

  const { form, errors, handleChange, handleSubmit } = createForm({
    initialValues: {
      login: '',
      password: '',
    },
    validationSchema: object().shape({
      login: string().required(),
      password: string().required(),
    }),
    onSubmit: values => {
      console.log(JSON.stringify(values));
    },
  });
</script>

<div>
  <h1>SignIn</h1>

  <form on:submit={handleSubmit}>
    <Field label="Username" error={$errors.login || null}>
      <Input
        name="login"
        on:change={handleChange}
        on:blur={handleChange}
        bind:value={$form.login}
        placeholder="Enter login" />
    </Field>
    <Field label="Password" error={$errors.password || null}>
      <Input
        password
        name="password"
        on:change={handleChange}
        on:blur={handleChange}
        bind:value={$form.password}
        placeholder="Enter password" />

    </Field>
    <button type="submit">submit</button>
  </form>
  Have no account?
    <Button clear on:click={() => dispatch('switchPage', 'signUp')}>
      SignUp
    </Button>
</div>
