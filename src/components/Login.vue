<template>
<v-card>
  <v-card-title style="font-size: 24px !important;">เข้าสู่ระบบ</v-card-title>
  <v-card-text>
  <v-form
    ref="loginform"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      :counter="20"
      :rules="nameRules"
      label="ชื่อผู้ใช้งาน"
      required
      outlined
    ></v-text-field>

    <v-text-field
      v-model="password"
      :rules="passwordRules"
      label="รหัสผ่าน"
      required
      outlined
    ></v-text-field>

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="Login()"
      block
    >
      เข้าสู่ระบบ
    </v-btn>

  </v-form>
  </v-card-text>
</v-card>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'กรุณากรอกชื่อผู้ใช้งาน',
      v => (v && v.length <= 20) || 'กรุณากรอกชื่อผู้ใช้งานห้ามเกิน 20 ตัวอักษร'
    ],
    password: '',
    passwordRules: [
      v => !!v || 'กรุณากรอกรหัสผ่าน'
    ]
  }),

  methods: {
    Login () {
      if (this.$refs.loginform.validate(true)) {
        localStorage.setItem('username', this.name)
        this.$EventBus.$emit('getUsername')
        this.$$router.push('/')
      }
    }
  }
}
</script>

<style>

</style>
