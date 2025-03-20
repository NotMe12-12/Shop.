body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
    background-color: #f8f8f8;
}

header {
    background: #333;
    color: white;
    padding: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.cart-icon {
    cursor: pointer;
    font-size: 18px;
}

.products {
    display: flex;
    justify-content: center;
    margin-top: 20px;
}

.product {
    background: white;
    padding: 15px;
    margin: 10px;
    border-radius: 8px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    width: 200px;
}

.product img {
    width: 100%;
    border-radius: 5px;
}

button {
    background: #ff5733;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    margin-top: 10px;
}

button:hover {
    background: #c70039;
}

/* Giỏ hàng */
.cart {
    position: fixed;
    right: -300px;
    top: 0;
    width: 250px;
    height: 100%;
    background: white;
    box-shadow: -3px 0px 10px rgba(0, 0, 0, 0.2);
    padding: 20px;
    transition: 0.3s;
}

.cart.show {
    right: 0;
}

.cart ul {
    list-style: none;
    padding: 0;
}

.cart li {
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
}

.cart button {
    width: 100%;
    margin-top: 10px;
    background: red;
}
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cửa Hàng Giày</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Cửa Hàng Giày</h1>
        <div class="cart-icon" onclick="toggleCart()">🛒 Giỏ hàng (<span id="cart-count">0</span>)</div>
    </header>

    <section class="products">
        <div class="product">
            <img src="shoe1.jpg" alt="Giày Thể Thao">
            <h2>Giày Thể Thao</h2>
            <p>Giá: <span class="price">800000</span>đ</p>
            <button onclick="addToCart('Giày Thể Thao', 800000)">Mua ngay</button>
        </div>
        <div class="product">
            <img src="shoe2.jpg" alt="Giày Da Nam">
            <h2>Giày Da Nam</h2>
            <p>Giá: <span class="price">1200000</span>đ</p>
            <button onclick="addToCart('Giày Da Nam', 1200000)">Mua ngay</button>
        </div>
    </section>

    <!-- Giỏ hàng -->
    <div class="cart" id="cart">
        <h2>Giỏ hàng</h2>
        <ul id="cart-items"></ul>
        <p><strong>Tổng tiền:</strong> <span id="cart-total">0</span>đ</p>
        <button onclick="clearCart()">Xóa giỏ hàng</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
let cart = [];
let cartCount = 0;
let cartTotal = 0;

// Thêm sản phẩm vào giỏ hàng
function addToCart(name, price) {
    cart.push({ name, price });
    cartCount++;
    cartTotal += price;

    document.getElementById("cart-count").innerText = cartCount;
    updateCart();
}

// Cập nhật giỏ hàng
function updateCart() {
    let cartItems = document.getElementById("cart-items");
    cartItems.innerHTML = "";

    cart.forEach((item, index) => {
        let li = document.createElement("li");
        li.innerHTML = `${item.name} - ${item.price.toLocaleString()}đ 
                        <button onclick="removeFromCart(${index})">❌</button>`;
        cartItems.appendChild(li);
    });

    document.getElementById("cart-total").innerText = cartTotal.toLocaleString();
}

// Xóa sản phẩm khỏi giỏ hàng
function removeFromCart(index) {
    cartTotal -= cart[index].price;
    cart.splice(index, 1);
    cartCount--;

    document.getElementById("cart-count").innerText = cartCount;
    updateCart();
}

// Xóa toàn bộ giỏ hàng
function clearCart() {
    cart = [];
    cartCount = 0;
    cartTotal = 0;

    document.getElementById("cart-count").innerText = cartCount;
    updateCart();
}

// Mở/đóng giỏ hàng
function toggleCart() {
    document.getElementById("cart").classList.toggle("show");
}
