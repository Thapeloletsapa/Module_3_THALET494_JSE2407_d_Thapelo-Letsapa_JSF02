<script>
  export let product;
</script>

<div class="product-card">
  <img src={product.image} alt={product.title} class="product-image" />
  <h2 class="product-title">{product.title}</h2>
  <p class="product-price">${product.price}</p>
  <p>Category: {product.category}</p>
  <a href={`/products/${product.id}`}>View Details</a>
  <button class="add-to-cart">Add to Cart</button>
</div>

<style>
  .product-card {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 1rem;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s;
  }

  .product-card:hover {
    transform: scale(1.05);
  }

  .product-image {
    width: 100%;
    height: auto;
    border-radius: 8px 8px 0 0;
  }

  .product-title {
    font-size: 1.2rem;
    margin: 0.5rem 0;
  }

  .product-price {
    color: #2c3e50;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  .add-to-cart {
    background-color: #3498db;
    color: #fff;
    border: none;
    border-radius: 4px;
    padding: 0.5rem 1rem;
    cursor: pointer;
  }

  .add-to-cart:hover {
    background-color: #2980b9;
  }
</style>
