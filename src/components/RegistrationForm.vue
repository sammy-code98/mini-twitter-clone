<template>
  <div>
    <q-card class="my-card">
      <q-item>
        <q-item-section avatar>
          <q-avatar>
            <q-icon
              name="mdi-twitter"
              class="text-primary"
              style="font-size: 2em;"
            />
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-weight-bold text-grey"
            >Create your account</q-item-label
          >
        </q-item-section>
      </q-item>

      <div class="q-pa-md" style="max-width: 400px">
        <q-form @submit.prevent="registerAccount">
          <q-input
            class="q-mb-md"
            outlined
            rounded
            dense
            v-model="name"
            label="Name *"
          />
          <q-input
            class="q-mb-md"
            outlined
            rounded
            dense
            v-model="email"
            type="email"
            label="Email *"
          />
          <q-input
            class="q-mb-md"
            outlined
            rounded
            dense
            type="password"
            v-model="password"
            label="Password *"
          />
          <div>
            <q-btn
              label="Register"
              no-caps
              type="submit"
              color="primary"
              rounded
              class="full-width"
            />
          </div>
        </q-form>
      </div>
    </q-card>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // store and retrive user data
      userData: {},
      name: "",
      email: "",
      password: ""
    };
  },
  methods: {
    registerAccount() {
      // record user details
      (this.userData.name = this.name),
        (this.userData.email = this.email),
        (this.userData.password = this.password);

      // add registration to localstorage

      // clear registration fields
    //   this clears the input fields once the user submits
      this.name = "";
      this.email = "";
      this.password = "";
      console.log(this.userData);
    }
  }
};
</script>
<style lang="sass" scoped>
.my-card
  width: 100%
  max-width: 250px
</style>
