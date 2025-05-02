// Navigation Toggle
const menuBtn = document.getElementById('menuBtn');
const mainNav = document.getElementById('mainNav');

menuBtn.addEventListener('click', () => {
    mainNav.classList.toggle('active');
    menuBtn.innerHTML = mainNav.classList.contains('active') ? 
        '<i class="fas fa-times"></i>' : '<i class="fas fa-bars"></i>';
});

// Close menu when clicking on links
const navLinks = document.querySelectorAll('nav ul li a');
navLinks.forEach(link => {
    link.addEventListener('click', () => {
        mainNav.classList.remove('active');
        menuBtn.innerHTML = '<i class="fas fa-bars"></i>';
    });
});

// Active link on scroll
window.addEventListener('scroll', () => {
    let current = '';
    const sections = document.querySelectorAll('section');
    const header = document.querySelector('header');
    const backToTop = document.getElementById('backToTop');
    
    // Show/hide back to top button
    if (window.scrollY > 500) {
        backToTop.classList.add('active');
    } else {
        backToTop.classList.remove('active');
    }
    
    // Change header background on scroll
    if (window.scrollY > 50) {
        header.style.backgroundColor = 'rgba(18, 18, 18, 0.95)';
        header.style.boxShadow = '0 4px 12px rgba(0, 0, 0, 0.1)';
    } else {
        header.style.backgroundColor = 'var(--black)';
        header.style.boxShadow = 'none';
    }
    
    // Active link on scroll
    sections.forEach(section => {
        const sectionTop = section.offsetTop - 100;
        const sectionHeight = section.clientHeight;
        if (window.scrollY >= sectionTop && window.scrollY < sectionTop + sectionHeight) {
            current = section.getAttribute('id');
        }
    });
    
    navLinks.forEach(link => {
        link.classList.remove('active');
        if (link.getAttribute('href') === `#${current}`) {
            link.classList.add('active');
        }
    });
});

// Smooth scrolling
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const targetId = this.getAttribute('href');
        if (targetId === '#cart') {
            document.querySelector('.cart-section').classList.add('active');
            document.querySelectorAll('section:not(.cart-section)').forEach(section => {
                section.style.display = 'none';
            });
            document.querySelector('footer').style.display = 'none';
        } else {
            document.querySelector('.cart-section').classList.remove('active');
            document.querySelectorAll('section:not(.cart-section)').forEach(section => {
                section.style.display = 'block';
            });
            document.querySelector('footer').style.display = 'block';
            
            const target = document.querySelector(targetId);
            window.scrollTo({
                top: target.offsetTop - 80,
                behavior: 'smooth'
            });
        }
    });
});

// Testimonial Slider
const testimonialSlides = document.querySelectorAll('.testimonial-slide');
const prevBtn = document.querySelector('.prev-btn');
const nextBtn = document.querySelector('.next-btn');
let currentSlide = 0;

function showSlide(n) {
    testimonialSlides.forEach(slide => {
        slide.classList.remove('active');
    });
    testimonialSlides[n].classList.add('active');
}

nextBtn.addEventListener('click', () => {
    currentSlide = (currentSlide + 1) % testimonialSlides.length;
    showSlide(currentSlide);
});

prevBtn.addEventListener('click', () => {
    currentSlide = (currentSlide - 1 + testimonialSlides.length) % testimonialSlides.length;
    showSlide(currentSlide);
});

// Auto slide testimonials
setInterval(() => {
    currentSlide = (currentSlide + 1) % testimonialSlides.length;
    showSlide(currentSlide);
}, 5000);

// Shopping Cart Functionality
const products = [
    { id: 1, name: 'Premium Interior Cleaner', price: 24.99, image: '/api/placeholder/100/100' },
    { id: 2, name: 'Professional Wheel Cleaner', price: 19.99, image: '/api/placeholder/100/100' },
    { id: 3, name: 'Luxury Car Wax', price: 34.99, image: '/api/placeholder/100/100' },
    { id: 4, name: 'Premium Microfiber Towels (5-Pack)', price: 15.99, image: '/api/placeholder/100/100' },
    { id: 5, name: 'Streak-Free Glass Cleaner', price: 12.99, image: '/api/placeholder/100/100' },
    { id: 6, name: 'Leather Cleaner & Conditioner', price: 22.99, image: '/api/placeholder/100/100' }
];

