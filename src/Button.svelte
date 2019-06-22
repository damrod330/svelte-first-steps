<script>
  export let className = "primary";
</script>

<style>
  .primary {
    border: 2px solid orangered;
    background: orangered;
    color: white;
  }

  .primary:hover {
    background: red;
    border: 2px dashed orange;
    color: white;
  }

  .secondary {
    border: 2px dashed deepskyblue;
    background: deepskyblue;
    color: white;
  }

  .secondary:hover {
    background: #108cd4;
    border: 2px dashed #2bb1ff;
    color: white;
  }

  .small {
    padding: 0.3rem 0.9rem;
    font-size: 0.8rem;
  }

  .large {
    padding: 0.6rem 1.4rem;
    font-size: 1.3rem;
  }

  button {
    text-transform: uppercase;
    padding: 0.4rem 1.2rem;
    font-size: 1rem;
    font-weight: 400;
    font-style: inherit;
    margin: 0.2rem;
    cursor: pointer;
  }
</style>

<button on:click on:keypress class={className}>
  <slot />
</button>
