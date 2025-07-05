<template>
  <section class="contact-section">
    <h2 class="section-title">How to reach us</h2>
    <p class="intro-text">
      Lorem ipsum dolor sit amet, consetetur sadipscing elitr.
    </p>

    <div class="contact-content-wrapper">
      <div class="contact-form-container">
        <form @submit.prevent="handleSubmit" class="contact-form">
          <div class="form-group">
            <label for="firstName">First Name *</label>
            <input type="text" id="firstName" v-model="form.firstName" required />
          </div>
          <div class="form-group">
            <label for="lastName">Last Name *</label>
            <input type="text" id="lastName" v-model="form.lastName" required />
          </div>
          <div class="form-group full-width">
            <label for="email">Email *</label>
            <input type="email" id="email" v-model="form.email" required />
          </div>
          <div class="form-group full-width">
            <label for="telephone">Telephone</label>
            <input type="tel" id="telephone" v-model="form.telephone" />
          </div>
          <div class="form-group full-width">
            <label for="message">Message</label>
            <textarea id="message" v-model="form.message"></textarea>
            <p class="required-note">* required fields</p>
          </div>
          <div class="form-group checkbox-group full-width">
            <input type="checkbox" id="terms" v-model="form.termsAgreed" required />
            <label for="terms">I agree to the <span class="terms-link" @click="openTermsAndConditions">Terms & Conditions</span></label>
          </div>
          <div class="form-group full-width">
            <button type="submit" class="submit-button">SUBMIT</button>
          </div>
        </form>
      </div>

      <div class="map-and-info-container">
        <div class="map-placeholder">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3039.294960309995!2d-3.704256423023403!3d40.4216766714493!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd422896d888e73d%3A0xb30e068e8d5f3d3!2sAmadeus%20IT%20Group!5e0!3m2!1sen!2ses!4v1701389880000!5m2!1sen!2ses"
            width="100%"
            height="530"
            style="border:0;"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
        </div>
      </div>
    </div>

    <!-- Terms & Conditions Modal -->
    <div v-if="showTermsModal" class="modal-overlay" @click="closeTermsModal">
      <div class="modal-content" @click.stop>
        <div class="modal-header">
          <h2>Terms & Conditions</h2>
          <button class="modal-close" @click="closeTermsModal">&times;</button>
        </div>
        <div class="modal-body">
          <p>Welcome to our Movie App. By using our services, you agree to the following terms and conditions:</p>
          
          <h3>1. Acceptance of Terms</h3>
          <p>By accessing and using this movie application, you accept and agree to be bound by the terms and provision of this agreement.</p>
          
          <h3>2. Use License</h3>
          <p>Permission is granted to temporarily use our movie app for personal, non-commercial transitory viewing only. This is the grant of a license, not a transfer of title.</p>
          
          <h3>3. User Account</h3>
          <p>When you create an account with us, you must provide information that is accurate, complete, and current at all times.</p>
          
          <h3>4. Privacy Policy</h3>
          <p>Your privacy is important to us. Please review our Privacy Policy, which also governs your use of the service.</p>
          
          <h3>5. Prohibited Uses</h3>
          <p>You may not use our service for any unlawful purpose or to solicit others to perform unlawful acts.</p>
          
          <h3>6. Contact Information</h3>
          <p>If you have any questions about these Terms & Conditions, please contact us at support@movieapp.com</p>
        </div>
        <div class="modal-footer">
          <button class="modal-btn" @click="closeTermsModal">Close</button>
        </div>
      </div>
    </div>
  </section>
  <section class="address-info">
    <div class="address-content">
      <div class="address-left">
        <h3>Amadeus IT Group</h3>
        <p>C. Salvador de Madariaga, 1</p>
        <p>28027 Madrid</p>
        <p>Spain</p>
      </div>
      <div class="address-right">
        <p class="follow-text">Follow us on</p>
        <div class="social-icons">
          <img src="/src/assets/Icons/Twitter White.svg" alt="Twitter" class="social-icon" />
          <img src="/src/assets/Icons/Youtube White.svg" alt="YouTube" class="social-icon" />
        </div>
      </div>
    </div>
  </section>
  
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'AppContactUs',
  setup() {
    const form = ref({
      firstName: '',
      lastName: '',
      email: '',
      telephone: '',
      message: '',
      termsAgreed: false,
    });

    const showTermsModal = ref(false);

    const handleSubmit = () => {
      // Placeholder for form submission logic
      // In a real application, you would send this data to a backend API
      if (form.value.termsAgreed && form.value.firstName && form.value.lastName && form.value.email) {
        console.log('Form Submitted:', form.value);
        alert('Thank you for your message! (Check console for data)');
        // Optionally reset form
        form.value = {
          firstName: '',
          lastName: '',
          email: '',
          telephone: '',
          message: '',
          termsAgreed: false,
        };
      } else {
        alert('Please fill in all required fields and agree to the terms.');
      }
    };

    const openTermsAndConditions = () => {
      showTermsModal.value = true;
    };

    const closeTermsModal = () => {
      showTermsModal.value = false;
    };

    return {
      form,
      handleSubmit,
      openTermsAndConditions,
      showTermsModal,
      closeTermsModal,
    };
  },
};
</script>

