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

               <div class="paiement">
                   <h3>Mode de paiement</h3>
                   <label for="fname">Carte acceptée</label>
                   <div class="icon-container">
                       <i class="fa fa-cc-visa" style="color:navy;"></i>
                       <i class="fa fa-cc-amex" style="color:blue;"></i>
                       <i class="fa fa-cc-mastercard" style="color:red;"></i>
                       <i class="fa fa-cc-discover" style="color:orange;"></i>
                    </div>
                    <div class="cardInfo">
                        <div class="formField">
                            <label for="cardName">Détenteur de la carte</label>
                            <input type="text" id="cardName" name="cardName" v-model="cardName" required>
                            <small v-if="errors.cardName" class="errorCardName">{{ errors.cardName }}</small>
                        </div>
                        <div class="formField">
                            <label for="cardNumber">Credit card number</label>
                            <input type="text" id="cardNumber" name="cardNumber" v-model="cardNumber" required>
                            <small v-if="errors.cardNumber" class="errorCardNumber">{{ errors.cardNumber }}</small>
                        </div>
                    </div>

                    <div class="cardInfoDate">
                        <div class="formField">
                            <label for="expirationDate">Date d'expiration</label>
                            <input type="text" id="expirationDate" name="expirationDate" v-model="expirationDate" required>
                            <small v-if="errors.expirationDate" class="errorExpirationDate">{{ errors.expirationDate }}</small>
                        </div>
                        <div class="formField">
                            <label for="cvv">CVV</label>
                            <input type="text" id="cvv" name="cvv" v-model="cvv" required>
                            <small v-if="errors.cvv" class="errorCvv">{{ errors.cvv }}</small>
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
            cardName: "",
            cardNumber: "",
            expirationDate: "",
            cvv: "",
            errors: {}
        }
    },

    methods: {
        confirmOrder(e) {

            e.preventDefault();

            //initialisation tableau erreurs
            this.errors = {};

            let cartLocalStorage = JSON.parse(localStorage.getItem("cartItem"));
            let products = cartLocalStorage;
            let contact;

            const wordValue = /[a-zA-Z-]/;
            const numberbValue = /[0-9]/
            const addressValue = /[a-zA-Z0-9\s]/;
            //const caractValue = /[!$%§^&*@(),.?":#{}|<>]/;
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

            const checkCardName = () => {
                if (this.cardName !== this.firstName || !this.cardName || this.cardName.length > 20 || this.cardName.length < 2) {
                    this.errors.cardName = 'L\'acheteur et le propriétaire de la carte doivent être identique !';
                }
            }

            const checkCardNumber = () => {
                if (numberbValue.test(this.cardNumber) === false || !this.cardNumber || this.cardNumber.length > 16 || this.cardNumber.length < 16) {
                    this.errors.cardNumber = 'Notez les 16 chiffres de la carte !';
                }
            }

            const checkExpirationDate = () => {
                if (numberbValue.test(this.expirationDate) === false || !this.expirationDate) {
                    this.errors.expirationDate = 'Vérifier l\'expiration de votre carte !';
                }
            }

            const checkCvv = () => {
                if (numberbValue.test(this.cvv) === false || !this.cvv || this.cvv.length > 3 || this.cvv.length < 3) {
                    this.errors.cvv = 'Vérifier le cvv au dos de votre carte !';
                }
            }

            let isFirstNameValid = checkFirstName(),
                isLastNameValid = checkLastName(),
                isEmailValid = checkEmail(),
                isAddressValid = checkAddress(),
                isCityValid = checkCity(),
                isZipValid = checkZip(),
                isCardNameValid = checkCardName(),
                isCardNumberValid = checkCardNumber(),
                isExpirationDateValid = checkExpirationDate(),
                isCvvValid = checkCvv();

            let isFormValid = isFirstNameValid && isLastNameValid &&
             isEmailValid && isAddressValid && isCityValid && isZipValid &&
             isCardNameValid && isCardNumberValid && isExpirationDateValid && isCvvValid ;

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

            console.log(products);
            
            localStorage.setItem('contact', JSON.stringify(contact));
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