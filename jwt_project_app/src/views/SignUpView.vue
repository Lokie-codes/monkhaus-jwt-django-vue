<template>
    <div class="signup-page"></div>
    <h1>Sign Up</h1>
    <form @submit.prevent="submitForm">
        <label for="username">Username</label>
        <input type="email" name="username" v-model="username"> <br><br>
        <label for="password">Password</label>
        <input type="password" name="password" v-model="password"> <br><br>
        <button type="submit">Sign Up</button>
    </form>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Signup',
    data() {
        return {
            username : '',
            password : ''
        }
    },
    methods: {
        submitForm(e) {
            const formData = {
                username: this.username,
                password: this.password,
            }

            axios
                .post('/api/v1/users/', formData)
                .then(response => {
                    console.log(response)
                    this.$router.push('/')
                })
                .catch(error => {
                    console.log(error)
                })
        }
    }
}
</script>