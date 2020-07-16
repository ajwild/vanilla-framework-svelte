<script>
  import "vanilla-framework/scss/standalone/patterns_contextual-menu.scss";

  export let active = false;
</script>

<span
  class="p-contextual-menu__dropdown"
  aria-hidden={!active}
  aria-label="submenu">
  <slot />
</span>
