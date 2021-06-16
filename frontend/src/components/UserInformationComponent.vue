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
                       <input type="text" id="email" name="email" required>
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
                            <label for="expDate">Date d'expiration</label>
                            <input type="text" id="exDate" name="exDate" required>
                        </div>
                        <div>
                            <label for="cvv">CVV</label>
                            <input type="text" id="cvv" name="cvv" required>
                        </div>
                    </div>    
                </div>
                <div>
                    <button>Confirmer la commande</button>
                </div>
            </div>
        </form>
    </div>
</template>

<style scoped>
form {
    width: 70%;
    margin: 30px auto;
    padding: 30px;
    background-color: rgba(175, 125, 95, 0.959);
}

div {
    margin: 15px 0;
}

.name, .cityInfo, .cardInfo, .cardInfoDate {
    display: flex;
    justify-content: space-around;
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
</style>