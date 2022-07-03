<template>
    <div class="login-page"></div>
    <h1>Log in</h1>
    <form @submit.prevent="submitForm">
        <label for="username">Username</label>
        <input type="email" name="username" v-model="username"> <br><br>
        <label for="password">Password</label>
        <input type="password" name="password" v-model="password"> <br><br>
        <button type="submit">Login</button>
    </form>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Login',
    data() {
        return {
            username : '',
            password : ''
        }
    },
    methods: {
        submitForm(e) {
            axios.defaults.headers.common['Authorization'] = ''
            localStorage.removeItem("access")

            const formData = {
                username: this.username,
                password: this.password,
            }

            axios
                .post('/api/v1/jwt/create/', formData)
                .then(response => {
                    console.log(response)
                    const access = response.data.access
                    this.$store.commit('setAccess', access)
                    axios.defaults.headers.common['Authorization'] = "JWT" + access
                    localStorage.setItem("access", access)

                    this.$router.push('/')
                })
                .catch(error => {
                    console.log(error)
                })
        }
    }
}
</script>