<script>
  import PersonList from "../components/PersonList.svelte";
  import { ApolloClient, InMemoryCache } from "@apollo/client";
  import { setClient, getClient, query } from "svelte-apollo";
  const client = new ApolloClient({
    uri: "http://localhost:3000",
    cache: new InMemoryCache(),
  });
  setClient(client);
</script>

<PersonList />
