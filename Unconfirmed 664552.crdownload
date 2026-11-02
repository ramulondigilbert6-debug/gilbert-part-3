/**
 * Bright Spark Electrical - Form Validation & Processing (js/validation.js)
 */

document.addEventListener('DOMContentLoaded', () => {
    initEnquiryForm();
    initContactForm();
});

/* 1. Enquiry Form Logic & Cost Calculation */
function initEnquiryForm() {
    const enquiryForm = document.querySelector('.enquiry-form') || document.getElementById('enquiry-form');
    if (!enquiryForm) return;

    const responseContainer = document.getElementById('enquiry-response');

    enquiryForm.addEventListener('submit', (e) => {
        e.preventDefault();

        if (!validateForm(enquiryForm)) return;

        const name = document.getElementById('fullname').value.trim();
        const service = document.getElementById('service-type').value;
        const urgency = document.getElementById('urgency').value;
        const qtyInput = document.getElementById('quantity');
        const quantity = qtyInput ? parseInt(qtyInput.value) || 1 : 1;

        let unitPrice = 0;
        let serviceName = '';

        switch (service) {
            case 'solar':
                unitPrice = 15000;
                serviceName = 'Solar / Inverter Installation';
                break;
            case 'wiring':
                unitPrice = 3500;
                serviceName = 'Residential / Commercial Rewiring';
                break;
            case 'fault':
                unitPrice = 850;
                serviceName = 'Emergency Fault Finding';
                break;
            case 'coc':
                unitPrice = 1800;
                serviceName = 'CoC Inspection & Sign-off';
                break;
            case 'generator':
                unitPrice = 4500;
                serviceName = 'Generator Backup Installation';
                break;
            default:
                unitPrice = 500;
                serviceName = 'General Electrical Service';
        }

        let urgencyMultiplier = 1.0;
        if (urgency === 'urgent') urgencyMultiplier = 1.25;
        if (urgency === 'emergency') urgencyMultiplier = 1.5;

        const totalCost = (unitPrice * quantity) * urgencyMultiplier;

        if (responseContainer) {
            responseContainer.style.display = 'block';
            responseContainer.className = 'response-card success';
            responseContainer.innerHTML = `
                <h3>Quote Estimate Generated!</h3>
                <p>Thank you, <strong>${escapeHTML(name)}</strong>. Here is your initial breakdown for <strong>${serviceName}</strong>:</p>
                <div class="pricing-summary">
                    <p><strong>Base Unit Price:</strong> R${unitPrice.toFixed(2)}</p>
                    <p><strong>Quantity / Units:</strong> ${quantity}</p>
                    <p><strong>Urgency Adjustment:</strong> ${urgency.toUpperCase()}</p>
                    <hr>
                    <p class="grand-total"><strong>Estimated Total: R${totalCost.toFixed(2)}</strong></p>
                </div>
                <p>Our dispatch team will contact you shortly to confirm your booking.</p>
            `;
            enquiryForm.reset();
        }
    });
}

/* 2. Contact Form Logic & mailto: Formatting */
function initContactForm() {
    const contactForm = document.getElementById('contact-form');
    if (!contactForm) return;

    const responseContainer = document.getElementById('contact-response');

    contactForm.addEventListener('submit', (e) => {
        e.preventDefault();

        if (!validateForm(contactForm)) return;

        const name = document.getElementById('contact-name').value.trim();
        const email = document.getElementById('contact-email').value.trim();
        const phone = document.getElementById('contact-phone').value.trim();
        const message = document.getElementById('contact-message').value.trim();

        const recipientEmail = "info@brightsparkelectrical.co.za";
        const emailSubject = encodeURIComponent(`Inquiry from ${name}`);
        const emailBody = encodeURIComponent(
            `Name: ${name}\nEmail: ${email}\nPhone: ${phone}\n\nMessage:\n${message}`
        );

        const mailtoURL = `mailto:${recipientEmail}?subject=${emailSubject}&body=${emailBody}`;

        if (responseContainer) {
            responseContainer.style.display = 'block';
            responseContainer.className = 'response-card success';
            responseContainer.innerHTML = `
                <h3>Message Ready to Send!</h3>
                <p>Thank you, <strong>${escapeHTML(name)}</strong>. Your input has been validated.</p>
                <a href="${mailtoURL}" class="btn btn-primary" style="display:inline-block; margin-top:10px; padding:10px 15px; background:#003366; color:#fff; text-decoration:none; border-radius:4px;">Open Email Client to Send</a>
            `;
            contactForm.reset();
        }
    });
}

/* Validation Engine */
function validateForm(form) {
    let isValid = true;
    const inputs = form.querySelectorAll('input[required], select[required], textarea[required]');

    inputs.forEach(input => {
        let errorElement = document.getElementById(`${input.id}-error`);
        let errorMessage = '';

        if (!input.value.trim()) {
            errorMessage = 'This field is required.';
            isValid = false;
        } else if (input.type === 'email' && !validateEmail(input.value)) {
            errorMessage = 'Please enter a valid email address.';
            isValid = false;
        } else if (input.type === 'tel' && !validatePhone(input.value)) {
            errorMessage = 'Please enter a valid phone number.';
            isValid = false;
        }

        if (errorElement) {
            errorElement.innerText = errorMessage;
            errorElement.style.display = errorMessage ? 'block' : 'none';
        }

        if (errorMessage) {
            input.classList.add('input-error');
        } else {
            input.classList.remove('input-error');
        }
    });

    return isValid;
}

function validateEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

function validatePhone(phone) {
    return /^(\+27|0)[0-9]{9}$/.test(phone.replace(/\s+/g, ''));
}

function escapeHTML(str) {
    return str.replace(/[&<>'"]/g, tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag));
}
