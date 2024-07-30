<script>
    import { onMount } from 'svelte';
    import ProductCard from './ProductCard.svelte';
  
    let products = [];
    let loading = true;
    let error = null;
  
    const fetchProducts = async () => {
      loading = true;
      error = null;
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        if (!response.ok) {
          throw new Error('Failed to fetch products');
        }
        products = await response.json();
      } catch (err) {
        error = err.message;
      } finally {
        loading = false;
      }
    };
  
    onMount(() => {
      fetchProducts();
    });
  </script>
  
  <div>
    {#if loading}
      <p>Loading...</p>
    {:else if error}
      <p class="text-red-500">{error}</p>
    {:else if products.length === 0}
      <p>No products available.</p>
    {:else}
      <div class="grid-container">
        {#each products as product (product.id)}
          <ProductCard {product} />
        {/each}
      </div>
    {/if}
  </div>
  
  <style>
    div {
      margin-top: 1rem;
    }
  
    .grid-container {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      gap: 1rem;
    }</style>
