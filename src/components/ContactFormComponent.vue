<template>
  <div class="form">
    <form @submit="handleSubmit" name="contact" class="form__form" netlify netlify-honeypot="bot-field">
      <input type="hidden" name="bot-field">
      <fieldset>
        <div class="field">
          <label for="name" class="label form__label">Name</label>
          <div class="control">
            <input
              @keyup="validateField(formFields.name)"
              type="text"
              name="name"
              id="name"
              class="input form__input"
              placeholder="ex. John Smith"
              v-model="form.name">
          </div>
        </div>
        <div class="field">
          <label for="email" class="label form__label">Email</label>
          <div class="control">
            <input type="email" name="email" id="email" class="input form__input" placeholder="ex. hello@email.com" v-model="form.email">
          </div>
        </div>
        <div class="field">
          <label for="message" class="label form__label">How can we help?</label>
          <div class="control">
            <textarea name="message" id="message" class="textarea form__textarea" v-model="form.message"></textarea>
          </div>
        </div>
        <div class="field">
          <div class="control">
            <button class="button form__button" @click="this.logEvent('click', 'Contact Form Submit')"><span>Submit</span></button>
          </div>
        </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ContactFormComponent',
  data() {
    return {
      form: {
        name: '',
        email: '',
        message: '',
      },
    };
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join('&');
    },
    handleSubmit() {
      fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({ 'form-name': 'contact', ...this.form }),
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/scss/styles.scss';

.form {
  padding: 2rem 1rem;
  background: $slate;
  border-radius: 25px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, .12), 0 1px 2px rgba(0, 0, 0, .24);
  &__label {
    color: #fff;
    font-weight: 700;
    font-style: italic;
    letter-spacing: 1px;
    padding-left: 1rem;
  }
  &__image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 25px;
  }
  &__input {
    border-radius: 25px;
    padding-left: 1rem;
    border-color: darken($slate, 5);
  }
  &__textarea {
    border-radius: 25px;
    padding: 1rem;
    resize: none;
    border-color: darken($slate, 5);
  }
  &__button {
    line-height: 0;
  }
}
</style>
