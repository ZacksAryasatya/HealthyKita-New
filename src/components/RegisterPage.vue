<template>
    <div class="d-flex justify-content-center align-items-center vh-100" style="background-color: #f4fdf4; font-family: monospace;">
        <div class="card shadow-sm" style="width: 24rem; border-radius: 50px;">
            <div class="card-body" >
                <h3 class="card-title text-center mb-4" style="font-family: sans-serif; font-weight: 545;">Register</h3>
                <div class="mb-3">
                    <label for="name" class="form-label">Nama Lengkap</label>
                    <input type="text" id="name" class="form-control" name="username" placeholder="Masukkan nama mu" v-model="userData.username"
                        required>
                </div>
                <div class="mb-3">
                    <label for="email" class="form-label">Alamat Email</label>
                    <input type="email" id="email" class="form-control"
                        placeholder="emailmu@example.com" name="email" v-model="userData.email" required>
                </div>
                <div class="mb-3">
                    <label for="password" class="form-label">Password</label>
                    <input type="password" id="password" class="form-control"
                        placeholder="Masukkan Password" name="password" v-model="userData.password" required>
                </div>
                <div class="mb-3">
                    <label for="confirmPassword" class="form-label">Konfirmasi Password</label>
                    <input type="password" id="confirmPassword" class="form-control"
                        placeholder="Konfirmasi Password" name="confirmpw" v-model="userData.confirmpw" required>
                </div>
                <button type="submit" class="btn btn-success w-100 animate" @click="registerData" :disabled="loading">Register</button>
                <div class="text-center mt-3">
                    <!-- Ikon Google -->
                    <div class="text-center">
                        <a href="#" class="social-icon"><i class="fa-brands fa-google"></i></a>
                    </div>
                    <!-- Login -->
                    <p id="login1">Sudah punya akun? </p><router-link to="/login"
                        class="text-success text-decoration-none" id="login">Login disini</router-link>
                </div>
            </div>
            <div v-if="loading" class="text-center">
                <p>harap tunggu...</p>
            </div>
            <h3 class="text-center" v-if="success && !loading">{{ response.message }}</h3>
            <h3 class="text-center" v-if="error && !loading">{{ response.message }}</h3>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import textFile from '!!raw-loader!./file.txt';
export default {
    name: 'RegisterPage',
    data() {
        return {
            arr: textFile,
            userData: {
                username: "",
                email: "",
                password: "",
                confirmpw: ""
            },
            success: false,
            error: false,
            loading: false,
            response: {}
        };
    },
    methods: {
        registerData() {
            this.success = false;
            this.error = false;
            this.loading = true;  // Start loading
            const { username, email, password, confirmpw } = this.userData;
            if (!username || !password || !email || !confirmpw){
                alert("Please fill out all required fields.");
                this.loading = false;  // Stop loading if validation fails
                return;
            }
            if (password !== confirmpw) {
                alert("Passwords do not match.");
                this.loading = false;  // Stop loading if passwords don't match
                return;
            }
            axios.post(`${this.arr}/api/signup/user`, {
                username: username,
                email: email,
                password: password,  
            },{withCredentials:true
})
            
            .then(async (response) => {
                this.success = true;
                this.response = response.data;
                this.userData = {
                    username: "",
                    email: "",
                    password: "",
                    confirmpw: ""
                };
                this.loading = false;  // Stop loading when request is successful
            })
            .catch((error) => {
                console.log(error);
                this.error = true;
                this.loading = false;  // Stop loading if there's an error
            });   
        }
    },
}
</script>

<style scoped>
#login1 {
    color: black;
    text-decoration: none;
    font-size: 14px;
    margin-top: 5px;
    display: inline-block;
    margin-bottom: 10px;
    margin-left: 2px;
    margin-right: 5px;
}

#login {
    font-size: 14px;
    display: inline-block;
    transition: color 0.3s ease-in-out;
    margin-bottom: 10px;
}

#login:hover {
    color: #357ab8;
}

.animate {
    transition: all 0.3s ease;
}

.animate:hover {
    transform: scale(1.05);
}

.animate:active {
    transform: scale(0.95);
}
</style>
