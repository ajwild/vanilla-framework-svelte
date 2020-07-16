<script>
  import "vanilla-framework/scss/standalone/patterns_contextual-menu.scss";

  export let active = false;
  let node;

  function dispatch(detail) {
    // Use CustomEvent to bubble event to top level of component
    node.dispatchEvent(new CustomEvent("trigger", { bubbles: true, detail }));
  }

  function windowMenuTrigger() {
    dispatch(false);
  }

  function handleClick(event) {
    dispatch(!active);

    window.removeEventListener("click", windowMenuTrigger);
    if (!active) {
      window.addEventListener("click", windowMenuTrigger, { once: true });
    }
  }
</script>

<button
  class="p-button--positive p-contextual-menu__toggle has-icon"
  aria-expanded={active}
  aria-haspopup="true"
  on:click|stopPropagation={handleClick}
  bind:this={node}>
  <slot>
    <span>Menu</span>
    <i class="p-icon--contextual-menu is-light p-contextual-menu__indicator" />
  </slot>
</button>
