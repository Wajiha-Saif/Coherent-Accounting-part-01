<template>
  <b-card>
    <validation-observer ref="simpleRules">
      <!-- form -->
      <b-form @submit.prevent="validationForm()">
        <b-row>
          <!-- old password -->
          <b-col cols="6">
            <b-form-group :label='$t("change_password.old_password")' label-for="old-password">
              <validation-provider
                #default="{ errors }"
                name="Password"
                vid="Password"
                rules="required"
              >
                <b-form-input
                  id="old-password"
                  v-model="passwordValueOld"
                  :state="errors.length > 0 ? false : null"
                  :type="passwordFieldTypeOld"
                  :placeholder='$t("change_password.old_password")'
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>
          <!--          <b-col md="6">-->
          <!--            <b-form-group-->
          <!--                label="Old Password"-->
          <!--                label-for="account-old-password"-->
          <!--            >-->
          <!--              <b-input-group class="input-group-merge">-->
          <!--                <b-form-input-->
          <!--                    id="account-old-password"-->
          <!--                    v-model="passwordValueOld"-->
          <!--                    name="old-password"-->
          <!--                    :type="passwordFieldTypeOld"-->
          <!--                    placeholder="Old Password"-->
          <!--                />-->
          <!--                <b-input-group-append is-text>-->
          <!--                  <feather-icon-->
          <!--                      :icon="passwordToggleIconOld"-->
          <!--                      class="cursor-pointer"-->
          <!--                      @click="togglePasswordOld"-->
          <!--                  />-->
          <!--                </b-input-group-append>-->
          <!--              </b-input-group>-->
          <!--            </b-form-group>-->
          <!--          </b-col>-->
          <!--/ old password -->
        </b-row>
        <b-row>
          <!-- new password -->
          <!--        <b-col md="6">-->
          <!--          <b-form-group-->
          <!--            label-for="account-new-password"-->
          <!--            label="New Password"-->
          <!--          >-->
          <!--            <b-input-group class="input-group-merge">-->
          <!--              <b-form-input-->
          <!--                id="account-new-password"-->
          <!--                v-model="newPasswordValue"-->
          <!--                :type="passwordFieldTypeNew"-->
          <!--                name="new-password"-->
          <!--                placeholder="New Password"-->
          <!--              />-->
          <!--              <b-input-group-append is-text>-->
          <!--                <feather-icon-->
          <!--                  :icon="passwordToggleIconNew"-->
          <!--                  class="cursor-pointer"-->
          <!--                  @click="togglePasswordNew"-->
          <!--                />-->
          <!--              </b-input-group-append>-->
          <!--            </b-input-group>-->
          <!--          </b-form-group>-->
          <!--        </b-col>-->
          <!--/ new password -->

          <!-- retype password -->
          <!--        <b-col md="6">-->
          <!--          <b-form-group-->
          <!--            label-for="account-retype-new-password"-->
          <!--            label="Retype New Password"-->
          <!--          >-->
          <!--            <b-input-group class="input-group-merge">-->
          <!--              <b-form-input-->
          <!--                id="account-retype-new-password"-->
          <!--                v-model="RetypePassword"-->
          <!--                :type="passwordFieldTypeRetype"-->
          <!--                name="retype-password"-->
          <!--                placeholder="New Password"-->
          <!--              />-->
          <!--              <b-input-group-append is-text>-->
          <!--                <feather-icon-->
          <!--                  :icon="passwordToggleIconRetype"-->
          <!--                  class="cursor-pointer"-->
          <!--                  @click="togglePasswordRetype"-->
          <!--                />-->
          <!--              </b-input-group-append>-->
          <!--            </b-input-group>-->
          <!--          </b-form-group>-->
          <!--        </b-col>-->
          <!--/ retype password -->

          <!-- new password -->
          <b-col cols="6">
            <b-form-group :label='$t("change_password.new_password")' label-for="new-password">
              <validation-provider
                #default="{ errors }"
                name="New Password"
                vid="newPassword"
                rules="required"
              >
                <b-form-input
                  id="new-password"
                  v-model="newPasswordValue"
                  :state="errors.length > 0 ? false : null"
                  :type="passwordFieldTypeNew"
                  :placeholder='$t("change_password.new_password")'
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>

          <!-- confirm password -->
          <b-col cols="6">
            <b-form-group :label='$t("change_password.confirm_new_password")' label-for="ac-password">
              <validation-provider
                #default="{ errors }"
                name="Confirm New Password"
                rules="required|confirmed:newPassword"
              >
                <b-form-input
                  id="ac-password"
                  v-model="RetypePassword"
                  :state="errors.length > 0 ? false : null"
                  :type="passwordFieldTypeRetype"
                  :placeholder='$t("change_password.new_password")'
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>

          <!-- buttons -->
          <b-col cols="12">
            <b-button
              v-ripple.400="'rgba(255, 255, 255, 0.15)'"
              variant="primary"
              class="mt-1 mr-1"
              type="submit"
            >
            {{ $t("change_password.save_changes") }}
            </b-button>
          </b-col>
          <!--/ buttons -->
        </b-row>
      </b-form>
    </validation-observer>
  </b-card>
