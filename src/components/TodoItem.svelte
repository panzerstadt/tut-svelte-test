<script>
  import { onMount } from "svelte";
  import axios from "axios";

  import config from "../config";

  let todo = "";
  $: todos = [];

  onMount(getTodos());
  function getTodos() {
    axios
      .get(
        `https://api.cosmicjs.com/v1/${config.bucket.slug}/object-type/todos?sort=created_at`
      )
      .then(response => {
        console.log(response);
        todos = response.data.objects;
      })
      .catch(e => {
        console.error(e);
      });
  }

  let frameworks = [
    { id: 1, name: "Svelte" },
    { id: 2, name: "Angular" },
    { id: 3, name: "React" },
    { id: 4, name: "Vue" }
  ];
</script>

<style>
  h1 {
    color: black;
    font-size: 20px;
  }
  ul {
    list-style-type: none;
    padding-left: 0;
  }
</style>

<h1>Personal Todo List</h1>
<ul>
  {#each frameworks as { id, name }}
    <li>{id} : {name}</li>
  {/each}
</ul>
