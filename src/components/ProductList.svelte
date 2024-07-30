<script>
  import { onMount } from 'svelte';
  import ProductCard from './ProductCard.svelte';
  
  let products = [];
  let displayedProducts = [];
  let loading = true;
  let error = null;
  let categories = [];
  let selectedCategory = 'All categories';
  let searchTerm = '';
  let sorting = 'default';

  const fetchProducts = async () => {
      loading = true;
      error = null;
      try {
          const response = await fetch('https://fakestoreapi.com/products');
          if (!response.ok) {
              throw new Error('Failed to fetch products');
          }
          products = await response.json();
          categories = ['All categories', ...new Set(products.map(product => product.category))];
          updateDisplayedProducts();
      } catch (err) {
          error = err.message;
      } finally {
          loading = false;
      }
  };

  const updateDisplayedProducts = () => {
      let filteredProducts = products;
      if (selectedCategory !== 'All categories') {
          filteredProducts = filteredProducts.filter(product => product.category === selectedCategory);
      }
      if (searchTerm) {
          filteredProducts = filteredProducts.filter(product => 
              product.title.toLowerCase().includes(searchTerm.toLowerCase())
          );
      }
      if (sorting === 'low') {
          filteredProducts.sort((a, b) => a.price - b.price);
      } else if (sorting === 'high') {
          filteredProducts.sort((a, b) => b.price - a.price);
      }
      displayedProducts = filteredProducts;
  };

  $: updateDisplayedProducts();

  onMount(() => {
      fetchProducts();
  });
</script>

<div class="controls">
  <select bind:value={sorting} on:change={updateDisplayedProducts} class="p-2 border rounded">
      <option value="default">Default</option>
      <option value="low">Price: Low to High</option>
      <option value="high">Price: High to Low</option>
  </select>

  <input type="text" bind:value={searchTerm} on:input={updateDisplayedProducts} placeholder="Search products..." class="p-2 border rounded">

  <select bind:value={selectedCategory} on:change={updateDisplayedProducts} class="p-2 border rounded">
      <option value="All categories">All categories</option>
      {#each categories as category}
          <option value={category}>{category}</option>
      {/each}
  </select>
</div>

{#if loading}
  <p>Loading...</p>
{:else if error}
  <p class="text-red-500">{error}</p>
{:else if displayedProducts.length === 0}
  <p>No products available.</p>
{:else}
  <div class="grid-container">
      {#each displayedProducts as product (product.id)}
          <ProductCard {product} />
      {/each}
  </div>
{/if}

<style>
  div {
      margin-top: 1rem;
  }

  .controls {
      margin-bottom: 1rem;
      display: flex;
      gap: 1rem;
  }

  .grid-container {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      gap: 1rem;
  }
</style>
