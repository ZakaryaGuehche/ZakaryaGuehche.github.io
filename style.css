// ==================== 
// INITIALIZATION
// ====================
document.addEventListener('DOMContentLoaded', function() {
    // Vérifier si AOS existe avant de l'initialiser
    if (typeof AOS !== 'undefined') {
        AOS.init({
            duration: 800,
            easing: 'ease-out',
            once: true,
            offset: 100,
            disable: 'mobile' // Optionnel : désactiver sur mobile pour meilleures performances
        });
    }

    initNavbar();
    initMobileMenu();
    initTypewriter();
    initCountUp();
    initProjectFilters();
    initBackToTop();
    initContactForm();
    initSmoothScroll();
});

// ==================== 
// NAVBAR
// ====================
function initNavbar() {
    const navbar = document.getElementById('navbar');
    if (!navbar) return;
    
    let lastScroll = 0;
    let ticking = false;
    
    window.addEventListener('scroll', function() {
        if (!ticking) {
            window.requestAnimationFrame(function() {
                const currentScroll = window.pageYOffset;
                
                // Scroll effect
                if (currentScroll > 50) {
                    navbar.classList.add('scrolled');
                } else {
                    navbar.classList.remove('scrolled');
                }
                
                // Active section highlighting
                updateActiveSection();
                
                lastScroll = currentScroll;
                ticking = false;
            });
            ticking = true;
        }
    });
}

function updateActiveSection() {
    const sections = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('.nav-link');
    let current = '';
    
    sections.forEach(function(section) {
        const sectionTop = section.offsetTop - 100;
        const sectionHeight = section.clientHeight;
        
        if (window.pageYOffset >= sectionTop && 
            window.pageYOffset < sectionTop + sectionHeight) {
            current = section.getAttribute('id');
        }
    });
    
    navLinks.forEach(function(link) {
        link.classList.remove('active');
        if (link.getAttribute('href').slice(1) === current) {
            link.classList.add('active');
        }
    });
}

// ==================== 
// MOBILE MENU
// ====================
function initMobileMenu() {
    const hamburger = document.getElementById('hamburger');
    const navMenu = document.getElementById('nav-menu');
    const navLinks = document.querySelectorAll('.nav-link');
    
    if (!hamburger || !navMenu) return;
    
    // Toggle menu
    hamburger.addEventListener('click', function() {
        const isActive = hamburger.classList.toggle('active');
        navMenu.classList.toggle('active');
        document.body.style.overflow = isActive ? 'hidden' : '';
        
        // Accessibility
        hamburger.setAttribute('aria-expanded', isActive);
    });
    
    // Close on link click
    navLinks.forEach(function(link) {
        link.addEventListener('click', function() {
            closeMenu();
        });
    });
    
    // Close on escape key
    document.addEventListener('keydown', function(e) {
        if (e.key === 'Escape' && navMenu.classList.contains('active')) {
            closeMenu();
        }
    });
    
    // Close on outside click
    document.addEventListener('click', function(e) {
        if (navMenu.classList.contains('active') && 
            !navMenu.contains(e.target) && 
            !hamburger.contains(e.target)) {
            closeMenu();
        }
    });
    
    function closeMenu() {
        hamburger.classList.remove('active');
        navMenu.classList.remove('active');
        document.body.style.overflow = '';
        hamburger.setAttribute('aria-expanded', 'false');
    }
}

// ==================== 
// TYPEWRITER EFFECT
// ====================
function initTypewriter() {
    const typewriter = document.getElementById('typewriter');
    if (!typewriter) return;
    
    const texts = [
        'Data Analyst',
        'Data Scientist',
        'Python Developer',
        'Power BI Expert'
    ];
    
    let textIndex = 0;
    let charIndex = 0;
    let isDeleting = false;
    let typingSpeed = 100;
    
    function type() {
        const currentText = texts[textIndex];
        
        if (isDeleting) {
            typewriter.textContent = currentText.substring(0, charIndex - 1);
            charIndex--;
            typingSpeed = 50;
        } else {
            typewriter.textContent = currentText.substring(0, charIndex + 1);
            charIndex++;
            typingSpeed = 100;
        }
        
        // Ajouter le curseur clignotant
        typewriter.style.borderRight = '2px solid #3b82f6';
        
        if (!isDeleting && charIndex === currentText.length) {
            isDeleting = true;
            typingSpeed = 2000; // Pause à la fin
        } else if (isDeleting && charIndex === 0) {
            isDeleting = false;
            textIndex = (textIndex + 1) % texts.length;
            typingSpeed = 500; // Pause avant le prochain mot
        }
        
        setTimeout(type, typingSpeed);
    }
    
    type();
}

