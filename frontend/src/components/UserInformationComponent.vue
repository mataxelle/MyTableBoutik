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
                           <small class="errorLastName"></small>
                        </div>
                        <div class="formField">
                           <label for="firstName"> Prénom</label>
                           <input type="text" id="firstName" name="firstname" v-model="firstName" required>
                           <small class="errorFirstName"></small>
                        </div>
                   </div>
                   <div class="emailInfo formField">
                       <label for="email"> Email</label>
                       <input type="email" id="email" name="email" v-model="email" required>
                       <small class="errorEmail"></small>
                   </div>
                   <div class="adressInfo formField">
                       <label for="address"> Adresse</label>
                       <input type="text" id="address" name="address" v-model="address" required>
                       <small class="errorAddress"></small>
                   </div>
                   <div class="cityInfo">
                       <div class="formField">
                           <label for="city"> Ville</label>
                           <input type="text" id="city" name="city" v-model="city" required>
                           <small class="errorCity"></small>
                       </div>
                       <div class="formField">
                            <label for="zip">Code Postal</label>
                            <input type="text" id="zip" name="zip" v-model="zip" required>
                            <small class="errorZip"></small>
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
                            <small class="errorCardName"></small>
                        </div>
                        <div class="formField">
                            <label for="cardNumber">Credit card number</label>
                            <input type="text" id="cardNumber" name="cardnumber" v-model="cardNumber" required>
                            <small class="errorCardNumber"></small>
                        </div>
                    </div>

                    <div class="cardInfoDate">
                        <div class="formField">
                            <label for="expirationDate">Date d'expiration</label>
                            <input type="text" id="expirationDate" name="expirationDate" v-model="expirationDate" required>
                            <small class="errorExpirationDate"></small>
                        </div>
                        <div class="formField">
                            <label for="cvv">CVV</label>
                            <input type="text" id="cvv" name="cvv" v-model="cvv" required>
                            <small class="errorCvv"></small>
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
            cvv: ""
        }
    },

    methods: {
        confirmOrder(e) {

            e.preventDefault();

            /*const firstName = document.getElementById('firstName').value;
            const lastName = document.getElementById('lastName').value;
            const email = document.getElementById('email').value;
            const address = document.getElementById('address').value;
            const city = document.getElementById('city').value;
            const zip = document.getElementById('zip').value;
            const cardName = document.getElementById('cardName').value;
            const cardNumber = document.getElementById('cardNumber').value;
            const expirationDate = document.getElementById('expirationDate').value;
            const cvv = document.getElementById('cvv').value;*/

            const wordValue = /[a-zA-Z-]/;
            const numberbValue = /[0-9]/
            const addressValue = /[a-zA-Z0-9\s]/;
            //const caractValue = /[!$%§^&*@(),.?":#{}|<>]/;
            const emailValue = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]/;

            if (wordValue.test(this.firstName) == false || !this.firstName || this.firstName.length > 20 || this.firstName.length < 2) {
                document.querySelector('.errorFirstName').textContent = 'Votre prénom doit avoir entre 2 et 20 carctères et pas de chiffres !';
                return false;
            }

            if (wordValue.test(this.lastName) == false || !this.lastName || this.lastName.length > 20 || this.lastName.length < 2) {
                document.querySelector('.errorLastName').textContent = 'Votre nom doit avoir entre 2 et 20 carctères et pas de chiffres !';
                return false;
            }

            if (emailValue.test(this.email) == false || !this.email) {
                document.querySelector('.errorEmail').textContent = 'Vérifiez votre email !';
                return false;
            }

            if (addressValue.test(this.address) == false || !this.address) {
                document.querySelector('.errorAddress').textContent = 'Vérifier votre adresse !';
                return false;
            }

            if (wordValue.test(this.city) == false || !this.city) {
                document.querySelector('.errorCity').textContent = 'Vérifier votre adresse !';
                return false;
            }

            if (numberbValue.test(this.zip) == false || !this.zip || this.zip.length < 5 || this.zip.length > 5) {
                document.querySelector('.errorZip').textContent = 'Il doit y avoir 5 chiffres !';
                return false;
            }

            if (wordValue.test(this.cardName) !== wordValue.test(this.firstName) || !this.cardName || this.cardName.length > 20 || this.cardName.length < 2) {
                document.querySelector('.errorCardName').textContent = 'L\'acheteur et le propriétaire de la carte doivent être identique !';
                return false;
            }

            if (numberbValue.test(this.cardNumber) == false || !this.cardNumber || this.cardNumber.length > 16 || this.cardNumber.length < 16) {
                document.querySelector('.errorCardNumber').textContent = 'Notez les 16 chiffres de la carte !';
                return false;
            }

            if (numberbValue.test(this.expirationDate) == false || !this.expirationDate) {
                document.querySelector('.errorExpirationDate').textContent = 'Vérifier l\'expiration de votre carte !';
                return false;
            }

            if (numberbValue.test(this.cvv) == false || !this.cvv || this.cvv.length > 3 || this.cvv.length < 3) {
                document.querySelector('.errorCvv').textContent = 'Vérifier le cvv au dos de votre carte !';
                return false;
            }
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