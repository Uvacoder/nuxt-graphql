<template>
  <v-app dark>
    <v-navigation-drawer v-model="drawer" fixed temporary app>
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" router exact>
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar fixed dense app flat clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"/>
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click="openRightDrawer('search')">
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-menu left bottom>
        <template #activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item @click="openRightDrawer('login')">
            <v-list-item-title>Login</v-list-item-title>
          </v-list-item>
          <v-list-item @click="openRightDrawer('register')">
            <v-list-item-title>Register</v-list-item-title>
          </v-list-item>
          <v-list-item @click="openRightDrawer('account')">
            <v-list-item-title>Account</v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title>Logout</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <Nuxt/>
    <v-navigation-drawer v-model="rightDrawer" width="340" right temporary fixed>
      <Login v-if="type === 'login'" class-props="row align-center justify-center fill-height pa-1">
        <template #login-links>
          <v-col cols="12" class="py-0">
            <v-btn small rounded text block class="my-2 text-capitalize" @click="type = 'forget-password'">
              Forgot Password?
            </v-btn>
            <v-btn small rounded block depressed color="primary" @click="type = 'register'">
              Sign Up
            </v-btn>
          </v-col>
        </template>
      </Login>
      <Register v-if="type === 'register'" class-props="row align-center justify-center fill-height pa-1">
        <template #register-links>
          <v-col cols="12" class="py-2">
            <v-btn small rounded text block depressed class="text-capitalize" @click="type = 'login'">
              Have an account? Login now
            </v-btn>
          </v-col>
        </template>
      </Register>
      <ForgetPassword v-if="type === 'forget-password'" class-props="row align-center justify-center fill-height pa-1" @reset-password-event="type = $event">
        <template #forget-password-form>
          <v-col cols="12" class="py-2">
            <v-btn small rounded text block depressed class="text-capitalize" @click="type = 'login'">
              Return to login
            </v-btn>
          </v-col>
        </template>
      </ForgetPassword>
      <ResetPassword v-if="type === 'reset-password'" class-props="row align-center justify-center fill-height pa-1"/>
      <Account v-if="type === 'account'"/>
      <Search v-if="type === 'search'"/>
    </v-navigation-drawer>
    <v-footer absolute app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import ErrorComponent from "~/components/Common/Error"
import LoadingComponent from "~/components/Common/Loading"

const Login = () => ({
  component: import("~/components/Common/Login"),
  loading: LoadingComponent,
  error: ErrorComponent,
  timeout: 3000
})
const Register = () => ({
  component: import("~/components/Common/Register"),
  loading: LoadingComponent,
  error: ErrorComponent,
  timeout: 3000
})
const ForgetPassword = () => ({
  component: import("~/components/Common/ForgetPassword"),
  loading: LoadingComponent,
  error: ErrorComponent,
  timeout: 3000
})
const ResetPassword = () => ({
  component: import("~/components/Common/ResetPassword"),
  loading: LoadingComponent,
  error: ErrorComponent,
  timeout: 3000
})
const Search = () => ({
  component: import("~/components/Common/Search"),
  loading: LoadingComponent,
  error: ErrorComponent,
  timeout: 3000
})
const Account = () => ({
  component: import("~/components/Common/Account"),
  loading: LoadingComponent,
  error: ErrorComponent,
  timeout: 3000
})
export default {
  components: {
    Login,
    Register,
    ForgetPassword,
    ResetPassword,
    Search,
    Account
  },
  data() {
    return {
      type: 'search',
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        }
      ],
      rightDrawer: false,
      title: 'Perfect Pixels'
    }
  },
  methods: {
    openRightDrawer(type) {
      this.type = (this.rightDrawer === true) ? 'search' : type
      this.rightDrawer = !this.rightDrawer
    }
  }
}
</script>
