<template>
  <div>
    <h1 id="h1"></h1>

    <router-link to="/">Continuer mes achats</router-link>

    <div id="cartAndCheckout">
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
          <tbody id="cartBody"></tbody>
          <tfoot>
            <tr>
              <td id="totalSomme" colspan="6"></td>
            </tr>
          </tfoot>
        </table>
      </div>

      <UserInformationComponent />
    </div>
  </div>
</template>

<script>
import UserInformationComponent from "@/components/UserInformationComponent.vue";

let cartLocalStorage = JSON.parse(localStorage.getItem("cartItem"));

export default {
  name: "CartComponent",
  components: {
    UserInformationComponent,
  },

  mounted() {
    if (!cartLocalStorage) {

      document.querySelector("h1").textContent = "Votre panier est vide !";
      document.getElementById("cartAndCheckout").style.display = "none";

    } else {
      document.querySelector("h1").textContent = "Mon panier";

      let totalSomme = 0;

      for (let i = 0; i < cartLocalStorage.length; i++) {
        const cartItem = cartLocalStorage[i];

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
          console.log('ok');
          row.style.background = "rgba(175, 125, 95, 0.31)";
        } else {                  //sinon impair
          console.log('no');
          row.style.background = "rgba(175, 125, 95, 0.959)";
        }

        cell1.textContent = cartItem.name;
        cell2.textContent = cartItem.vanish;
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
    }
  },
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

tr {
  background: rgb(48, 45, 45); 
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