<script>
    // @ts-nocheck
      import Header from "./components/Header.svelte";
      import ProductList from "./components/ProductList.svelte";
      import ProductDetail from "./components/ProductDetail.svelte";
      import { writable } from 'svelte/store';
      import { Router, Route } from 'svelte-routing';
    
      // State management for filters and sorting
      export let filters = writable({
        category: 'All categories',
        searchTerm: '',
        sorting: 'default'
      });
    
      const updateFilters = (newFilters) => {
        filters.update(current => ({ ...current, ...newFilters }));
      };
    
      let isMenuOpen = false;
    
      const toggleMenu = () => {
        isMenuOpen = !isMenuOpen;
      };
    </script>
    
    <Header {isMenuOpen} {toggleMenu} />
    
    <Router>
      <Route path="/">
        <ProductList {filters} {updateFilters} />
      </Route>
      <Route path="/products/:id" let:params>
        <ProductDetail {params} />
      </Route>
    </Router>
    
    <style>
      main {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
      }
    </style>