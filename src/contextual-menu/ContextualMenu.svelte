<script>
  import "vanilla-framework/scss/standalone/patterns_contextual-menu.scss";

  let active = false;

  function handleTrigger(event) {
    active = event.detail;
  }
</script>

<span class="p-contextual-menu--left" on:trigger={handleTrigger}>
  <slot {active} />
</span>
