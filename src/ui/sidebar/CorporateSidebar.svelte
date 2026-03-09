<script>

import Sidebar from "../../lib/components/layout/Sidebar.svelte";

</script>

<div class="corporate-sidebar">

  <Sidebar />

</div>

<style>

.corporate-sidebar {

  background: var(--color-sidebar-background);
  color: var(--color-sidebar-foreground);

  height: 100%;
  display: flex;
  flex-direction: column;

}

</style>