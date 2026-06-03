// ShopSimple - Toko Online JavaScript

// Data Produk
const products = [
    {
        id: 1,
        name: "Headphone Bluetooth Premium",
        price: 299000,
        originalPrice: 499000,
        category: "elektronik",
        emoji: "🎧",
        rating: 4.8,
        sold: 1250
    },
    {
        id: 2,
        name: "Smart Watch Pro Series",
        price: 599000,
        originalPrice: 899000,
        category: "elektronik",
        emoji: "⌚",
        rating: 4.9,
        sold: 890
    },
    {
        id: 3,
        name: "Sneakers Casual Pria",
        price: 359000,
        originalPrice: 559000,
        category: "fashion",
        emoji: "👟",
        rating: 4.7,
        sold: 2100
    },
    {
        id: 4,
        name: "Tas Ransel Laptop",
        price: 189000,
        originalPrice: 299000,
        category: "fashion",
        emoji: "🎒",
        rating: 4.6,
        sold: 1560
    },
    {
        id: 5,
        name: "Paket Snack Premium",
        price: 79000,
        originalPrice: 129000,
        category: "makanan",
        emoji: "🍿",
        rating: 4.9,
        sold: 3200
    },
    {
        id: 6,
        name: "Kopi Arabika 500g",
        price: 149000,
        originalPrice: 229000,
        category: "makanan",
        emoji: "☕",
        rating: 4.8,
        sold: 980
    },
    {
        id: 7,
        name: "Gelang Fashion",
        price: 45000,
        originalPrice: 89000,
        category: "aksesoris",
        emoji: "💎",
        rating: 4.5,
        sold: 4500
    },
    {
        id: 8,
        name: "Power Bank 20000mAh",
        price: 249000,
        originalPrice: 399000,
        category: "elektronik",
        emoji: "🔋",
        rating: 4.7,
        sold: 1800
    },
    {
        id: 9,
        name: "Kaos Polos Premium",
        price: 89000,
        originalPrice: 149000,
        category: "fashion",
        emoji: "👕",
        rating: 4.6,
        sold: 5600
    },
    {
        id: 10,
        name: "Jam Dinding Minimalis",
        price: 129000,
        originalPrice: 199000,
        category: "aksesoris",
        emoji: "🕐",
        rating: 4.4,
        sold: 720
    },
    {
        id: 11,
        name: "Coklat Import Premium",
        price: 119000,
        originalPrice: 179000,
        category: "makanan",
        emoji: "🍫",
        rating: 4.9,
        sold: 1400
    },
    {
        id: 12,
        name: "Wireless Mouse",
        price: 149000,
        originalPrice: 249000,
        category: "elektronik",
        emoji: "🖱️",
        rating: 4.6,
        sold: 3200
    }
];

// Cart State
let cart = [];

// Format harga ke Rupiah
function formatPrice(price) {
    return 'Rp ' + price.toLocaleString('id-ID');
}

// Generate star rating
function generateStars(rating) {
    const fullStars = Math.floor(rating);
    const hasHalfStar = rating % 1 >= 0.5;
    let stars = '';
    
    for (let i = 0; i < fullStars; i++) {
        stars += '★';
    }
    if (hasHalfStar) {
        stars += '½';
    }
    
    return stars;
}

// Render produk
function renderProducts(productsToRender = products) {
    const productGrid = document.getElementById('productGrid');
    
    if (productsToRender.length === 0) {
        productGrid.innerHTML = `
            <div style="grid-column: 1/-1; text-align: center; padding: 50px; color: #999;">
                <p style="font-size: 48px;">🔍</p>
                <p>Produk tidak ditemukan</p>
            </div>
        `;
        return;
    }
    
    productGrid.innerHTML = productsToRender.map(product => `
        <div class="product-card" data-category="${product.category}">
            <div class="product-image">${product.emoji}</div>
            <div class="product-info">
                <div class="product-name">${product.name}</div>
                <div class="product-price">${formatPrice(product.price)}</div>
                <div class="product-original-price">${formatPrice(product.originalPrice)}</div>
                <div class="product-rating">
                    <span class="stars">${generateStars(product.rating)}</span>
                    <span>${product.rating} | Terjual ${product.sold}</span>
                </div>
                <button class="btn-add-cart" onclick="addToCart(${product.id})">
                    🛒 Tambah ke Keranjang
                </button>
            </div>
        </div>
    `).join('');
}

