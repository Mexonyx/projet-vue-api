<template>
  <h1>Stations de vélo</h1>
  <div v-if="stations">
    <h1>Stations BiCloo Nantes</h1>
    <label for="query"
      >Rechercher par propriétés (adresse, nombre de place etc...)
    </label>
    <input type="text" :id="query" :value="query" :name="query" />
    <ul style="list-style-type: none">
      <li
        v-for="station in stations"
        v-bind:key="station.fields"
        style="
          display: inline-block;
          padding: 14px;
          align-content: space-between;
        "
      >
        <AStation
          :nom="station.fields.nom"
          :adresse="station.fields.adresse"
          :cp="station.fields.cp"
          :conditions="station.fields.conditions"
          :exploitant="station.fields.exploitant"
          :ouverture="station.fields.ouverture"
          :capacite="station.fields.capacite"
          :ligneTc="station.fields.ligne_tc"
        />
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import AStation from "@/components/AStation.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    AStation,
  },

  data: function () {
    return {
      apiURL:
        "https://data.nantesmetropole.fr/api/records/1.0/search/?dataset=244400404_stations-velos-libre-service-nantes-metropole&q=",
      rowNumber: 10,
      stations: null,
      query: "",
    };
  },
  created: function () {
    this.fetchDataQueryAsync();
  },

  watch: {
    query: "fetchDataQueryAsync",
  },
  methods: {
    fetchDataQueryAsync: async function () {
      try {
        const response = await axios.get(this.apiURL + this.query);
        console.log(response.data);
        this.stations = response.data.records;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
