<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kral E-Ticaret</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #ff512f, #dd2476);
    margin: 0;
    padding: 0;
    color: white;
  }
  header {
    background: rgba(0,0,0,0.6);
    padding: 15px;
    text-align: center;
    position: sticky;
    top: 0;
    z-index: 100;
  }
  header h1 {
    margin: 0;
  }
  .stats {
    margin-top: 5px;
    font-size: 14px;
  }
  .container {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(250px,1fr));
    gap: 15px;
    padding: 20px;
  }
  .product {
    background: rgba(255,255,255,0.1);
    border-radius: 8px;
    padding: 15px;
    text-align: center;
    box-shadow: 0 2px 5px rgba(0,0,0,0.3);
  }
  .product img {
    width: 100%;
    height: 150px;
    border-radius: 5px;
    object-fit: cover;
  }
  .product button {
    background: gold;
    border: none;
    padding: 8px 10px;
    margin: 5px;
    color: black;
    font-weight: bold;
    border-radius: 5px;
    cursor: pointer;
  }
  .cart {
    background: rgba(0,0,0,0.5);
    margin: 20px;
    padding: 15px;
    border-radius: 8px;
  }
  .comments {
    background: rgba(0,0,0,0.4);
    margin: 20px;
    padding: 15px;
    border-radius: 8px;
  }
  .comments ul {
    list-style: none;
    padding: 0;
  }
  .comments li {
    background: rgba(255,255,255,0.1);
    margin: 5px 0;
    padding: 5px;
    border-radius: 5px;
  }
</style>
</head>
<body>

<header>
  <h1>🏷️ Kral E-Ticaret</h1>
  <div class="stats">
    Sepet: <span id="cartCount">0</span> ürün | Beğeni: <span id="likes">0</span>
  </div>
</header>

<!-- Ürün Listesi -->
<div class="container" id="product-list"></div>

<!-- Sepet -->
<div class="cart">
  <h2>🛒 Sepet</h2>
  <ul id="cart-items"></ul>
  <p><strong>Toplam:</strong> <span id="total">0</span> ₺</p>
</div>

<!-- Yorumlar -->
<div class="comments">
  <h2>💬 Yorumlar</h2>
  <input type="text" id="commentInput" placeholder="Yorum ekle...">
  <button onclick="addComment()">Ekle</button>
  <ul id="commentList"></ul>
</div>

<script>
let products = [
  { id: 1, name: "Telefon", price: 8500, image: "https://via.placeholder.com/250x150" },
  { id: 2, name: "Laptop", price: 18500, image: "https://via.placeholder.com/250x150" },
  { id: 3, name: "Kulaklık", price: 1500, image: "https://via.placeholder.com/250x150" }
];

let cart = [];
let cartCount = 0;
let likes = 0;

const productList = document.getElementById("product-list");
const cartItems = document.getElementById("cart-items");
const total = document.getElementById("total");

function renderProducts() {
  productList.innerHTML = "";
  products.forEach(p => {
    productList.innerHTML += `
      <div class="product">
        <img src="${p.image}" alt="${p.name}">
        <h3>${p.name}</h3>
        <p>${p.price} ₺</p>
        <button onclick="addToCart(${p.id})">Sepete Ekle</button>
        <button onclick="removeProduct(${p.id})">Sil</button>
        <button onclick="likeProduct()">👍 Beğen</button>
      </div>
    `;
  });
}

function addToCart(id) {
  const product = products.find(p => p.id === id);
  cart.push(product);
  cartCount++;
  document.getElementById("cartCount").textContent = cartCount;
  renderCart();
}

function renderCart() {
  cartItems.innerHTML = "";
  let totalPrice = 0;
  cart.forEach(item => {
    cartItems.innerHTML += `<li>${item.name} - ${item.price} ₺</li>`;
    totalPrice += item.price;
  });
  total.textContent = totalPrice;
}

function removeProduct(id) {
  products = products.filter(p => p.id !== id);
  renderProducts();
}

function likeProduct() {
  likes++;
  document.getElementById("likes").textContent = likes;
}

// Yorum ekleme
function addComment() {
  const commentInput = document.getElementById("commentInput");
  const commentList = document.getElementById("commentList");
  const comment = commentInput.value.trim();
  if (comment !== "") {
    const li = document.createElement("li");
    li.textContent = comment;
    commentList.appendChild(li);
    commentInput.value = "";
  }
}

renderProducts();
</script>

</body>
</html>
