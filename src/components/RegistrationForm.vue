<template>
  <div>
    <div v-if="!registered">
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
          <div
            v-if="error.length > 0"
            class="text-caption text-negative q-mt-md"
          >
            {{ error }}
          </div>
        </div>
      </q-card>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // store and retrive user data
      userData: {},
      usersID: 0,
      name: "",
      email: "",
      password: "",
      error: "",
      //   use this property to detect if user is registerd or not
    //   then toggle to show tweet content
      registered: false
    };
  },
  methods: {
    registerAccount() {
      if (this.name !== "" && this.email !== "" && this.password !== "") {
        (this.userData.id = ++this.usersID),
          // record user details
          (this.userData.name = this.name),
          (this.userData.email = this.email),
          (this.userData.password = this.password);
      } else {
        this.error = "Please complete all the form fields";
      }

      // add registration to localstorage
      localStorage.setItem("simple_tweet_registered", true);
      //   Add the whole userData object as JSON string
      localStorage.setItem(
        "simple_tweet_registered_user",
        JSON.stringify(this.userData)
      );

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
