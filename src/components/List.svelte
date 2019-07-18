<script>
  let frameworks = [
    { id: 1, name: "Svelte" },
    { id: 2, name: "Angular" },
    { id: 3, name: "React" },
    { id: 4, name: "Vue" }
  ];

  export let name;
</script>

<style>
  h1 {
    color: black;
    font-size: 20px;
    margin: 0;
  }
  ul {
    list-style-type: none;
    padding-left: 0;
  }

  li {
    font-size: 16px;
  }
</style>

<h1>List of Frameworks to learn</h1>
<ul>
  {#each frameworks as { id, name }}
    <li>{id} : {name}</li>
  {/each}
</ul>
