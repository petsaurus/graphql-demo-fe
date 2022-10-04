<script>
  import { gql } from "@apollo/client";
  import { mutation } from "svelte-apollo";

  let name = "";
  const upsertPerson = mutation(
    gql`
      mutation ($record: PersonInput!) {
        upsertPerson(record: $record) {
          name
          id
        }
      }
    `,
    {
      refetchQueries: "active",
    }
  );

  const upsert = () => {
    upsertPerson({ variables: { record: { name } } });
    name = "";
  };
</script>

<input bind:value={name} placeholder="new contact name" />
<button on:click={upsert}>create new contact</button>