let cart = [];
const addToCartBtns = document.querySelectorAll('.add-to-cart-btn');
const cartCountElement = document.getElementById('cartCount');
const cartItemsContainer = document.getElementById('cartItems');
const cartEmptyMessage = document.getElementById('cartEmpty');
const cartSummary = document.getElementById('cartSummary');
const subtotalElement = document.getElementById('subtotal');
const taxElement = document.getElementById('tax');
const totalElement = document.getElementById('total');

// Add to cart
addToCartBtns.forEach(btn => {
    btn.addEventListener('click', function() {
        const productId = parseInt(this.closest('.product-card').getAttribute('data-id'));
        const product = products.find(p => p.id === productId);
        
        const existingItem = cart.find(item => item.id === productId);
        if (existingItem) {
            existingItem.quantity += 1;
        } else {
            cart.push({
                id: product.id,
                name: product.name,
                price: product.price,
                image: product.image,
                quantity: 1
            });
        }
        
        // Show success message
        const successMessage = document.createElement('div');
        successMessage.classList.add('success-message');
        successMessage.style.position = 'fixed';
        successMessage.style.bottom = '20px';
        successMessage.style.right = '20px';
        successMessage.style.backgroundColor = 'var(--primary-blue)';
        successMessage.style.color = 'white';
        successMessage.style.padding = '15px 20px';
        successMessage.style.borderRadius = '5px';
        successMessage.style.boxShadow = '0 5px 15px rgba(0,0,0,0.2)';
        successMessage.style.zIndex = '1000';
        successMessage.textContent = `${product.name} added to cart!`;
        
        document.body.appendChild(successMessage);
        
        setTimeout(() => {
            successMessage.style.opacity = '0';
            successMessage.style.transition = 'opacity 0.5s ease';
            setTimeout(() => {
                document.body.removeChild(successMessage);
            }, 500);
        }, 2000);
        
        updateCart();
    });
});

// Update cart
function updateCart() {
    cartCountElement.textContent = cart.reduce((total, item) => total + item.quantity, 0);
    
    if (cart.length === 0) {
        cartEmptyMessage.style.display = 'block';
        cartSummary.style.display = 'none';
        cartItemsContainer.innerHTML = '';
        return;
    }
    
    cartEmptyMessage.style.display = 'none';
    cartSummary.style.display = 'block';
    cartItemsContainer.innerHTML = '';
    
    let subtotal = 0;
    
    cart.forEach(item => {
        const itemTotal = item.price * item.quantity;
        subtotal += itemTotal;
        
        const cartItemElement = document.createElement('div');
        cartItemElement.classList.add('cart-item');
        cartItemElement.innerHTML = `
            <div class="cart-item-image">
                <img src="${item.image}" alt="${item.name}">
            </div>
            <div class="cart-item-details">
                <h4 class="cart-item-title">${item.name}</h4>
                <div class="cart-item-price">$${item.price.toFixed(2)}</div>
                <div class="cart-item-quantity">
                    <button class="quantity-btn decrease-btn" data-id="${item.id}">-</button>
                    <input type="number" class="quantity-input" value="${item.quantity}" min="1" data-id="${item.id}">
                    <button class="quantity-btn increase-btn" data-id="${item.id}">+</button>
                    <button class="cart-item-remove" data-id="${item.id}">
                        <i class="fas fa-trash"></i> Remove
                    </button>
                </div>
            </div>
        `;
        
        cartItemsContainer.appendChild(cartItemElement);
    });
    
    // Calculate tax and total
    const tax = subtotal * 0.07;
    const total = subtotal + tax;
    
    subtotalElement.textContent = `$${subtotal.toFixed(2)}`;
    taxElement.textContent = `$${tax.toFixed(2)}`;
    totalElement.textContent = `$${total.toFixed(2)}`;
    
    // Add event listeners to quantity buttons and remove buttons
    document.querySelectorAll('.decrease-btn').forEach(btn => {
        btn.addEventListener('click', function() {
            const id = parseInt(this.getAttribute('data-id'));
            const item = cart.find(item => item.id === id);
            if (item.quantity > 1) {
                item.quantity -= 1;
            }
            updateCart();
        });
    });
    
    document.querySelectorAll('.increase-btn').forEach(btn => {
        btn.addEventListener('click', function() {
            const id = parseInt(this.getAttribute('data-id'));
            const item = cart.find(item => item.id === id);
            item.quantity += 1;
            updateCart();
        });
    });
    
    document.querySelectorAll('.quantity-input').forEach(input => {
        input.addEventListener('change', function() {
            const id = parseInt(this.getAttribute('data-id'));
            const item = cart.find(item => item.id === id);
            const value = parseInt(this.value);
            if (value > 0) {
                item.quantity = value;
            } else {
                this.value = item.quantity;
            }
            updateCart();
        });
    });
    
    document.querySelectorAll('.cart-item-remove').forEach(btn => {
        btn.addEventListener('click', function() {
            const id = parseInt(this.getAttribute('data-id'));
            cart = cart.filter(item => item.id !== id);
            updateCart();
        });
    });
}

