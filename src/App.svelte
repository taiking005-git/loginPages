<script>
  import LoginPage from "./Components/LoginPage.svelte";
  import SingupPage from "./Components/SingupPage.svelte";
  import { Router, Route } from "svelte-routing";

  export let url = "";
</script>

<Router {url}>
  <main class="container">
    <Route path="/" component={LoginPage} />
    <Route path="signup" component={SingupPage} />
  </main>
</Router>