<style scoped>
.contact-section {
  display: flex;
  flex-direction: column;
  padding: 60px 80px;
  width: 100vw;
  margin: 0;
  box-sizing: border-box;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
  text-align: left;
  color: #fff;
  background-color: #000;
}

.section-title {
  font-size: 2.5em; /* Adjust as per design */
  margin-bottom: 5px;
  font-weight: bold;
}

.intro-text {
  font-size: 1.1em;
  line-height: 1.6;
  color: #b4b4b4;
  margin-bottom: 40px;
}

.contact-content-wrapper {
  display: flex;
  flex-wrap: wrap; /* Allows wrapping for responsiveness */
  gap: 80px; /* Increased from 30px to make larger gap */
  justify-content: center;
  align-items: flex-start; /* Align items to the top */
}

.contact-form-container {
  flex: 1;
  min-width: 300px;
  max-width: 500px; /* Added max-width to make form smaller */
  text-align: left; /* Align form labels/inputs left */
}

.form-group {
  margin-bottom: 15px;
  width: calc(50% - 10px); /* Reduced spacing between columns */
  display: inline-block;
  vertical-align: top; /* Align top for multi-column inputs */
}

.form-group:nth-child(odd) {
  margin-right: 20px; /* Increased spacing between columns */
}

.form-group.full-width {
  width: 100%;
  margin-right: 0;
}

.form-group label {
  display: block;
  margin-bottom: 1px;
  color: #b4b4b4;
  font-weight: 500;
  font-size: 1.1em;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group input[type="tel"],
.form-group textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #333;
  border-radius: 5px;
  background-color: #3c3c3c;
  color: #fff;
  font-size: 1em;
  box-sizing: border-box; /* Include padding in width */
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #888;
}

.form-group textarea {
  min-height: 100px;
  resize: vertical; /* Allow vertical resizing */
}

