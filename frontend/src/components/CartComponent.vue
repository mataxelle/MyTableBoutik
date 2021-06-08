<template>
  <div>
    <h1 id="h1"></h1>

    <div>
      <table id="tableCart">
        <thead>
          <tr>
            <th>Produit</th>
            <th>Couleur</th>
            <th>Prix unitaire</th>
            <th>Qt</th>
            <th>Total</th>
          </tr>
        </thead>
        <tbody id="cartBody"></tbody>
        <tfoot>
          <tr>
            <td id="totalSomme"></td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</template>

<script>
let cartLocalStorage = JSON.parse(localStorage.getItem("cartItem"));

export default {
  name: "CartComponent",

  mounted() {
    if (!cartLocalStorage) {

      document.querySelector("h1").textContent = "Panier vide !";
      document.getElementById("tableCart").style.display = 'none';

    } else {

      document.querySelector("h1").textContent = "Finaliser votre commande !";

      let totalSomme = 0;

      for (let i = 0; i < cartLocalStorage.length; i++) {
        const cartItem = cartLocalStorage[i];

        let totalRow = (cartItem.quantity * cartItem.price) / 100;

        const table = document.getElementById("cartBody");
        const row = table.insertRow(); //tr
        const cell1 = row.insertCell(0); //td
        const cell2 = row.insertCell(1);
        const cell3 = row.insertCell(2);
        const cell4 = row.insertCell(3);
        const cell5 = row.insertCell(4);
        const cell6 = row.insertCell(5);
        const cancelBtn = document.createElement('button');
        cancelBtn.classList.add('cancelBtn');
        cancelBtn.textContent = 'x';
        console.log(cancelBtn);

        cell1.textContent = cartItem.name;
        cell2.textContent = cartItem.vanish;
        cell3.textContent = cartItem.price / 100 + "€";
        cell4.textContent = cartItem.quantity;
        cell5.textContent = totalRow + "€";
        cell6.appendChild(cancelBtn);

        totalSomme = totalSomme + totalRow;

        cancelBtn.addEventListener("click", (e) => {
          e.preventDefault();
          console.log('cliqué');

          table.deleteRow(i);
          cartLocalStorage.splice(i, 1);
          localStorage.setItem('cartItem', JSON.stringify(cartLocalStorage));
          document.location.reload();
        });
      }

      document.getElementById("totalSomme").textContent = `Total : ${totalSomme}`;
    }
  }
};
</script>