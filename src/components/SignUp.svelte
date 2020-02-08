<script>
  import { createForm } from 'svelte-forms-lib';
  import { object, string } from 'yup';
  import { createEventDispatcher } from 'svelte';
  import { Field, Input, Button, Checkbox } from 'svelte-chota';

  const dispatch = createEventDispatcher();

  const { form, errors, handleChange, handleSubmit } = createForm({
    initialValues: {
      email: '',
      password: '',
      password2: '',
      phone: '',
    },
    validationSchema: object().shape({
      email: string().required(),
      password: string().required(),
      password2: string().required(),
      phone: string().required(),
    }),
    onSubmit: values => {
      console.log(JSON.stringify(values));
    },
  });
  let checkboxValues = [];
</script>

<div>
  <h1>SignUp</h1>
  <form on:submit={handleSubmit}>
    <Field label="Email" error={$errors.email || null}>
      <Input
        name="email"
        on:change={handleChange}
        on:blur={handleChange}
        bind:value={$form.email}
        placeholder="Enter email" />
    </Field>
    <Field label="Phone" error={$errors.phone || null}>
      <Input
        name="phone"
        on:change={handleChange}
        on:blur={handleChange}
        bind:value={$form.phone}
        placeholder="Enter phone number" />
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
    <Field label="Confirm Password" error={$errors.password2 || null}>
      <Input
        password
        name="password2"
        on:change={handleChange}
        on:blur={handleChange}
        bind:value={$form.password2}
        placeholder="Confirm password" />

    </Field>
    <div class="flex align-middle justify-center flex-col">
      <div class="flex items-center">
        <Checkbox value="first" bind:group={checkboxValues} />
        &nbsp;I work for free
      </div>
      <div class="flex items-center">
        <Checkbox value="second" bind:group={checkboxValues} />
        &nbsp;Agree with personal data processing
      </div>
    </div>

    <button type="submit">submit</button>
  </form>
  Have account?
  <Button clear on:click={() => dispatch('switchPage', 'signIn')}>
    SignIn
  </Button>
</div>
