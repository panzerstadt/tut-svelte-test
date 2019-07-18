<script>
  import { fade, slide } from "svelte/transition";

  import List from "./components/List.svelte";
  import Login from "./components/Login.svelte";
  import TodoItem from "./components/TodoItem.svelte";
  import Card from "./components/Card.svelte";

  let loggedIn = false;
  let name = "";
  function handleClick(e) {
    loggedIn = e.detail.user.loggedIn;
    name = e.detail.user.name;
  }
</script>

<style>
  h1 {
    color: black;
    font-size: 15px;
    margin: 0;
    margin-right: 20px;
  }

  .main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .login {
    display: flex;
    justify-content: space-between;
    align-items: center;

    padding: 10px 20px;
    width: calc(100% - 40px);
  }
</style>

<div class="main">
  <div class="login">

    <h1>
      {#if loggedIn}
        <span in:fade>Hello {name}!</span>
      {:else}
        <span in:fade>Login to view your personal progress</span>
      {/if}
    </h1>

    <Login on:click={handleClick} />
  </div>

  <Card>
    <List {name} />
  </Card>

  {#if loggedIn}
    <Card>
      <TodoItem />
    </Card>
  {/if}

</div>
