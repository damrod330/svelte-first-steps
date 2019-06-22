<script>
  import Product from "./Product.svelte";
  import Cart from "./Cart.svelte";
  import Button from "./Button.svelte";
  import Card from "./Card.svelte";

  let idCounter = 1000,
    title = "",
    price = 0,
    description = "",
    products = [],
    cartItems = [];

  function createProduct() {
    let newProduct = {
      id: idCounter++,
      title: title,
      price: price,
      description: description,
      date: new Date()
    };

    products = products.concat(newProduct).sort(function(a, b) {
      return b.date - a.date;
    });
  }

  function addToCart(e) {
    let currentItem = cartItems.find(item => item.id === e.detail.id);
    console.log(currentItem);
    if (!currentItem) {
      let newItem = {
        id: e.detail.id,
        title: e.detail.title,
        price: e.detail.price,
        quantity: 1,
        priceTotal: e.detail.price
      };
      cartItems = cartItems.concat(newItem).sort(function(a, b) {
        return b.priceTotal - a.priceTotal;
      });
    } else {
      currentItem.quantity++;
      currentItem.priceTotal = currentItem.price * currentItem.quantity;
      cartItems = cartItems.sort(function(a, b) {
        return b.priceTotal - a.priceTotal;
      });
    }
  }
</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
  }

  .container section {
    width: 100%;
  }

  label,
  input,
  textarea {
    width: 100%;
  }

  input,
  textarea {
    border: none;
    border-bottom: 1px dashed grey;
    background-color: whitesmoke;
    border-radius: 4px;
  }

  input:focus,
  textarea:focus {
    border: none;
    outline: none;
    border: 1px solid orangered;
  }
</style>

<div class="container">
  <section>
    <Card>
      <Cart items={cartItems} />
    </Card>
    <Card>

      <div>
        <label for="title">Title</label>
        <input type="text" id="title" bind:value={title} />
      </div>
      <div>
        <label for="price">Price</label>
        <input type="number" id="price" bind:value={price} />
      </div>
      <div>
        <label for="description">Description</label>
        <textarea id="description" bind:value={description} />
      </div>
      <Button className="secondary large" on:click={createProduct}>
        Create Product
      </Button>
    </Card>
  </section>
  <section>
    {#if products.length === 0}
      <p>No products were found</p>
    {:else}
      {#each products as product}
        <Product {product} on:addcart={addToCart} />
      {/each}
    {/if}
  </section>
</div>
