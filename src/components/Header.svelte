

<style>
    .product-card {
        position: relative;
        overflow: hidden;
        background-color: #c2c3c2;
        border: 1px solid #ccc;
        border-radius: 0.5rem;
        transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .product-card:hover {
        transform: scale(1.05); /* Scale up by 5% on hover */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Optional: Add shadow on hover */
    }

    .modal {
        display: none;
        position: fixed;
        z-index: 999;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        justify-content: center;
        align-items: center;
    }

    .modal-content {
        background-color: #ffffff;
        padding: 20px;
        max-width: 600px;
        border-radius: 0.5rem;
        position: relative;
        text-align: center;
    }

    .close-modal {
        position: absolute;
        top: 10px;
        right: 10px;
        cursor: pointer;
    }

    body {
        background-color: #5e5b5b;
    }
</style>

<svelte:head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Product Store</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</svelte:head>

<script>
    let navbarOpen = false; // Define the variable
</script>

<header class="sticky z-50 top-0">
    <!-- ... rest of the header content ... -->
    <nav class="bg-gray-500 border-gray-200">
        <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
            <a href="/">
                <button class="flex items-center space-x-3 rtl:space-x-reverse">
                    <span class="self-center text-2xl font-semibold whitespace-nowrap text-white">SwiftCart</span>
                </button>
            </a>

            <button
                on:click={() => navbarOpen = !navbarOpen}
                type="button"
                class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-white rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200"
                aria-controls="navbar-default"
                aria-expanded={navbarOpen}
            >
                <span class="sr-only">Open main menu</span>
                <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15"/>
                </svg>
            </button>
        </div>
    </nav>
</header>