.checkbox-group {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.checkbox-group input[type="checkbox"] {
  margin-right: 10px;
  width: 20px;
  height: 20px;
  appearance: none;
  -webkit-appearance: none;
  border: 2px solid #ccc;
  background-color: transparent;
  position: relative;
  cursor: pointer;
}

.checkbox-group input[type="checkbox"]:checked {
  background-color: #F0C000;
  border-color: #F0C000;
}

.checkbox-group input[type="checkbox"]:checked::after {
  content: '✓';
  position: absolute;
  top: -2px;
  left: 2px;
  color: #000;
  font-size: 14px;
  font-weight: bold;
}

.checkbox-group label {
  margin-bottom: 0;
  margin-left: 0;
  color: #888;
  font-size: 1.1em;
  font-weight: normal;
}

.terms-link {
  color: #ccc;
  text-decoration: underline;
  cursor: pointer;
  transition: color 0.3s ease;
}

.terms-link:hover {
  color: #F0C000;
  text-decoration: underline;
}

.required-note {
  color: #b4b4b4;
  font-size: 1.1em;
  margin-top: 5px;
  margin-bottom: 0;
  text-align: left;
}

.submit-button {
  background-color: #F0C000;
  color: #fff;
  padding: 12px 40px; /* Increased padding for longer button */
  border: none;
  border-radius: 5px;
  font-size: 1.1em;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
  width: auto;
  min-width: 180px; /* Increased min-width */
  display: block;
  margin: 0 0 0 auto;
}

.submit-button:hover {
  background-color: #e0b000;
}

.map-and-info-container {
  flex: 1;
  min-width: 300px; /* Minimum width before wrapping */
  display: flex;
  flex-direction: column;
  gap: 30px; /* Space between map and address info */
}

.map-placeholder iframe {
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.address-info {
  background-color: #1a1a1a;
  padding: 30px 80px;
  border-radius: 0;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  text-align: left;
  width: 100vw;
  margin: 0;
  box-sizing: border-box;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
  color: #fff;
}

.address-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
}

.address-left {
  flex: 1;
}

.address-right {
  display: flex;
  align-items: center;
  gap: 15px;
}

.address-info h3 {
  font-size: 1.1em;
  margin: 0 0 15px 0;
}

.address-info p {
  font-size: 1em;
  margin: 5px 0;
  line-height: 1.4;
}

.follow-text {
  font-size: 1em;
  margin: 0;
  white-space: nowrap;
}

.social-icons {
  display: flex;
  gap: 10px;
}

.social-icon {
  width: 24px;
  height: 24px;
  cursor: pointer;
  transition: opacity 0.3s ease;
}

.social-icon:hover {
  opacity: 0.7;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
}

.modal-content {
  background-color: #1a1a1a;
  border-radius: 8px;
  max-width: 600px;
  max-height: 80vh;
  width: 90%;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 30px;
  border-bottom: 1px solid #333;
}

.modal-header h2 {
  color: #F0C000;
  margin: 0;
  font-size: 1.5em;
}

.modal-close {
  background: none;
  border: none;
  color: #ccc;
  font-size: 2em;
  cursor: pointer;
  padding: 0;
  line-height: 1;
  transition: color 0.3s ease;
}

.modal-close:hover {
  color: #F0C000;
}

.modal-body {
  padding: 30px;
  max-height: 60vh;
  overflow-y: auto;
  color: #ccc;
  line-height: 1.6;
}

.modal-body h3 {
  color: #fff;
  font-size: 1.2em;
  margin-top: 20px;
  margin-bottom: 10px;
}

.modal-body p {
  margin-bottom: 15px;
}

.modal-footer {
  padding: 20px 30px;
  border-top: 1px solid #333;
  text-align: right;
}

.modal-btn {
  background-color: #F0C000;
  color: #000;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  font-size: 1em;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.modal-btn:hover {
  background-color: #e0b000;
}

/* Responsive adjustments */
@media (max-width: 992px) {
  .contact-section {
    padding: 60px 60px;
  }
  
  .contact-content-wrapper {
    gap: 60px; /* Reduced gap for tablets */
  }
  
  .contact-form-container,
  .map-and-info-container {
    min-width: 280px;
  }

  .address-info {
    padding: 30px 60px;
  }
}

@media (max-width: 768px) {
  .contact-section {
    padding: 40px 40px;
  }
  
  .contact-content-wrapper {
    flex-direction: column;
    align-items: center;
    gap: 50px; /* Reduced gap for mobile */
  }

  .contact-form_container,
  .map-and-info-container {
    width: 100%;
    max-width: 100%;
  }

  .form-group {
    width: 100%;
    margin-right: 0;
    margin-bottom: 20px;
  }
  
  .section-title {
    font-size: 2em;
  }
  
  .intro-text {
    font-size: 1em;
  }

  .address-info {
    padding: 30px 40px;
  }

  .address-content {
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
  }

  .address-right {
    align-self: flex-start;
  }
  
  .address-info h3 {
    margin-bottom: 10px;
  }
  
  .address-info p {
    margin-bottom: 5px;
  }
}

@media (max-width: 480px) {
  .contact-section {
    padding: 30px 20px;
  }
  
  .section-title {
    font-size: 1.8em;
  }
  
  .intro-text {
    font-size: 0.9em;
    margin-bottom: 30px;
  }
  
  .contact-form-container,
  .map-and-info-container {
    padding: 20px;
  }
  
  .submit-button {
    padding: 12px 20px;
    font-size: 1em;
    width: 100%;
    max-width: 200px;
  }
  
  .map-placeholder iframe {
    height: 400px; /* Increased from 300px */
  }

  .address-info {
    padding: 30px 20px;
  }
}
</style>