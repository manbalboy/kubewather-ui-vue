<template>
  <div class="container register-page">
    <div class="row">
      <div class="col-md-5 ml-auto">
        <div class="info-area info-horizontal mt-5">
          <div class="icon icon-warning">
            <i class="tim-icons icon-wifi"></i>
          </div>
          <div class="description">
            <h3 class="info-title">Marketing</h3>
            <p class="description">
              We've created the marketing campaign of the website. It was a very interesting collaboration.
            </p>
          </div>
        </div>
        <div class="info-area info-horizontal">
          <div class="icon icon-primary">
            <i class="tim-icons icon-triangle-right-17"></i>
          </div>
          <div class="description">
            <h3 class="info-title">Fully Coded in HTML5</h3>
            <p class="description">
              We've developed the website with HTML5 and CSS3. The client has access to the code using GitHub.
            </p>
          </div>
        </div>
        <div class="info-area info-horizontal">
          <div class="icon icon-info">
            <i class="tim-icons icon-trophy"></i>
          </div>
          <div class="description">
            <h3 class="info-title">Built Audience</h3>
            <p class="description"> There is also a Fully Customizable CMS Admin Dashboard for this product. </p>
          </div>
        </div>
      </div>

      <div class="col-md-7 mr-auto">
        <form @submit.prevent="register">
          <card class="card-register card-white">
            <template slot="header">
              <img class="card-img" src="img/card-primary.png" alt="Card image" />
              <h4 class="card-title">Register</h4>
            </template>

            <BaseInput
              v-model="model.fullName"
              v-validate="'required'"
              :error="getError('Full Name')"
              name="Full Name"
              placeholder="Full Name"
              addon-left-icon="tim-icons icon-single-02"
            >
            </BaseInput>

            <BaseInput
              v-model="model.email"
              v-validate="'required|email'"
              :error="getError('email')"
              name="email"
              placeholder="Email"
              autocomplete="username"
              addon-left-icon="tim-icons icon-email-85"
            >
            </BaseInput>

            <BaseInput
              v-model="model.password"
              v-validate="'required|min:5'"
              :error="getError('password')"
              name="password"
              type="password"
              placeholder="Password"
              autocomplete="current-password"
              addon-left-icon="tim-icons icon-lock-circle"
            >
            </BaseInput>

            <BaseCheckbox class="text-left">
              I agree to the <a href="#something">terms and conditions</a>.
            </BaseCheckbox>

            <base-button slot="footer" native-type="submit" type="primary" round block size="lg">
              Get Started
            </base-button>
          </card>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
  import { BaseCheckbox, BaseInput } from '@/components';

  export default {
    name: 'RegisterPage',
    components: {
      BaseCheckbox,
      BaseInput,
    },
    layout: 'auth',
    data() {
      return {
        model: {
          email: '',
          fullName: '',
          password: '',
        },
      };
    },
    methods: {
      getError(fieldName) {
        return this.errors.first(fieldName);
      },
      async register() {
        const isValidForm = await this.$validator.validateAll();
        if (isValidForm) {
          // TIP use this.model to send it to api and perform register call
        }
      },
    },
  };
</script>
<style></style>
