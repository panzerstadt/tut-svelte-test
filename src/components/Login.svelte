<script>
  import { createEventDispatcher } from "svelte";

  let user = { loggedIn: false, name: "" };
  const dispatch = createEventDispatcher();

  const DUMMY = "panzerstadt";

  function toggle() {
    // ...login logic here
    // get username

    user.loggedIn = !user.loggedIn; // happens first
    if (user.loggedIn) {
      user.name = DUMMY; // assign username if logged in
    } else {
      user.name = "";
    }

    dispatch("click", {
      user // is the fresh state updated two lines ago,
    });
    // no race conditions!
  }
</script>

<style>
  button {
    border: 1px solid black;
    background-color: white;
    border-radius: 15px;
    padding: 5px 10px;

    font-size: 12px;
  }
</style>

{#if user.loggedIn}
  <button on:click={toggle}>Log Out</button>
{:else}
  <button on:click={toggle}>Login</button>
{/if}
