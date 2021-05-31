<template>
    <div class="foot_box">
        <div class="foot_box_inside">
            <a href="">Livraison</a>
            <a href="">Moyen de paiement</a>
        </div>
        <div class="foot_box_inside">
            <a href="">Contact</a>
            <a href="">FAQ</a>
        </div>
    </div>
</template>

<style scoped>
.foot_box, .foot_box_inside {
    display: flex;
}

.foot_box {
    flex-direction: row;
    justify-content: space-around;
}

.foot_box_inside {
    flex-direction: column;
    align-items: center;
}
</style>