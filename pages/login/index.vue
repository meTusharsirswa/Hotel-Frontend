<template>
  <section>
    <v-container>
      <v-row align="center" justify="center" class="mt-12">
        <v-col cols="12" sm="6" md="12">
          <v-card flat class="my-13 mx-auto" width="50%">
            <v-card-text>
              <h3 class="">Login your Account</h3>
              <v-row>
                <v-col cols="12">
                  <ValidationObserver
                  ref="file-details-form"
                  v-slot="{handleSubmit}"
                  >
                  <form @submit.prevent="handleSubmit(login)" class="">
                    <ValidationProvider
                    name="email"
                    rules="required"
                    v-slot="{errors}"
                    >

                    <v-text-field
                      v-model="form.email"
                      label="Email"
                      autocomplete="false"
                      class="mt-3"
                      outlined
                      :error-messages = "errors"
                      :hide-details = "!errors.length"
                    >
                    </v-text-field>
                                        </ValidationProvider>
                    <ValidationProvider
                    name="password"
                    rules="required"
                    v-slot="{ errors }"
                    >

                    <v-text-field
                      v-model="form.password"
                      label="Password"
                      outlined
                      autocomplete=" false"
                      class="mt-3"
                      type="password"
                      :error-messages = "errors"
                      :hide-details = "!errors.length"
                    >

                    </v-text-field>
                    </ValidationProvider>

                    <v-btn
                      dark
                      class="default-button mt-5"
                      type="submit"
                      tile
                      elevation="12"
                      block
                      >Login !!</v-btn
                    >
                  </form>
                   </ValidationObserver>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<script>
import { ValidationObserver, ValidationProvider } from "vee-validate";

export default {
  components: {
    ValidationObserver,
    ValidationProvider,
  },
  data() {
    return {
      form: {
        email: null,
        password: null,
      },
    };
  },
  methods: {
    async login() {
      await this.$auth
        .loginWith("local", { data: this.form })
        .then((res) => {
          if (res.data.success) {
            console.log(res.data.success);
            this.$swal({
              icon: "success",
              title: "sign in Successfully !!",
              toast: true,
              position: "top-right",
              showConfirmButton: false,
              timer: 3000,
              timerProgressBar: true,
            });
            this.$router.push("/dashboard");
          } else {
            this.$swal({
              icon: "error",
              title: res.data?.message,
              toast: true,
              position: "top-right",
              showConfirmButton: false,
              timer: 3000,
              timerProgressBar: true,
              didOpen: (toast) => {
                toast.addEventListener("mouseenter", this.$swal.stopTimer);
                toast.addEventListener("mouseleave", this.$swal.resumeTimer);
              },
            });
            }
        })
        .catch((error) => {
          this.$swal({
            icon: "error",
            title: error,
            toast: true,
            position: "top-right",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener("mouseenter", this.$swal.stopTimer);
              toast.addEventListener("mouseleave", this.$swal.resumeTimer);
            },
          });
        });
    },
  },
};
</script>
