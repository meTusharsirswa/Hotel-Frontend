<template>
  <section>
    <v-container>
      <v-row align="center" justify="center" class="mt-12"></v-row>
      <v-col cols="12" sm="6" md="12">
        <v-card flat class="my-13 mx-auto" width="50%">
          <v-card-text>
            <h3>Sign Up Your Account</h3>
            <v-row>
              <v-col cols="12">
                <ValidationObserver
                  ref="file-details-form"
                  v-slot="{ handleSubmit }"
                >
                  <form @submit.prevent="handleSubmit(register)">
                    <v-row>
                      <v-col cols="12" sm="6">
                        <ValidationProvider
                          name="First Name"
                          rules="required"
                          v-slot="{ errors }"
                        >
                          <v-text-field
                            v-model="model.first_name"
                            label="First Name"
                            outlined
                            autocomplete="false"
                            class="mt-4"
                            :error-messages="errors"
                            :hide-details="!errors.length"
                          ></v-text-field>
                        </ValidationProvider>
                      </v-col>

                      <v-col cols="12" sm="6">
                        <ValidationProvider
                          name="Last Name"
                          rules="required"
                          v-slot="{ errors }"
                        >
                          <v-text-field
                            v-model="model.last_name"
                            label="Last Name"
                            outlined
                            autocomplete="false"
                            class="mt-4"
                            :error-messages="errors"
                            :hide-details="!errors.length"
                          ></v-text-field>
                        </ValidationProvider>
                      </v-col>

                      <v-col cols="12">
                        <ValidationProvider
                          name="Email"
                          rules="required"
                          v-slot="{ errors }"
                        >
                          <v-text-field
                            v-model="model.email"
                            label="Email"
                            type="email"
                            outlined
                            autocomplete="false"
                            :error-messages="errors"
                            :hide-details="!errors.length"
                          ></v-text-field>
                        </ValidationProvider>
                      </v-col>
                      <v-col cols="12">
                        <ValidationProvider
                          name="Password"
                          rules="required"
                          v-slot="{ errors }"
                        >
                          <v-text-field
                            v-model="model.password"
                            label="Password"
                            outlined
                            autocomplete="false"
                            type="password"
                            :error-messages="errors"
                            :hide-details="!errors.length"
                          ></v-text-field>
                        </ValidationProvider>
                      </v-col>
                    </v-row>
                    <v-btn
                      type="submit"
                      class="default-button mt-8"
                      dark
                      block
                      tile
                    >
                      Sign Up
                    </v-btn>
                  </form>
                </ValidationObserver>
              </v-col>
            </v-row>
          </v-card-text>
        </v-card>
      </v-col>
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
      model: {
        first_name: null,
        last_name: null,
        email: null,
        password: null,
      },
    };
  },
  methods: {
    async register() {
      try {
        // Attempt to register the user
        await this.$axios.$post("/register", this.model);

        // Attempt to login the user
        const res = await this.$auth.loginWith("local", {
          data: {
            email: this.model.email,
            password: this.model.password,
          },
        });

        if (res.data.success) {
          console.log(res.data.message)
          console.log(res)
          this.$swal({
            icon: "success",
            title: res.data.message,
            toast: true,
            position: "top-right",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
          });
          this.$router.push("/dashboard");
        }else if(!(res.data.success)){
          console.log(res)
          console.log(res.data.message)
          this.$swal({
            icon: "error",
            title: res.data?.message,
            toast: true,
            position: "top-right",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
          });
        }
        else{
          alert("else is run ")
        }
      } catch (err) {
        this.$swal({
          icon: "error",
          text: err.res.message,
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
    },
  },
};
</script>
