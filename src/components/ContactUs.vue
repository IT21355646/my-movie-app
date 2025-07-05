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
            <input type="text" id="firstName" v-model="form.firstName" placeholder="First Name *" required />
          </div>
          <div class="form-group">
            <input type="text" id="lastName" v-model="form.lastName" placeholder="Last Name *" required />
          </div>
          <div class="form-group">
            <input type="email" id="email" v-model="form.email" placeholder="Email *" required />
          </div>
          <div class="form-group">
            <input type="tel" id="telephone" v-model="form.telephone" placeholder="Telephone" />
          </div>
          <div class="form-group full-width">
            <textarea id="message" v-model="form.message" placeholder="Message"></textarea>
          </div>
          <div class="form-group checkbox-group full-width">
            <input type="checkbox" id="terms" v-model="form.termsAgreed" required />
            <label for="terms">I agree to the Terms & Conditions</label>
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
            height="450"
            style="border:0;"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
        </div>
        <div class="address-info">
          <h3>Amadeus IT Group</h3>
          <p>C. Salvador de Madariaga, 1</p>
          <p>28027 Madrid</p>
          <p>Spain</p>
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

    return {
      form,
      handleSubmit,
    };
  },
};
</script>

<style scoped>
.contact-section {
  padding: 60px 20px;
  width: 100%;
  margin: 0;
  text-align: center;
  color: #fff;
}

.section-title {
  font-size: 2.5em; /* Adjust as per design */
  color: #F0C000; /* Use your accent color */
  margin-bottom: 20px;
  font-weight: bold;
}

.intro-text {
  font-size: 1.1em;
  line-height: 1.6;
  color: #ccc;
  margin-bottom: 40px;
}

.contact-content-wrapper {
  display: flex;
  flex-wrap: wrap; /* Allows wrapping for responsiveness */
  gap: 30px; /* Space between form and map */
  justify-content: center;
  align-items: flex-start; /* Align items to the top */
}

.contact-form-container {
  flex: 1; /* Takes available space */
  min-width: 300px; /* Minimum width before wrapping */
  background-color: #1a1a1a;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  text-align: left; /* Align form labels/inputs left */
}

.form-group {
  margin-bottom: 15px;
  width: calc(50% - 7.5px); /* Two columns layout */
  display: inline-block;
  vertical-align: top; /* Align top for multi-column inputs */
}

.form-group:nth-child(odd) {
  margin-right: 15px; /* Spacing between columns */
}

.form-group.full-width {
  width: 100%;
  margin-right: 0;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  color: #ccc;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group input[type="tel"],
.form-group textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #333;
  border-radius: 5px;
  background-color: #222;
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
  accent-color: #F0C000; /* Style checkbox accent color */
}

.checkbox-group label {
  margin-bottom: 0; /* Override default label margin */
  color: #ccc;
  font-size: 0.95em;
}

.submit-button {
  background-color: #F0C000;
  color: #000;
  padding: 12px 25px;
  border: none;
  border-radius: 5px;
  font-size: 1.1em;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
  width: auto; /* Allow button to size itself */
  min-width: 120px;
  display: block; /* Make it a block element */
  margin: 0 auto; /* Center the button */
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
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  text-align: left;
}

.address-info h3 {
  font-size: 1.5em;
  color: #F0C000;
  margin-top: 0;
  margin-bottom: 10px;
}

.address-info p {
  font-size: 1em;
  color: #ccc;
  margin-bottom: 5px;
  line-height: 1.4;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .contact-content-wrapper {
    flex-direction: column; /* Stack form and map vertically */
    align-items: center; /* Center items when stacked */
  }

  .contact-form-container,
  .map-and-info-container {
    width: 100%; /* Full width when stacked */
  }

  .form-group {
    width: 100%; /* Make all form fields full width */
    margin-right: 0;
  }
}

@media (max-width: 480px) {
  .contact-section {
    padding: 40px 15px;
  }
  .section-title {
    font-size: 2em;
  }
  .intro-text {
    font-size: 0.9em;
  }
  .contact-form-container,
  .map-and-info-container {
    padding: 20px;
  }
  .submit-button {
    padding: 10px 20px;
    font-size: 1em;
  }
}
</style>