// ==================== 
// COUNT UP ANIMATION
// ====================
function initCountUp() {
    const counters = document.querySelectorAll('.stat-number');
    
    const observerOptions = { 
        threshold: 0.5,
        rootMargin: '0px 0px -100px 0px'
    };
    
    const observer = new IntersectionObserver(function(entries) {
        entries.forEach(function(entry) {
            if (entry.isIntersecting && !entry.target.classList.contains('counted')) {
                const counter = entry.target;
                counter.classList.add('counted'); // Éviter les répétitions
                
                const target = parseInt(counter.getAttribute('data-count'));
                const duration = 2000;
                const increment = target / (duration / 16);
                let current = 0;
                
                function updateCounter() {
                    current += increment;
                    if (current < target) {
                        counter.textContent = Math.ceil(current);
                        requestAnimationFrame(updateCounter);
                    } else {
                        counter.textContent = target + '+';
                    }
                }
                
                updateCounter();
            }
        });
    }, observerOptions);
    
    counters.forEach(function(counter) {
        observer.observe(counter);
    });
}

// ==================== 
// PROJECT FILTERS
// ====================
function initProjectFilters() {
    const filterBtns = document.querySelectorAll('.filter-btn');
    const projectCards = document.querySelectorAll('.project-card');
    
    if (filterBtns.length === 0 || projectCards.length === 0) return;
    
    filterBtns.forEach(function(btn) {
        btn.addEventListener('click', function() {
            // Update active button
            filterBtns.forEach(function(b) {
                b.classList.remove('active');
            });
            btn.classList.add('active');
            
            const filter = btn.getAttribute('data-filter');
            
            // Filter projects
            projectCards.forEach(function(card, index) {
                const category = card.getAttribute('data-category');
                
                if (filter === 'all' || category === filter) {
                    card.classList.remove('hidden');
                    card.style.opacity = '0';
                    card.style.transform = 'translateY(20px)';
                    
                    setTimeout(function() {
                        card.style.transition = 'all 0.5s ease';
                        card.style.opacity = '1';
                        card.style.transform = 'translateY(0)';
                    }, index * 100);
                } else {
                    card.style.opacity = '0';
                    card.style.transform = 'translateY(20px)';
                    setTimeout(function() {
                        card.classList.add('hidden');
                    }, 300);
                }
            });
            
            // Reinitialize AOS for filtered items
            if (typeof AOS !== 'undefined') {
                AOS.refresh();
            }
        });
    });
}

// ==================== 
// BACK TO TOP
// ====================
function initBackToTop() {
    const backToTop = document.getElementById('backToTop');
    
    if (!backToTop) return;
    
    let ticking = false;
    
    window.addEventListener('scroll', function() {
        if (!ticking) {
            window.requestAnimationFrame(function() {
                if (window.pageYOffset > 300) {
                    backToTop.classList.add('visible');
                } else {
                    backToTop.classList.remove('visible');
                }
                ticking = false;
            });
            ticking = true;
        }
    });
    
    backToTop.addEventListener('click', function(e) {
        e.preventDefault();
        window.scrollTo({
            top: 0,
            behavior: 'smooth'
        });
    });
}

