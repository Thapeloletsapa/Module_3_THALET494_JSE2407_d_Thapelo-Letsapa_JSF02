<script>
  import { onMount } from 'svelte';
  import { navigate } from 'svelte-routing';

  export let params;

  let product;
  let loading = true;
  let error = null;

  const fetchProduct = async () => {
    loading = true;
    error = null;
    try {
      const response = await fetch(`https://fakestoreapi.com/products/${params.id}`);
      if (!response.ok) {
        throw new Error('Failed to fetch product');
      }
      product = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      loading = false;
    }
  };

  onMount(() => {
    fetchProduct();
  });

  const goBack = () => {
    navigate('/');
  };
</script>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p class="text-red-500">{error}</p>
{:else}
  <div class="product-detail">
    <button on:click={goBack}>Back</button>
    <h2>{product.title}</h2>
    <img src={product.image} alt={product.title} />
    <p>{product.description}</p>
    <p>${product.price}</p>
    <p>Category: {product.category}</p>
    <p>Rating: {product.rating.rate} ({product.rating.count} reviews)</p>
  </div>
{/if}

<style>
  .product-detail {
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  img {
    max-width: 100%;
    height: auto;
  }
</style>