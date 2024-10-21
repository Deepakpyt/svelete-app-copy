<script lang="ts">
  import { goto } from "$app/navigation";
  import { faWarning, faSpinner } from "@fortawesome/free-solid-svg-icons";
  import debug from "debug";
  import Fa from "svelte-fa";
  import { firebaseAuthAdapter } from "$lib/services/firebaseAuth";

  const log = debug("app:routes:login:page.svelte");

  export let form;

  $: log("form:", form);

  let email = form?.email ?? "";
  let password = "";
  let error = form?.error ?? "";
  let loading = false;

  async function handleLogin() {
    loading = true;

    const result = await firebaseAuthAdapter.login(email, password);
    loading = false;

    if (result.user) {
      goto("/dashboard");
    } else {
      error = result.error || "An unknown error occurred";
    }
  }
</script>

<section style="padding: 3rem;" class="max-w-sm mx-auto">
  <div class="prose">
    <h1
      style={` -webkit-text-fill-color: #0000;
			background: -webkit-linear-gradient(270deg,#d6001c -54.17%,#6d297b);
			background-clip: text;
			-webkit-background-clip: text;`}
    >
      Log In
    </h1>
  </div>
  <form class="flex flex-col gap-6 my-6" on:submit|preventDefault={handleLogin}>
    {#if form?.error || error}
      <div class="alert alert-error">
        <div>
          <Fa icon={faWarning} />
          {form?.error || error}
        </div>
      </div>
    {/if}
    <p>
      <input
        autocomplete="email"
        autocorrect="off"
        type="email"
        name="email"
        placeholder="Email..."
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-red focus:border-red block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-red dark:focus:border-red"
        required
        bind:value={email}
      />
    </p>
    <p>
      <input
        autocomplete="current-password"
        type="password"
        name="password"
        placeholder="Password..."
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-red focus:border-red block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-red dark:focus:border-red"
        required
        bind:value={password}
      />
    </p>
    <p class="buttonlogin flex gap-6 mt-6">
      <button
        class="btn btn-primary flex items-center justify-center"
        style={`background-color: var(--app-primary-color, #d60016);
				border: none;
				color: white;`}
        disabled={loading}
      >
        {#if loading}
          <Fa icon={faSpinner} class="animate-spin" />
          <span class="ml-2">Logging in...</span>
        {:else}
          Log In
        {/if}
      </button>
    </p>
  </form>
</section>

<style>
  @media (max-width: 640px) {
    .prose h1 {
      font-size: 1.5rem;
      line-height: 1.2;
    }

    .flex {
      flex-direction: column;
    }
    .btn {
      width: 100%;
    }
  }

  .prose h1 {
    font-size: 2rem;
    text-align: center;
  }

  .btn {
    width: auto;
  }

  .animate-spin {
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
