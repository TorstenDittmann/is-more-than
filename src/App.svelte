<script>
  import { fade } from "svelte/transition";
  import db from "./db";

  let value;
  let searchElement;

  $: current = db.reduce((acc, cur) => {
    return value <= acc.amount && cur.amount < acc.amount ? cur : acc;
  });
</script>

<style lang="scss">
  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;

    .search {
      border: none;
      width: 100%;
      text-align: center;
      font-size: 7.5vw;
      outline: none;

      &::-webkit-outer-spin-button,
      &::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
      }

      &[type="number"] {
        -moz-appearance: textfield;
      }
    }

    h1 {
      color: #ff3e00;
      text-transform: uppercase;
      font-size: 4em;
      font-weight: 100;
    }
  }
</style>

<main>
  <input
    type="number"
    class="search"
    min="1"
    placeholder="input a number here"
    bind:value
    bind:this={searchElement} />
  {#if value}
    <section transition:fade>
      <h1>is more than {current.amount}</h1>
      <h2>{current.text}</h2>
      {#if current.link}
        <a href={current.link}>{current.link}</a>
      {/if}
    </section>
  {/if}
</main>
