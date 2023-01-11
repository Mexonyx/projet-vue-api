<template>
  <div class="div">
    <b style="font-size: 25px">{{ nom }}</b
    ><br />
    <i style="font-size: 15px">{{ adresse }} {{ cp }}</i
    ><br />
    Conditions : {{ conditions }}<br />
    Exloitant : {{ exploitant }}<br />
    Horaires d'ouverture : {{ ouverture }}<br />
    Capacite de la station : {{ capacite }}<br />
    <b v-if="ligne_tc" style="font-size: 17px"
      ><i>Lignes proche de la station: {{ ligneTc }}</i></b
    >
  </div>
</template>

<script>
export default {
  name: "AStation",
  props: {
    nom: String,
    adresse: String,
    cp: String,
    conditions: String,
    exploitant: String,
    ouverture: String,
    capacite: String,
    ligneTc: String,
  },
};
</script>

<style>
.div {
  border: 1px solid black;
  border-radius: 12px;
  padding: 14px;
  display: table-cell;
}
</style>
