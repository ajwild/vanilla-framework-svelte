<script>
  // Package import from GitHub
  import {
    ContextualMenu,
    ContextualMenuContent,
    ContextualMenuGroup,
    ContextualMenuItem,
    ContextualMenuTrigger
  } from "vanilla-framework-svelte";

  // Local import when editing
  // import ContextualMenu from "../../src/contextual-menu/ContextualMenu.svelte";
  // import ContextualMenuTrigger from "../../src/contextual-menu/ContextualMenuTrigger.svelte";
  // import ContextualMenuContent from "../../src/contextual-menu/ContextualMenuContent.svelte";
  // import ContextualMenuGroup from "../../src/contextual-menu/ContextualMenuGroup.svelte";
  // import ContextualMenuItem from "../../src/contextual-menu/ContextualMenuItem.svelte";

  let status = null;

  function changeStatus(newStatus) {
    status = newStatus;
  }
</script>

<div>Status: {status}</div>
<ContextualMenu let:active>
  <ContextualMenuTrigger {active} />
  <ContextualMenuContent {active}>
    <ContextualMenuGroup>
      <ContextualMenuItem on:click={() => changeStatus('complete')}>
        Complete
      </ContextualMenuItem>
      <ContextualMenuItem on:click={() => changeStatus('partial')}>
        Partial
      </ContextualMenuItem>
      <ContextualMenuItem on:click={() => changeStatus('not-started')}>
        Not started
      </ContextualMenuItem>
    </ContextualMenuGroup>
    <ContextualMenuGroup>
      <ContextualMenuItem on:click={() => changeStatus(null)}>
        Clear
      </ContextualMenuItem>
    </ContextualMenuGroup>
  </ContextualMenuContent>
</ContextualMenu>
