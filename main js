/**
 * Bright Spark Electrical - Main JavaScript Enhancements (js/main.js)
 */

document.addEventListener('DOMContentLoaded', () => {
    initAccordion();
    initLeafletMap();
    initLightbox();
    initDynamicSearch();
});

/* 1. Interactive FAQ Accordion */
function initAccordion() {
    const accordionHeaders = document.querySelectorAll('.accordion-header');
    
    accordionHeaders.forEach(header => {
        header.addEventListener('click', () => {
            const accordionItem = header.parentElement;
            const accordionContent = header.nextElementSibling;
            const isActive = accordionItem.classList.contains('active');
            
            document.querySelectorAll('.accordion-item').forEach(item => {
                item.classList.remove('active');
                if (item.querySelector('.accordion-content')) {
                    item.querySelector('.accordion-content').style.maxHeight = null;
                }
            });

            if (!isActive) {
                accordionItem.classList.add('active');
                accordionContent.style.maxHeight = accordionContent.scrollHeight + 'px';
            }
        });
    });
}

/* 2. Leaflet.js Interactive Map Integration */
function initLeafletMap() {
    const mapElement = document.getElementById('store-map');
    if (!mapElement) return;

    // Polokwane Central Coordinates
    const storeCoordinates = [-23.9045, 29.4217];

    const map = L.map('store-map').setView(storeCoordinates, 14);

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

    L.marker(storeCoordinates).addTo(map)
        .bindPopup(`
            <strong>Bright Spark Electrical HQ</strong><br>
            45 Market Street, Polokwane Central<br>
            <em>24/7 Emergency Response Available</em>
        `).openPopup();
}

/* 3. Modal Lightbox Gallery */
function initLightbox() {
    const galleryImages = document.querySelectorAll('.lightbox-trigger');
    const lightboxModal = document.getElementById('lightbox-modal');
    if (!lightboxModal) return;

    const lightboxImg = document.getElementById('lightbox-img');
    const lightboxCaption = document.getElementById('lightbox-caption');
    const closeBtn = document.querySelector('.lightbox-close');

    galleryImages.forEach(img => {
        img.addEventListener('click', () => {
            lightboxModal.style.display = 'block';
            lightboxImg.src = img.src;
            lightboxCaption.innerText = img.alt || 'Bright Spark Project Showcase';
        });
    });

    if (closeBtn) {
        closeBtn.addEventListener('click', () => {
            lightboxModal.style.display = 'none';
        });
    }

    lightboxModal.addEventListener('click', (e) => {
        if (e.target === lightboxModal) {
            lightboxModal.style.display = 'none';
        }
    });
}

/* 4. Real-Time Menu Search & Filtering (menu.html) */
function initDynamicSearch() {
    const searchInput = document.getElementById('catalogue-search');
    const categoryFilter = document.getElementById('category-filter');
    const items = document.querySelectorAll('.searchable-item');

    if (!searchInput && !categoryFilter) return;

    function filterItems() {
        const query = searchInput ? searchInput.value.toLowerCase().trim() : '';
        const selectedCategory = categoryFilter ? categoryFilter.value.toLowerCase() : 'all';

        items.forEach(item => {
            const title = item.querySelector('.item-title')?.innerText.toLowerCase() || '';
            const description = item.querySelector('.item-desc')?.innerText.toLowerCase() || '';
            const category = item.dataset.category ? item.dataset.category.toLowerCase() : '';

            const matchesQuery = title.includes(query) || description.includes(query);
            const matchesCategory = selectedCategory === 'all' || category === selectedCategory;

            if (matchesQuery && matchesCategory) {
                item.style.display = '';
            } else {
                item.style.display = 'none';
            }
        });
    }

    if (searchInput) searchInput.addEventListener('input', filterItems);
    if (categoryFilter) categoryFilter.addEventListener('change', filterItems);
}