</template>

<script>
import ToastificationContent from "@core/components/toastification/ToastificationContent.vue";
import {
  BButton,
  BForm,
  BFormGroup,
  BFormInput,
  BRow,
  BCol,
  BCard,
  BInputGroup,
  BInputGroupAppend,
} from "bootstrap-vue";
import Ripple from "vue-ripple-directive";
import { extend, ValidationProvider, ValidationObserver } from "vee-validate";
import { required, min, confirmed } from "vee-validate/dist/rules";
import axios from "@/libs/axios";
import useJwt from "@/auth/jwt/useJwt";

extend("required", required);
extend("min", min);
extend("confirmed", confirmed);

export default {
  components: {
    ValidationProvider,
    ValidationObserver,
    BButton,
    BForm,
    BFormGroup,
    BFormInput,
    BRow,
    BCol,
    BCard,
    // eslint-disable-next-line vue/no-unused-components
    BInputGroup,
    // eslint-disable-next-line vue/no-unused-components
    BInputGroupAppend,
  },
  directives: {
    Ripple,
  },
  data() {
    return {
      passwordValueOld: "",
      newPasswordValue: "",
      RetypePassword: "",
      passwordFieldTypeOld: "password",
      passwordFieldTypeNew: "password",
      passwordFieldTypeRetype: "password",
    };
  },
  computed: {
    passwordToggleIconOld() {
      return this.passwordFieldTypeOld === "password"
        ? "EyeIcon"
        : "EyeOffIcon";
    },
    passwordToggleIconNew() {
      return this.passwordFieldTypeNew === "password"
        ? "EyeIcon"
        : "EyeOffIcon";
    },
    passwordToggleIconRetype() {
      return this.passwordFieldTypeRetype === "password"
        ? "EyeIcon"
        : "EyeOffIcon";
    },
  },
  // watch: {
  //   newPasswordValue(newV, oldV) {
  //   },
  //   RetypePassword(newV, oldV) {
  //   },
  // },
  methods: {
    togglePasswordOld() {
      this.passwordFieldTypeOld =
        this.passwordFieldTypeOld === "password" ? "text" : "password";
    },
    togglePasswordNew() {
      this.passwordFieldTypeNew =
        this.passwordFieldTypeNew === "password" ? "text" : "password";
    },
    togglePasswordRetype() {
      this.passwordFieldTypeRetype =
        this.passwordFieldTypeRetype === "password" ? "text" : "password";
    },
    validationForm() {
      this.$refs.simpleRules.validate().then((success) => {
        if (success) {
          // eslint-disable-next-line
          this.updatePassword();
        }
      });
    },
    //update password
    async updatePassword() {
      const credentials = {
        oldPassword: this.passwordValueOld,
        newPassword: this.newPasswordValue,
      };

      let token = useJwt.getToken();
      await useJwt
        .wrongOldPassword(token, credentials)
        .then((response) => {
          if (response.status === 200) {
            this.$toast({
              component: ToastificationContent,
              props: {
                title: "Password updated successfully ",
                icon: "DeleteIcon",
                variant: "success",
              },
            });
          }
        })
        .catch((error) => {
          this.$toast({
            component: ToastificationContent,
            props: {
              title: `Incorrect old password `,
              icon: "AlertTriangleIcon",
              variant: "danger",
            },
          });
        });

    },
    makeToast(variant = null, title = null, message = null) {
      this.$bvToast.toast(message, {
        title,
        variant,
        solid: false,
      });
    },
  },
};
</script>