// ==================== 
// CONTACT FORM
// ====================
function initContactForm() {
    const form = document.getElementById('contact-form');
    
    if (!form) return;
    
    // Validation en temps réel
    const inputs = form.querySelectorAll('input, textarea');
    inputs.forEach(function(input) {
        input.addEventListener('blur', function() {
            validateField(input);
        });
        
        input.addEventListener('input', function() {
            if (input.classList.contains('error')) {
                validateField(input);
            }
        });
    });
    
    form.addEventListener('submit', function(e) {
        e.preventDefault();
        
        // Valider tous les champs
        let isValid = true;
        inputs.forEach(function(input) {
            if (!validateField(input)) {
                isValid = false;
            }
        });
        
        if (!isValid) return;
        
        const btn = form.querySelector('.btn-submit');
        const originalText = btn.innerHTML;
        
        btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Envoi en cours...';
        btn.disabled = true;
        
        // Soumettre le formulaire
        fetch(form.action, {
            method: 'POST',
            body: new FormData(form),
            headers: {
                'Accept': 'application/json'
            }
        })
        .then(function(response) {
            if (response.ok) {
                showMessage('Message envoyé avec succès ! 🎉', 'success');
                form.reset();
            } else {
                throw new Error('Erreur lors de l\'envoi');
            }
        })
        .catch(function(error) {
            showMessage('Erreur lors de l\'envoi. Veuillez réessayer.', 'error');
            console.error('Error:', error);
        })
        .finally(function() {
            btn.innerHTML = originalText;
            btn.disabled = false;
        });
    });
    
    function validateField(field) {
        const value = field.value.trim();
        let isValid = true;
        let errorMessage = '';
        
        // Required validation
        if (field.hasAttribute('required') && !value) {
            isValid = false;
            errorMessage = 'Ce champ est requis';
        }
        
        // Email validation
        if (field.type === 'email' && value) {
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(value)) {
                isValid = false;
                errorMessage = 'Email invalide';
            }
        }
        
        // Show/hide error
        const existingError = field.parentElement.querySelector('.error-message');
        if (existingError) {
            existingError.remove();
        }
        
        if (!isValid) {
            field.classList.add('error');
            const errorDiv = document.createElement('div');
            errorDiv.className = 'error-message';
            errorDiv.textContent = errorMessage;
            field.parentElement.appendChild(errorDiv);
        } else {
            field.classList.remove('error');
        }
        
        return isValid;
    }
    
    function showMessage(message, type) {
        const messageDiv = document.createElement('div');
        messageDiv.className = `form-message ${type}`;
        messageDiv.textContent = message;
        
        form.insertBefore(messageDiv, form.firstChild);
        
        setTimeout(function() {
            messageDiv.style.opacity = '0';
            setTimeout(function() {
                messageDiv.remove();
            }, 300);
        }, 5000);
    }
}

// ==================== 
// SMOOTH SCROLL
// ====================
function initSmoothScroll() {
    const links = document.querySelectorAll('a[href^="#"]');
    
    links.forEach(function(link) {
        link.addEventListener('click', function(e) {
            const href = this.getAttribute('href');
            
            if (href === '#' || href === '#!') return;
            
            e.preventDefault();
            
            const target = document.querySelector(href);
            
            if (target) {
                const offsetTop = target.offsetTop - 80;
                
                window.scrollTo({
                    top: offsetTop,
                    behavior: 'smooth'
                });
                
                // Update URL without jumping
                if (history.pushState) {
                    history.pushState(null, null, href);
                }
            }
        });
    });
}

// ==================== 
// UTILITY FUNCTIONS
// ====================

// Debounce function for performance
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

// Throttle function for scroll events
function throttle(func, limit) {
    let inThrottle;
    return function() {
        const args = arguments;
        const context = this;
        if (!inThrottle) {
            func.apply(context, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}

// ==================== 
// CONSOLE MESSAGE
// ====================
console.log('%c👋 Bonjour !', 'font-size: 24px; font-weight: bold; color: #3b82f6;');
console.log('%cMerci de visiter mon portfolio.', 'font-size: 14px; color: #4a4a5a;');
console.log('%cContactez-moi : zakaryaguehche.pro@gmail.com', 'font-size: 14px; color: #3b82f6; font-weight: bold;');
console.log('%c\n💼 Recherche alternance Data Analyst/Scientist\n📅 Disponible : Septembre 2026\n⏰ Rythme : 3 semaines / 1 semaine\n', 'font-size: 12px; color: #10b981;');