// Checkout button
document.querySelector('.checkout-btn').addEventListener('click', function() {
    alert('Thank you for your order! This would connect to a payment processor in a real implementation.');
});

// Contact form submission
document.getElementById('contactForm').addEventListener('submit', function(e) {
    e.preventDefault();
    
    // In a real implementation, this would send the form data to a server
    const formData = {
        name: document.getElementById('name').value,
        email: document.getElementById('email').value,
        phone: document.getElementById('phone').value,
        subject: document.getElementById('subject').value,
        message: document.getElementById('message').value
    };
    
    console.log('Form Data:', formData);
    
    // Show success message
    const successMessage = document.createElement('div');
    successMessage.style.backgroundColor = '#4CAF50';
    successMessage.style.color = 'white';
    successMessage.style.padding = '15px';
    successMessage.style.marginTop = '20px';
    successMessage.style.borderRadius = '5px';
    successMessage.textContent = 'Thank you for your message! We will get back to you shortly.';
    
    this.appendChild(successMessage);
    this.reset();
    
    setTimeout(() => {
        this.removeChild(successMessage);
    }, 5000);
});

// Newsletter form submission
document.querySelector('.newsletter-form').addEventListener('submit', function(e) {
    e.preventDefault();
    
    const email = this.querySelector('.newsletter-input').value;
    
    // In a real implementation, this would send the email to a server
    console.log('Newsletter Subscription:', email);
    
    // Show success message
    const successMessage = document.createElement('div');
    successMessage.style.backgroundColor = '#4CAF50';
    successMessage.style.color = 'white';
    successMessage.style.padding = '15px';
    successMessage.style.marginTop = '20px';
    successMessage.style.borderRadius = '5px';
    successMessage.textContent = 'Thank you for subscribing to our newsletter!';
    
    this.appendChild(successMessage);
    this.reset();
    
    setTimeout(() => {
        this.removeChild(successMessage);
    }, 5000);
});

// Initialize cart
updateCart();

// Back to store button from cart
const backToStoreBtn = document.createElement('button');
backToStoreBtn.classList.add('cta-btn');
backToStoreBtn.style.marginTop = '30px';
backToStoreBtn.style.display = 'block';
backToStoreBtn.textContent = 'Continue Shopping';
backToStoreBtn.addEventListener('click', function() {
    document.querySelector('.cart-section').classList.remove('active');
    document.querySelectorAll('section:not(.cart-section)').forEach(section => {
        section.style.display = 'block';
    });
    document.querySelector('footer').style.display = 'block';
    
    // Scroll to store section
    const storeSection = document.getElementById('store');
    window.scrollTo({
        top: storeSection.offsetTop - 80,
        behavior: 'smooth'
    });
});

document.querySelector('.cart-section').appendChild(backToStoreBtn);
