<template>
  <div>
    <h1 v-if="cartItems">Mon panier</h1>
    <h1 v-else>Panier vide</h1>

    <router-link to="/">Continuer mes achats</router-link>

    <div id="cartAndCheckout" v-if="cartItems.length > 0">
      <div class="tableDiv">
        <table id="tableCart">
          <thead>
            <tr>
              <th>Produit</th>
              <th>Couleur</th>
              <th>Prix unitaire</th>
              <th>Qt</th>
              <th>Total</th>
              <th>x</th>
            </tr>
          </thead>
          <tbody id="cartBody">
            <tr v-for="(cartItem, index) in cartItems" :key="index" :cartItem="cartItem">
              <td>{{ cartItem.name }}</td>
              <td>{{ cartItem.varnish }}</td>
              <td>{{ cartItem.price / 100 + "€" }}</td>
              <td>{{ cartItem.quantity }}</td>
              <td>{{ cartItem.price / 100 * cartItem.quantity }}</td>
              <td><button @click="removeToCart">X</button></td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <td id="totalSomme" colspan="6"> Total </td>
            </tr>
          </tfoot>
        </table>
      </div>
    </div>

  </div>
</template>

<script>

const cartLocalStorage = JSON.parse(localStorage.getItem("cartItem"));

export default {
  name: "CartComponent",
  components: {},

  data() {
    return {
      cartItems: {}
    }
  },

  mounted() {

    this.cartItems = cartLocalStorage;

    /*if (!cartLocalStorage.length) {

      document.querySelector("h1").textContent = "Votre panier est vide !";
      document.getElementById("cartAndCheckout").style.display = "none";

    } else {
      document.querySelector("h1").textContent = "Mon panier";

      let totalSomme = 0;

      for (let i = 0; i < cartLocalStorage.length; i++) {
        const cartItem = cartLocalStorage[i];

        this.cartItems = cartItem;

        let totalRow = (cartItem.quantity * cartItem.price) / 100;

        const table = document.getElementById("cartBody");
        const rowCount = table.rows.length;
        const row = table.insertRow(rowCount); //tr. (0) ajoute l'item en première ligne
        const cell1 = row.insertCell(0); //td
        const cell2 = row.insertCell(1);
        const cell3 = row.insertCell(2);
        const cell4 = row.insertCell(3);
        const cell5 = row.insertCell(4);
        const cell6 = row.insertCell(5);
        const cancelBtn = document.createElement("button");
        cancelBtn.classList.add("cancelBtn");
        cancelBtn.textContent = "x";

        if (rowCount % 2 == 0) {  // vérifie si le nombre est pair
          row.style.background = "rgba(175, 125, 95, 0.31)";
        } else {                  //sinon impair
          row.style.background = "rgba(175, 125, 95, 0.959)";
        }

        cell1.textContent = cartItem.name;
        cell2.textContent = cartItem.varnish;
        cell3.textContent = cartItem.price / 100 + "€";
        cell4.textContent = cartItem.quantity;
        cell5.textContent = totalRow + "€";
        cell6.appendChild(cancelBtn);

        totalSomme = totalSomme + totalRow;

        cancelBtn.addEventListener("click", (e) => {
          e.preventDefault();
          console.log("cliqué");

          table.deleteRow(i);
          cartLocalStorage.splice(i, 1);
          localStorage.setItem("cartItem", JSON.stringify(cartLocalStorage));
          document.location.reload();
        });
      }

      document.getElementById(
        "totalSomme"
      ).textContent = `Total : ${totalSomme} €`;
    }*/
  },

  methods: {
    removeToCart(index) {

      index.preventDefault();

      document.getElementById("cartBody").deleteRow(index);
      cartLocalStorage.splice(index, 1);
      localStorage.setItem("cartItem", JSON.stringify(cartLocalStorage));
      document.location.reload();
    }
  }
};
</script>

<style scoped>

.tableDiv {
  margin: 40px 0 80px 0;
}

table {
  margin: auto;
  width: 85%;
  border-collapse: collapse;
}

thead tr, tfoot tr {
  background: rgb(48, 45, 45); 
}

tbody tr:nth-child(odd) {
  background-color: rgba(175, 125, 95, 0.31);
}

th, #totalSomme {
  background: #333;
  color: white;
  font-weight: bold;
  padding: 6px;
  border: 1px solid #ccc;
}

th {
  text-align: center;
}

#totalSomme {
  text-align: right;
  padding-right: 90px;
}
</style>