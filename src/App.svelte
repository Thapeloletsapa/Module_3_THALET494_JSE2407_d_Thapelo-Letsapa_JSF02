<script>
// @ts-nocheck

    import Header from "./components/Header.svelte";
    import ProductList from "./components/ProductList.svelte";
  </script>
  
  <main >
    <Header />
    <ProductList />
  </main>

  <style>
    main {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }
  </style>