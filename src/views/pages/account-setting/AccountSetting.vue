<template>
  <b-tabs
    vertical
    content-class="col-12 col-md-9 mt-1 mt-md-0"
    pills
    nav-wrapper-class="col-md-3 col-12"
    nav-class="nav-left"
  >
    <b-tab active>
      <template #title>
        <feather-icon
          icon="UserIcon"
          size="18"
          class="mr-50"
        />
        <span class="font-weight-bold"> {{ $t('my_profile_page.general') }} </span>
      </template>
      <account-setting-general
        v-if="options.general"
        :general-data="options.general"
      />
    </b-tab>
    <b-tab>
      <template #title>
        <feather-icon
          icon="LockIcon"
          size="18"
          class="mr-50"
        />
        <span class="font-weight-bold">{{ $t('my_profile_page.change_password') }}</span>
      </template>
      <account-setting-password/>
    </b-tab>
    <b-tab>
      <template #title>
        <feather-icon
          icon="PackageIcon"
          size="18"
          class="mr-50"
        />
        <span class="font-weight-bold">{{ $t('my_profile_page.current_plan') }}</span>
      </template>
      <AccountCurrentPlan />
    </b-tab>
    <!--/ change password tab -->

    <!-- info -->
<!--    <b-tab>-->

<!--      &lt;!&ndash; title &ndash;&gt;-->
<!--      <template #title>-->
<!--        <feather-icon-->
<!--            icon="InfoIcon"-->
<!--            size="18"-->
<!--            class="mr-50"-->
<!--        />-->
<!--        <span class="font-weight-bold">Information</span>-->
<!--      </template>-->

<!--      <account-setting-information-->
<!--          v-if="options.info"-->
<!--          :information-data="options.info"-->
<!--      />-->
<!--    </b-tab>-->

    <!-- social links -->
<!--    <b-tab>-->

<!--      &lt;!&ndash; title &ndash;&gt;-->
<!--      <template #title>-->
<!--        <feather-icon-->
<!--            icon="LinkIcon"-->
<!--            size="18"-->
<!--            class="mr-50"-->
<!--        />-->
<!--        <span class="font-weight-bold">Social</span>-->
<!--      </template>-->

<!--      <account-setting-social-->
<!--          v-if="options.social"-->
<!--          :social-data="options.social"-->
<!--      />-->
<!--    </b-tab>-->

    <!-- notification -->
<!--    <b-tab>-->

<!--      &lt;!&ndash; title &ndash;&gt;-->
<!--      <template #title>-->
<!--        <feather-icon-->
<!--            icon="BellIcon"-->
<!--            size="18"-->
<!--            class="mr-50"-->
<!--        />-->
<!--        <span class="font-weight-bold">Notifications</span>-->
<!--      </template>-->

<!--      <account-setting-notification-->
<!--          v-if="options.notification"-->
<!--          :notification-data="options.notification"-->
<!--      />-->
<!--    </b-tab>-->
  </b-tabs>
</template>

<script>
import { BTabs, BTab } from 'bootstrap-vue'
import AccountSettingGeneral from './AccountSettingGeneral.vue'
import AccountSettingPassword from './AccountSettingPassword.vue'
import AccountCurrentPlan from '@/views/pages/account-setting/AccountCurrentPlan.vue'
// import AccountSettingInformation from './AccountSettingInformation.vue'
// import AccountSettingSocial from './AccountSettingSocial.vue'
// import AccountSettingNotification from './AccountSettingNotification.vue'

export default {
  components: {
    BTabs,
    BTab,
    AccountSettingGeneral,
    AccountSettingPassword,
    AccountCurrentPlan,
    // AccountSettingInformation,
    // AccountSettingSocial,
    // AccountSettingNotification,
  },
  data() {
    return {
      options: {
        general: {
          // eslint-disable-next-line global-require
          avatar: require('@/assets/images/portrait/small/avatar-s-11.jpg'),
          username: 'johndoe',
          fullName: 'John Doe',
          email: 'granger007@hogward.com',
          company: 'Crystal Technologies',
        },
        info: {
          bio: '',
          dob: null,
          country: 'USA',
          website: '',
          phone: 6562542568,
        },
        social: {
          socialLinks: {
            twitter: 'https://www.twitter.com',
            facebook: '',
            google: '',
            linkedIn: 'https://www.linkedin.com',
            instagram: '',
            quora: '',
          },
          connections: {
            twitter: {
              // eslint-disable-next-line global-require
              profileImg: require('@/assets/images/avatars/11-small.png'),
              id: 'johndoe',
            },
            google: {
              // eslint-disable-next-line global-require
              profileImg: require('@/assets/images/avatars/3-small.png'),
              id: 'luraweber',
            },
            facebook: {},
            github: {},
          },
        },
        notification: {
          commentOnArticle: true,
          AnswerOnForm: true,
          followMe: false,
          newAnnouncements: true,
          productUpdates: true,
          blogDigest: false,
        },
      },
    }
  },
  beforeCreate() {
    // this.$http.get('/account-setting/data').then(res => { this.options = res.data })
  },
}
</script>
