<template>
	<div>
		<h1>Simulacija utrke 4 automobila</h1>
		
		
		<div>
			<h2>Unesi automobile</h2>
			<input v-model="carBrand" placeholder="Marka automobila" />
			<input v-model="carModel" placeholder="Model automobila" />
			<button @click="addCar">Dodaj automobil</button>
		</div>
		
		
		<div>
			<h2>Postavke utrke:</h2>
			<input v-model.number="trackLength" type="number" placeholder="Duljina kruga" />
			<input v-model.number="laps" type="number" placeholder="Broj krugova" />
			<button @click="startRace">Pokreni utrku</button>
		</div>
		
		<div v-if="raceResults.length">
			<h2>Rezultati utrke:</h2>
			<ul>
				<li v-for="(result, index) in raceResults" :key="index">
					{{ result.carBrand }} - {{ result.carModel }} - {{ result.time }}min - Mjesto: {{ index + 1 }}
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			carBrand: '',
			carModel: '',
			trackLength: 0,
			laps: 0,
			cars: [],
			raceResults: [],
		};
	},
	methods: {
		addCar() {
			if (this.carBrand && this.carModel) {
				this.cars.push({
					carBrand: this.carBrand,
					carModel: this.carModel,
					time: 0,
				});
				this.carBrand = '';
				this.carModel = '';
			}
		},
		startRace() {
			if (this.trackLength > 0 && this.laps > 0 && this.cars.length >=4) {
			
				this.cars.forEach((car) => {
					car.time = Math.random() * (this.trackLength * this.laps * 0.1);
				});
			
				this.cars.sort((a, b) => a.time - b.time);
			
				this.raceResults = this.cars.slice(0, 4);
			} else {
				alert('Unesite sve potrebne informacije za utrku!');
			}
		},
	},
};
</script>

<style scoped>
div {
  font-family: Arial, sans-serif;
  margin: 20px;
}

h1 {
  font-size: 24px;
  color: #333;
  text-align: center;
}

h2 {
  font-size: 18px;
  margin-top: 20px;
}

input[type="text"],
input[type="number"] {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px 20px;
  background-color: #007BFF;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  font-size: 16px;
  margin: 5px 0;
  padding: 5px;
  background-color: #f4f4f4;
  border-radius: 5px;
}

.alert {
  padding: 10px;
  background-color: #ff7f7f;
  color: #fff;
  border-radius: 5px;
  margin-top: 10px;
}

</style>