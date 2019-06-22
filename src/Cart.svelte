<script>
  import Card from "./Card.svelte";
  export let items;

  $: cartTotal = items.reduce((sum, currentItem) => {
    return sum + currentItem.priceTotal;
  }, 0);
</script>

<style>
  .left {
    text-align: left;
  }

  .right {
    text-align: left;
  }

  table {
    background-color: whitesmoke;
    width: 100%;
    border: none;
    margin: 0;
    border-collapse: collapse;
  }
  thead {
    background-color: deepskyblue;
    color: white;
    font-weight: bold;
  }
  thead,
  td {
    border-bottom: 1px solid #ddd;
    padding: 0.5rem;
    text-align: right;
  }
  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
</style>

{#if items.length === 0}
  <p>No items found in cart. Go on, add some!</p>
{:else}
  <table>
    <col width="40%" />
    <col width="20%" />
    <col width="20%" />
    <col width="20%" />
    <thead>
      <td class="left">Name</td>
      <td>Price per unit</td>
      <td>Quantity</td>
      <td>Price total</td>
    </thead>
    {#each items as item}
      <tr>
        <td class="left">{item.title}</td>
        <td>${item.price.toFixed(2)}</td>
        <td>{item.quantity}</td>
        <td>${item.priceTotal.toFixed(2)}</td>
      </tr>
    {/each}
  </table>
  <h3 class="right">Total: ${cartTotal}</h3>
{/if}
