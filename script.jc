/* script.js */
const MENU_ITEMS = [
    {
        id: 'chicken-biryani',
        name: 'Chicken Biryani',
        description: 'Authentic Mughlai style chicken biryani with aromatic spices and tender chicken pieces.',
        price: 150,
        image: 'https://images.unsplash.com/photo-1563379091339-03b21bc4a4f8?q=80&w=800&auto=format&fit=crop'
    },
    {
        id: 'egg-biryani',
        name: 'Egg Biryani',
        description: 'Fragrant basmati rice cooked with boiled eggs and secret spice blend.',
        price: 125,
        image: 'https://images.unsplash.com/photo-1589302168068-964664d93dc0?q=80&w=800&auto=format&fit=crop'
    },
    {
        id: 'paneer-biryani',
        name: 'Paneer Biryani',
        description: 'Soft paneer cubes marinated in spicy masala and layered with long-grain rice.',
        price: 120,
        image: 'https://images.unsplash.com/photo-1645177625172-5953f9ad8bc3?q=80&w=800&auto=format&fit=crop'
    },
    {
        id: 'chaap-biryani',
        name: 'Chaap Biryani',
        description: 'Soya chaap chunks cooked in a rich, spicy gravy and layered with aromatic rice.',
        price: 130,
        image: 'https://images.unsplash.com/photo-1633945274405-b6c8069047b0?q=80&w=800&auto=format&fit=crop'
    }
];

let cart = {}; // Format: { 'item-id': quantity }

// DOM Elements
const menuContainer = document.getElementById('menu-container');
const cartItemsContainer = document.getElementById('cart-items');
const cartTotalEl = document.getElementById('cart-total');
const cartCountEl = document.getElementById('cart-count');
const cartDrawer = document.getElementById('cart-drawer');
const cartOverlay = document.getElementById('cart-overlay');

// Initialize App
function init() {
    renderMenu();
    updateCartUI();
}

// Render Menu Items
function renderMenu() {
    menuContainer.innerHTML = MENU_ITEMS.map(item => `
        <div class="bg-white rounded-3xl overflow-hidden shadow-xl text-brand-dark flex flex-col group">
            <div class="h-56 overflow-hidden relative">
                <img src="${item.image}" alt="${item.name}" class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500">
                <div class="absolute inset-0 bg-gradient-to-t from-brand-dark/40 to-transparent"></div>
            </div>
            <div class="p-6 flex flex-col flex-grow">
                <div class="flex justify-between items-start mb-2">
                    <h3 class="text-xl font-black font-display">${item.name}</h3>
                    <span class="text-brand-red font-black">₹${item.price}</span>
                </div>
                <p class="text-gray-500 text-sm mb-6 flex-grow">${item.description}</p>
                <button onclick="addToCart('${item.id}')" class="w-full bg-brand-dark/5 hover:bg-brand-red text-brand-dark hover:text-white py-4 rounded-2xl font-bold transition-colors flex items-center justify-center gap-2">
                    <i class="fa-solid fa-cart-plus"></i> Add to Cart
                </button>
            </div>
        </div>
    `).join('');
}

// Cart Logic
function addToCart(id) {
    cart[id] = (cart[id] || 0) + 1;
    updateCartUI();
    openCart();
}

function removeFromCart(id) {
    if (cart[id] > 1) {
        cart[id]--;
    } else {
        delete cart[id];
    }
    updateCartUI();
}

function updateCartUI() {
    let total = 0;
    let count = 0;
    
    if (Object.keys(cart).length === 0) {
        cartItemsContainer.innerHTML = `
            <div class="flex flex-col items-center justify-center h-full text-white/40">
                <i class="fa-solid fa-basket-shopping text-6xl mb-4"></i>
                <p>Your cart is empty</p>
            </div>
        `;
    } else {
        cartItemsContainer.innerHTML = Object.entries(cart).map(([id, quantity]) => {
            const item = MENU_ITEMS.find(m => m.id === id);
            total += item.price * quantity;
            count += quantity;
            return `
                <div class="flex justify-between items-center bg-white/5 p-4 rounded-xl mb-3 border border-white/10">
                    <div>
                        <h4 class="font-bold text-white">${item.name}</h4>
                        <div class="text-brand-gold text-sm font-bold">₹${item.price} <span class="text-white/40 font-normal">x ${quantity}</span></div>
                    </div>
                    <div class="flex items-center gap-3 bg-brand-dark p-1 rounded-lg border border-white/10">
                        <button onclick="removeFromCart('${id}')" class="w-8 h-8 flex items-center justify-center text-white hover:bg-brand-red rounded transition-colors">
                            <i class="fa-solid fa-minus text-xs"></i>
                        </button>
                        <span class="font-bold w-4 text-center text-white">${quantity}</span>
                        <button onclick="addToCart('${id}')" class="w-8 h-8 flex items-center justify-center text-white hover:bg-brand-red rounded transition-colors">
                            <i class="fa-solid fa-plus text-xs"></i>
                        </button>
                    </div>
                </div>
            `;
        }).join('');
    }

    cartTotalEl.innerText = `₹${total}`;
    cartCountEl.innerText = count;
    
    if (count > 0) {
        cartCountEl.classList.remove('hidden');
    } else {
        cartCountEl.classList.add('hidden');
    }
}

// Drawer Controls
function openCart() {
    cartDrawer.classList.remove('translate-x-full');
    cartOverlay.classList.remove('hidden');
    document.body.style.overflow = 'hidden'; // Prevent background scrolling
}

function closeCart() {
    cartDrawer.classList.add('translate-x-full');
    cartOverlay.classList.add('hidden');
    document.body.style.overflow = '';
}

// Checkout Logic
function getOrderDetails() {
    let total = 0;
    let text = "Hello Teekhi Biryani! I'd like to place an order:\n\n";
    
    Object.entries(cart).forEach(([id, quantity]) => {
        const item = MENU_ITEMS.find(m => m.id === id);
        total += item.price * quantity;
        text += `▪ ${quantity}x ${item.name} (₹${item.price * quantity})\n`;
    });
    
    text += `\n*Total Amount: ₹${total}*`;
    return { text, total };
}

function checkoutWhatsApp() {
    if (Object.keys(cart).length === 0) return alert("Please add items to your cart first!");
    
    const { text } = getOrderDetails();
    const phone = "919999035966";
    const whatsappUrl = `https://wa.me/${phone}?text=${encodeURIComponent(text)}`;
    
    window.open(whatsappUrl, '_blank');
}

function checkoutUPI() {
    if (Object.keys(cart).length === 0) return alert("Please add items to your cart first!");
    
    const { total } = getOrderDetails();
    const upiId = "teekhibiryani@upi"; // Replace with your actual merchant UPI ID
    const name = "Teekhi Biryani";
    const upiUrl = `upi://pay?pa=${upiId}&pn=${encodeURIComponent(name)}&am=${total}&cu=INR`;
    
    // Create a temporary link to trigger the UPI intent on mobile devices
    const link = document.createElement('a');
    link.href = upiUrl;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
}

// Run initialization on load
document.addEventListener('DOMContentLoaded', init);