// Filter kategori
function filterCategory(category) {
    // Update active button
    document.querySelectorAll('.category-btn').forEach(btn => {
        btn.classList.remove('active');
    });
    event.target.classList.add('active');
    
    // Filter produk
    if (category === 'semua') {
        renderProducts(products);
    } else {
        const filtered = products.filter(p => p.category === category);
        renderProducts(filtered);
    }
}

// Search produk
function searchProduct() {
    const searchTerm = document.getElementById('searchInput').value.toLowerCase();
    
    if (searchTerm === '') {
        renderProducts(products);
        return;
    }
    
    const filtered = products.filter(p => 
        p.name.toLowerCase().includes(searchTerm) ||
        p.category.toLowerCase().includes(searchTerm)
    );
    
    renderProducts(filtered);
}

// Search on Enter key
document.addEventListener('DOMContentLoaded', function() {
    document.getElementById('searchInput')?.addEventListener('keypress', function(e) {
        if (e.key === 'Enter') {
            searchProduct();
        }
    });
    
    // Render initial products
    renderProducts();
    updateCartUI();
});

// Tambah ke cart
function addToCart(productId) {
    const product = products.find(p => p.id === productId);
    const existingItem = cart.find(item => item.id === productId);
    
    if (existingItem) {
        existingItem.quantity += 1;
    } else {
        cart.push({
            ...product,
            quantity: 1
        });
    }
    
    updateCartUI();
    showNotification(`${product.name} ditambahkan ke keranjang`);
}

// Update quantity
function updateQuantity(productId, change) {
    const item = cart.find(item => item.id === productId);
    
    if (item) {
        item.quantity += change;
        
        if (item.quantity <= 0) {
            removeFromCart(productId);
        } else {
            updateCartUI();
        }
    }
}

// Hapus dari cart
function removeFromCart(productId) {
    cart = cart.filter(item => item.id !== productId);
    updateCartUI();
}

// Update UI cart
function updateCartUI() {
    const cartCount = document.getElementById('cartCount');
    const cartItems = document.getElementById('cartItems');
    const totalPrice = document.getElementById('totalPrice');
    
    // Update count
    const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
    cartCount.textContent = totalItems;
    
    // Update items
    if (cart.length === 0) {
        cartItems.innerHTML = `
            <div class="cart-empty">
                <div class="cart-empty-icon">🛒</div>
                <p>Keranjang belanja masih kosong</p>
            </div>
        `;
    } else {
        cartItems.innerHTML = cart.map(item => `
            <div class="cart-item">
                <div class="cart-item-image">${item.emoji}</div>
                <div class="cart-item-details">
                    <div class="cart-item-name">${item.name}</div>
                    <div class="cart-item-price">${formatPrice(item.price)}</div>
                    <div class="cart-item-quantity">
                        <button class="qty-btn" onclick="updateQuantity(${item.id}, -1)">-</button>
                        <span>${item.quantity}</span>
                        <button class="qty-btn" onclick="updateQuantity(${item.id}, 1)">+</button>
                    </div>
                </div>
                <button class="remove-btn" onclick="removeFromCart(${item.id})">Hapus</button>
            </div>
        `).join('');
    }
    
    // Update total
    const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
    totalPrice.textContent = formatPrice(total);
}

// Toggle cart sidebar
function toggleCart() {
    const cartSidebar = document.getElementById('cartSidebar');
    const overlay = document.getElementById('overlay');
    
    cartSidebar.classList.toggle('open');
    overlay.classList.toggle('show');
}

// Checkout
function checkout() {
    if (cart.length === 0) {
        showNotification('Keranjang masih kosong!');
        return;
    }
    
    const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
    const itemCount = cart.reduce((sum, item) => sum + item.quantity, 0);
    
    alert(`Terima kasih telah berbelanja!\n\nTotal: ${formatPrice(total)}\nJumlah Item: ${itemCount}\n\nPesanan Anda sedang diproses.`);
    
    // Clear cart
    cart = [];
    updateCartUI();
    toggleCart();
}

// Show notification
function showNotification(message) {
    const notification = document.getElementById('notification');
    notification.textContent = message;
    notification.classList.add('show');
    
    setTimeout(() => {
        notification.classList.remove('show');
    }, 3000);
}
