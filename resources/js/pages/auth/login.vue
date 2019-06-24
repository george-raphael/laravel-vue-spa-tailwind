<template>
  <div class="container mx-auto h-full flex justify-center items-center">
    <div class="md:w-1/2">
      <tw-card :title="$t('login')">
        <form @submit.prevent="login" @keydown="form.onKeydown($event)">

          <!-- Email -->
          <div class="mt-4">
            <label class="col-md-3 col-form-label text-md-right" for="email">{{ $t('email') }}</label>
            <div class="col-md-7">
              <input v-model="form.email" :class="{ 'is-invalid': form.errors.has('email') }" class="form-input" type="email" name="email" id="email" placeholder="username@example.com" required autocomplete="email">
              <has-error :form="form" field="email" />
            </div>
          </div>

          <!-- Password -->
          <div class="mt-4">
            <label class="col-md-3 col-form-label text-md-right" for="password">{{ $t('password') }}</label>
            <div class="col-md-7">
              <input v-model="form.password" :class="{ 'is-invalid': form.errors.has('password') }" class="form-input" type="password" name="password" id="password" required autocomplete="current-password">
              <has-error :form="form" field="password" />
            </div>
          </div>

          <!-- Remember Me -->
          <div class="mt-4">
            <div class="flex items-center justify-between">
              <tw-checkbox v-model="remember" name="remember">{{ $t('remember_me') }}</tw-checkbox>
            </div>
          </div>

          <div class="mt-4 flex items-center justify-between">
            <!-- Submit Button -->
            <v-button :loading="form.busy">{{ $t('login') }}</v-button>
            <router-link :to="{ name: 'password.request' }" class="inline-block align-baseline font-bold text-sm text-blue hover:text-blue-darker no-underline">
              {{ $t('forgot_password') }}
            </router-link>

            <!-- GitHub Login Button -->
            <login-with-github />
          </div>

        </form>
      </tw-card>
    </div>
  </div>
</template>

<script>
import Form from 'vform'
import LoginWithGithub from '~/components/LoginWithGithub'

export default {
  middleware: 'guest',

  components: {
    LoginWithGithub
  },

  metaInfo () {
    return { title: this.$t('login') }
  },

  data: () => ({
    form: new Form({
      email: '',
      password: ''
    }),
    remember: false
  }),

  methods: {
    async login () {
      // Submit the form.
      const { data } = await this.form.post('/api/login')

      // Save the token.
      this.$store.dispatch('auth/saveToken', {
        token: data.token,
        remember: this.remember
      })

      // Fetch the user.
      await this.$store.dispatch('auth/fetchUser')

      // Redirect home.
      this.$router.push({ name: 'home' })
    }
  }
}
</script>
