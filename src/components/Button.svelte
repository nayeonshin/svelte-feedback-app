<script>
  export let style = "primary";
  export let type = "button";
  export let disabled = false;
</script>

<button {type} {disabled} class={style}>
  <slot />
</button>

<style>
  button {
    color: #fff;
    cursor: pointer;
    border: 0;
    border-radius: 8px;
    height: 40px;
    width: 100px;
  }

  .primary {
    background-color: #202142;
  }

  .secondary {
    background: #ff6a95;
  }

  button:hover {
    opacity: 0.9;
    transform: scale(0.98);
  }

  button:disabled {
    background-color: #cccccc;
    color: #333;
    cursor: auto;
  }

  button:disabled:hover {
    opacity: 1;
    transform: scale(1);
  }
</style>
