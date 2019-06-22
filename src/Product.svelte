<script>
  import { createEventDispatcher } from "svelte";
  import Button from "./Button.svelte"; 
  import Card from "./Card.svelte"; 

  export let product;

    const dispatch = createEventDispatcher();

  function addToCart() {
    dispatch("addcart", product);
  }
</script>

<style>

  h1 {
    font-size: 1.6rem;
    margin: 0.2rem 0;
    font-weight: bold;
  }

  h1 span {
    font-weight: bolder;
    color: orangered;
    float: right;
  }

  h4 {
    font-size: 0.6rem;
    margin: 0.2rem 0;
    font-weight: bolder;
    color: gray;
  }
  p {
    font-size: 1rem;
    margin: 1rem 0;
  }
</style>

<Card>
  <h1>
     {product.title}
    <span>${product.price.toFixed(2)}</span>
  </h1>
  <h4>{product.date.toLocaleString()}</h4>
  <p>{product.description}</p>
  <Button className="primary" on:click={addToCart}>Add to chart</Button>
</Card>
