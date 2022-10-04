<script>
  import { gql } from "@apollo/client";
  import { query } from "svelte-apollo";
  import NewPerson from "./NewPerson.svelte";

  const data = query(gql`
    {
      persons {
        companyId
        id
        name
        city
        company {
          name
        }
      }
    }
  `);
</script>

<NewPerson />

{#if $data.loading}
  Loading...
{:else if $data.error}
  Error: {$data.error.message}
{:else}
  <div class="container">
    <b>Name</b>
    <b>Office</b>
    <b>City</b>
    {#each $data.data.persons as person}
      <span>{person.name}</span>
      <span>{person.company?.name || ""}</span>
      <span>{person.city || ""}</span>
    {/each}
  </div>
{/if}

<style>
  .container {
    background-color: #baeba9;
    display: grid;
    grid-template-columns: auto auto auto;
    column-gap: 0.1rem;
    row-gap: 0.1rem;
    padding: 0.1rem;
    margin-top: 2rem;
  }
  .container span {
    background-color: #c6ffb1;
    padding: 0.3rem;
  }
</style>
