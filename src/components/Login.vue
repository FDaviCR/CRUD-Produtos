<template>
    <div class="container">
        <div id="erro">
            <p v-show="error">{{ erro }}</p>
        </div>
        <div class="field">
        <p class="control has-icons-left has-icons-right">
            <input id="username" class="input" type="username" placeholder="Username" v-model="username">
            <span class="icon is-small is-left">
                <i class="fas fa-envelope"></i>
            </span>
            <span class="icon is-small is-right">
                <i class="fas fa-check"></i>
            </span>
        </p>
        </div>
        <div class="field">
        <p class="control has-icons-left">
            <input id="password" class="input" type="password" placeholder="Password" v-model="password">
            <span class="icon is-small is-left">
                <i class="fas fa-lock"></i>
            </span>
        </p>
        </div>
        <div class="field">
        <p class="control">
            <button class="button is-black" @click="login">
                Login
            </button>
        </p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

var axiosConfig = {
        headers: {
            Authorization: 'Bearer ' + localStorage.getItem('token')
        }
    }

export default {
    data(){
        return{
            error: false,
            erro: '',
            username: '',
            password: ''
        }
    },
    methods:{
        login: function(){
            var login = this.username;
            var password = this.password;

            console.log(login+' '+password);

            axios.post("http://localhost:3000/users",{
                login,
                password
            }).then(res => {
                localStorage.setItem("token", res.data.token);
                axiosConfig.headers.Authorization = "Bearer " + localStorage.getItem("token");
                this.error = false;
                console.log("Logou");
            }).catch(err => {
                this.error = true;

                if(err == 'Error: Request failed with status code 401') {
                    this.erro = "Senha inválida!";
                }else if(err == 'Error: Request failed with status code 404') {
                    this.erro = "Usuário desconhecido!";
                }else{
                    this.erro = "Erro desconhecido" ;
                }
            });
        }
    }
}
</script>

<style scoped>
    input{
        width:33%;
        min-width: 300px;
    }

    #erro{
        background-color: red;
        margin-top: 10px;
        margin-bottom: 10px;
        text-align: center;        
    }
</style>