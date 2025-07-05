<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MarketHive - Marketplace</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import { getFirestore, collection, getDocs } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    async function loadProducts() {
      const querySnapshot = await getDocs(collection(db, "products"));
      const productsContainer = document.querySelector(".products");
      productsContainer.innerHTML = "";
      querySnapshot.forEach((doc) => {
        const data = doc.data();
        const card = document.createElement("div");
        card.className = "product-card";
        card.innerHTML = `
          <img src="${data.image}" alt="${data.name}" />
          <div class="info">
            <h3>${data.name}</h3>
            <p>$${data.price}</p>
          </div>
        `;
        productsContainer.appendChild(card);
      });
    }

    window.addEventListener("DOMContentLoaded", loadProducts);
  </script>
  <style>
    body {
      font-family: 'Inter', sans-serif;
      margin: 0;
      background-color: #f9f9f9;
    }
    header, footer {
      background-color: #2c3e50;
      color: white;
      padding: 20px 40px;
    }
    nav a {
      color: white;
      margin-left: 20px;
      text-decoration: none;
      font-weight: bold;
    }
    .hero {
      background: #ddd;
      text-align: center;
      padding: 80px 20px;
    }
    .products {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 20px;
      padding: 40px;
    }
    .product-card {
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      overflow: hidden;
    }
    .product-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
    }
    .info {
      padding: 20px;
    }
  </style>
</head>
<body>
  <header>
    <h1>MarketHive</h1>
    <nav>
      <a href="index.html">Home</a>
      <a href="add-product.html">Add Product</a>
      <a href="login.html">Login</a>
    </nav>
  </header>

  <section class="hero">
    <h2>Welcome to MarketHive</h2>
    <p>Your local & global product marketplace</p>
  </section>

  <section class="products">
    <p>Loading products...</p>
  </section>

  <footer>
    &copy; 2025 MarketHive
  </footer>
</body>
</html>
