<template>
		<h1>Stations de vélo</h1>
		<div id="demo">
			<div  v-if="stations">
				<h1>Stations BiCloo Nantes</h1>
					<label for="query">Rechercher par propriétés (adresse, nombre de place etc...) </label>
					<input
					type="text"
					id="query"
					value="query"
					name="query"
					>
				<ul style="list-style-type: none;">
					<li v-for="station in stations" style="display: inline-block; padding: 14px; align-content: space-between;">
						<div style="border:1px solid black; border-radius: 12px; padding: 14px; display: table-cell;">
							<b style="font-size: 25px;">{{ station.fields.nom }}</b><br>
							<i style="font-size: 15px;">{{ station.fields.adresse }} {{ station.fields.cp }}</i><br>
							Conditions : {{ station.fields.conditions }}<br>
							Exloitant : {{ station.fields.exploitant }}<br>
							Horaires d'ouverture : {{ station.fields.ouverture }}<br>
							Capacite de la station : {{ station.fields.capacite }}<br>
							<b v-if="station.fields.ligne_tc" style="font-size: 17px;"><i>Lignes proche de la station: {{ station.fields.ligne_tc }}</i></b>
						</div>
					</li>
				</ul>
			</div>
		</div>
</template>

<script>
export default {
  name: "Index",
  props: {
    msg: String,
  },
};
const apiURL =
				"https://data.nantesmetropole.fr/api/records/1.0/search/?dataset=244400404_stations-velos-libre-service-nantes-metropole&q=";
			

			Vue.createApp({
				data() {
					return {
            rowNumber: 10,
            stations: null,
						query: "",
					};
				},

				created: function () {
					this.fetchDataQueryAsync()
				},

				watch: {
					query: "fetchDataQueryAsync",
				},
				methods: {
					fetchDataQueryAsync: async function () {
						try {
							const response = await axios.get(apiURL+this.query)
							console.log(response.data)
							this.stations = response.data.records
						} catch(error){
							console.log(error)
						}
					},
				},
			}).mount("#demo");
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#demo {
				font-family: "Helvetica", Arial, sans-serif;
			}
			a {
				text-decoration: none;
				color: #f66;
			}
			li {
				line-height: 1.5em;
				margin-bottom: 20px;
			}
</style>
