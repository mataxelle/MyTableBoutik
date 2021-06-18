<template>
    <div>

        <h2>Finalisez votre commande</h2>
        <form action="">
            <div class="form">
               <div class="adress">
                   <h3>Addresse de livraison</h3>
                   <div class="name">
                       <div>
                           <label for="lastName"> Nom</label>
                           <input type="text" id="lastName" name="lastName" required>
                        </div>
                        <div>
                           <label for="firstName"> Prénom</label>
                           <input type="text" id="firstName" name="firstname" required>
                        </div>
                   </div>
                   <div class="emailInfo">
                       <label for="email"> Email</label>
                       <input type="email" id="email" name="email" required>
                   </div>
                   <div class="adressInfo">
                       <label for="address"> Adresse</label>
                       <input type="text" id="address" name="address" required>
                   </div>
                   <div class="cityInfo">
                       <div>
                           <label for="city"> Ville</label>
                           <input type="text" id="city" name="city" required>
                       </div>
                       <div>
                            <label for="zip">Code Postal</label>
                            <input type="text" id="zip" name="zip" required>
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
                        <div>
                            <label for="cardName">Détenteur de la carte</label>
                            <input type="text" id="cardName" name="cardName" required>
                        </div>
                        <div>
                            <label for="cardNumber">Credit card number</label>
                            <input type="text" id="cardNumber" name="cardnumber" required>
                        </div>
                    </div>

                    <div class="cardInfoDate">
                        <div>
                            <label for="expirationDate">Date d'expiration</label>
                            <input type="text" id="expirationDate" name="expirationDate" required>
                        </div>
                        <div>
                            <label for="cvv">CVV</label>
                            <input type="text" id="cvv" name="cvv" required>
                        </div>
                    </div>    
                </div>
                <div>
                    <button @click="confirmOrder">Confirmer la commande</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "UserInformationComponent",

    methods: {
        confirmOrder() {

            const firstName = document.getElementById('firstName').value;
            const lastName = document.getElementById('lastName').value;
            const email = document.getElementById('email').value;
            const address = document.getElementById('address').value;
            const city = document.getElementById('city').value;
            const zip = document.getElementById('zip').value;
            const cardName = document.getElementById('cardName').value;
            const cardNumber = document.getElementById('cardNumber').value;
            const expirationDate = document.getElementById('expirationDate').value;
            const cvv = document.getElementById('cvv').value;

            const wordValue = /[a-zA-Z-]/;
            const numberbValue = /[0-9]/
            const addressValue = /[a-zA-Z0-9\s]/;
            //const caractValue = /[!$%§^&*@(),.?":#{}|<>]/;
            const emailValue = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]/;

            if (wordValue.test(firstName) == false || firstName == "" || firstName.length > 20 || firstName.length < 2) {
                alert('Vérifier votre prénom !');
                return false;
            }

            if (wordValue.test(lastName) == false || lastName == "" || lastName.length > 20 || lastName.length < 2) {
                alert('Vérifier votre nom !');
                return false;
            }

            if (emailValue.test(email) == false || email == "") {
                alert('Vérifier votre email !');
                return false;
            }

            if (addressValue.test(address) == false || address == "") {
                alert('Vérifier votre prénom !');
                return false;
            }

            if (wordValue.test(city) == false || city == "") {
                alert('Vérifier votre ville !');
                return false;
            }

            if (numberbValue.test(zip) == false || zip == "" || zip.length < 5 || zip.length > 5) {
                alert('Vérifier votre code postal !');
                return false;
            }

            if (wordValue.test(cardName) == false || cardName == "" || cardName.length > 20 || cardName.length < 2) {
                alert('Vérifier le nom du propriétaire de la carte !');
                return false;
            }

            if (numberbValue.test(cardNumber) == false || cardNumber == "" || cardNumber.length > 16 || cardNumber.length < 16) {
                alert('Vérifier votre numéro de carte !');
                return false;
            }

            if (numberbValue.test(expirationDate) == false || expirationDate == "") {
                alert('Vérifier l\'expiration de votre carte !');
                return false;
            }

            if (numberbValue.test(cvv) == false || cvv == ""|| cvv.length > 3 || cvv.length < 3) {
                alert('Vérifier le cvv de votre carte !');
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

button {
    margin: 10px 0;
    height: 40px;
    width: 40%;
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