<template>
    <div>

        <h2>Finalisez votre commande</h2>
        <form method="POST" action="" @submit="confirmOrder">
            <div class="form">
               <div class="adress">
                   <h3>Addresse de livraison</h3>
                   <div class="name">
                       <div class="formField">
                           <label for="lastName"> Nom</label>
                           <input type="text" id="lastName" name="lastName" v-model="lastName" required>
                           <small v-if="errors.lastName" class="errorLastName">{{ errors.lastName }}</small>
                        </div>
                        <div class="formField">
                           <label for="firstName"> Prénom</label>
                           <input type="text" id="firstName" name="firstname" v-model="firstName" required>
                           <small v-if="errors.firstName" class="errorFirstName">{{ errors.firstName }}</small>
                        </div>
                   </div>
                   <div class="emailInfo formField">
                       <label for="email"> Email</label>
                       <input type="email" id="email" name="email" v-model="email" required>
                       <small v-if="errors.email" class="errorEmail">{{ errors.email }}</small>
                   </div>
                   <div class="adressInfo formField">
                       <label for="address"> Adresse</label>
                       <input type="text" id="address" name="address" v-model="address" required>
                       <small v-if="errors.address" class="errorAddress">{{ errors.address }}</small>
                   </div>
                   <div class="cityInfo">
                       <div class="formField">
                           <label for="city"> Ville</label>
                           <input type="text" id="city" name="city" v-model="city" required>
                           <small v-if="errors.city" class="errorCity">{{ errors.city }}</small>
                       </div>
                       <div class="formField">
                            <label for="zip">Code Postal</label>
                            <input type="text" id="zip" name="zip" v-model="zip" required>
                            <small v-if="errors.zip" class="errorZip">{{ errors.zip }}</small>
                       </div>
                   </div>
                </div>
                <div>
                    <input type="submit" value="Confimer ma commande" class="button">
                </div>
            </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "UserInformationComponent",

    data: () => {
        return {
            lastName: "",
            firstName: "",
            email: "",
            address: "",
            city: "",
            zip: "",
            errors: {}
        }
    },

    methods: {
        confirmOrder(e) {

            e.preventDefault();

            //initialisation tableau erreurs
            this.errors = {};

            let cartLocalStorage = JSON.parse(localStorage.getItem("cartItem"));
            let products = [];
            for (const product of cartLocalStorage) {
                products.push(product.id);
            }
            let contact;

            const wordValue = /[a-zA-Z-]/;
            const numberbValue = /[0-9]/
            const addressValue = /[a-zA-Z0-9\s]/;
            const emailValue = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]/;
            

            const checkFirstName = () => {
                if (wordValue.test(this.firstName) === false || !this.firstName || this.firstName.length > 20 || this.firstName.length < 2) {
                    this.errors.firstName = 'Votre prénom doit avoir entre 2 et 20 carctères et pas de chiffres !';
                }
            }

            const checkLastName = () => {
                if (wordValue.test(this.lastName) === false || !this.lastName || this.lastName.length > 20 || this.lastName.length < 2) {
                    this.errors.lastName = 'Votre nom doit avoir entre 2 et 20 carctères et pas de chiffres !';
                }
            }

            const checkEmail = () => {
                if (emailValue.test(this.email) === false || !this.email) {
                    this.errors.email = 'Vérifiez votre email !';
                }
            }

            const checkAddress = () => {
                if (addressValue.test(this.address) === false || !this.address) {
                    this.errors.address = 'Vérifier votre adresse !';
                }
            }

            const checkCity = () => {
                if (wordValue.test(this.city) === false || !this.city) {
                    this.errors.city = 'Vérifier votre adresse !';
                }
            }

            const checkZip = () => {
                if (numberbValue.test(this.zip) === false || !this.zip || this.zip.length < 5 || this.zip.length > 5) {
                    this.errors.zip = 'Il doit y avoir 5 chiffres !';
                }
            }

            let isFirstNameValid = checkFirstName(),
                isLastNameValid = checkLastName(),
                isEmailValid = checkEmail(),
                isAddressValid = checkAddress(),
                isCityValid = checkCity(),
                isZipValid = checkZip();

            let isFormValid = isFirstNameValid && isLastNameValid &&
             isEmailValid && isAddressValid && isCityValid && isZipValid;

            if (!isFormValid) {
                contact = {
                    firstName: this.firstName,
                    lastName: this.lastName,
                    email: this.email,
                    address: this.address,
                    city: this.city,
                    zip: this.zip
                };
            } else {
                console.log('ERREUR PFFF !')
            }
            
            localStorage.setItem('contact', JSON.stringify(contact));

            // 
            // +"?orderId=" + response.orderId  rien
            // + response.orderId   undefined

            axios.post("http://localhost:3000/api/furniture/order", 
                    {
                        contact: contact,
                        products: products
                    },{
                        headers: {'Content-Type':'application/json;charset=UTF-8'}
                    }
            )
            .then((response) => {
                const orderId = response.data.orderId;
                this.$router.replace({
                    name: 'Order-Confirmation', params: { orderId: orderId }
                });
            })
            .catch((error) => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
form {
    width: 50%;
    margin: 30px auto;
    padding: 30px;
    background-color: rgba(175, 125, 95, 0.959);
}

div {
    margin: 15px 0;
}

.name, .cityInfo, .cardInfo, .cardInfoDate {
    display: flex;
    justify-content: space-between;
}

.name div, .cityInfo div,.cardInfo div, .cardInfoDate div {
    width: 40%;
}

input {
    width: 100%;
    min-height: 25px;
    border: 0;
    font-size: 1rem;
    letter-spacing: .15rem;
    margin-top: 5px;
    border-radius: 4px;
}

label {
    text-transform: uppercase;
    font-size: 12px;
    letter-spacing: 2px;

}

i {
    margin-right: 10px;
}

.button {
    margin: 10px 0;
    height: 40px;
    color: #cfc9e1;
    background-color: #4a3b76;
    text-transform: uppercase;
    border: 0;
    border-radius: .3rem;
    letter-spacing: 2px;
}

@media (max-width: 736px) {

    .name, .cityInfo, .cardInfo, .cardInfoDate {
    flex-direction: column;
    }

    .name div, .cityInfo div,.cardInfo div, .cardInfoDate div, button {
    width: 100%;
    }
    
}
</style>