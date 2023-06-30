

<template>
	<div class="card">
		<div class="nav-menu">

			

		</div>
<div class="body">
  <div class="search">
				<a>
					<input
						type="text"
						class="search-bar"
						placeholder="Search dishes, restaurants"
						v-model="searchQuery"
					/>

				</a>
			</div>
			
			<div class="statistique">
				<div class="top-stat">
					<div class="stat-order">
						<h1 class="number">{{Orderstoday}}</h1>
						<h2 class="subtitle">Orders today</h2>
					</div>
					<div class="stat-order">
						<h1 class="number">{{Ordersweek}}</h1>
						<h2 class="subtitle">Orders this week</h2>
					</div>
				</div>
      </div>
	</div>
  </div>
</template>
<script>
/* eslint-disable vue/multi-word-component-names */

import axios from 'axios';

export default {
	name: 'StatComponent',
    
    data() {
        return {
            Orderstoday:0,
            Ordersweek:0,
            revenueData: [null],
			
            
            
			searchQuery: '',
            
            intervalId: null,
        };
    },
    methods: {
        
      async fetchRestaurantStats() {
      try {
        let response = await axios.get(`http://3.83.173.28:7000/api/order/get/currentstatistics/${this.searchQuery}`);
        console.log(response.data);
        this.revenueData = response.data;
        let response2 = await axios.get(`http://3.83.173.28:7000/api/order/get/statistics/${this.searchQuery}`);
        const arr = Object.values(response2.data);
		console.log(arr);
        this.Orderstoday = arr[0];
        this.Ordersweek = arr[1];

      } catch (error) {
        console.error(error);
      }
  },
        removeOrder(index) {
            this.orders.splice(index, 1);
        },
    },
   
    mounted() {
    // Call the fetchData method when the component is created
    this.fetchRestaurantStats();
  },
  watch: {
    searchQuery: {
      handler: 'fetchRestaurantStats',
      immediate: false
    }
  },

	removeOrder(index) {
		this.orders.splice(index, 1);
	},
    
    
};
</script>

<style >

.search,
.title-div,
.categories,
.title-section {
	margin-right: auto;
}
.search::before {
	content: url("@/assets/search.svg"); /* Replace with your icon path */
	position: relative;
	pointer-events: none;
	top: 40px;
	left: 20px;
}
.search-bar {
	width: 86vw;
	padding-left: 50px;

	max-width: 660px;
}
@media (max-width: 555px){
	.search-bar {
		width: 78vw;
	}
}
.body {
	display: flex;
	overflow: auto;
	flex-wrap: wrap;
	justify-content: space-around;
	padding: 20px;
	text-align: left;
	padding-top: 0;
	align-items: center;
	align-content: space-around;
	overflow-x: hidden;
}
.card {
	max-width: 750px;
	min-width: 350px;
	width: 100%;
	margin: auto;
	background: #ffffff9d;
	border-radius: 25px;
	padding-bottom: 5px;
	display: block;
	overflow: auto;
}
.nav-menu {
	display: flex;
	margin: 20px;
	justify-content: space-between;
	margin-bottom: 10px;
}
.menu-left {
	display: flex;
	flex-direction: row;
}

.settings {
	display: flex;
}
.title-delivery {
	padding-top: 7px;
	padding-left: 12px;
	display: flex;
	flex-direction: column;
	align-items: flex-start;
}
.deliver-to {
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 15px;
	line-height: 14px;
	text-transform: uppercase;
	color: #fc6e2a;
	margin-top: 3px;
	margin-bottom: 2px;
}
.btn-delivery {
	font-family: "Sen";
	font-style: normal;
	font-weight: 400;
	font-size: 17px;
	line-height: 17px;
	/* identical to box height */
	color: #676767;
	background-color: transparent;
	border: 0;
	padding: 0;
}
.cart {
	display: flex;
}
.top-stat {
	display: flex;
}
.statistique {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
}
.stat-order {
	background: #ffffff;
	border-radius: 20px;
	padding: 20px;
	margin: 16px;
}
.number {
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 52.32px;
	line-height: 63px;
	/* identical to box height */

	display: flex;
	align-items: center;
	text-align: center;

	color: #32343e;
	margin: 2.5px;
}
.subtitle {
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 13px;
	line-height: 16px;
	/* identical to box height */

	text-align: center;
	text-transform: uppercase;

	color: #838799;
	margin: 0;
}
.chart {
	background: #ffffff;
	border-radius: 20px;
	padding: 20px;
	margin: 16px;
	width: 75vw;
	max-width: 700px;
	min-width: 300px;
}
.deliveryRequest {
	position: absolute;
	z-index: 5;
	background: #ffffff;
	border: 1px solid #e8e8e8;
	padding: 20px;
	border-radius: 24px;
	box-shadow: 0px -2px 40px rgba(58, 119, 153, 0.15);
}
.top-content {
	height: 100%;
}

.bottom-content {
	display: flex;

	justify-content: center;
}
.btn-accept {
	background: #669bbc;
	border-radius: 12px;
	width: 80px;
	height: 62px;
	left: 24px;
	top: 526px;
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 14px;
	line-height: 17px;
	/* identical to box height */

	text-align: center;
	text-transform: uppercase;
	border: 0;
	color: #ffffff;
	cursor: pointer;
}
.btn-reject {
	background: #b5313c;
	border-radius: 12px;
	width: 80px;
	height: 62px;
	left: 24px;
	top: 526px;
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 14px;
	line-height: 17px;
	/* identical to box height */

	text-align: center;
	text-transform: uppercase;
	border: 0;
	color: #ffffff;
	cursor: pointer;
}
.text-popup {
	margin-left: 10px;
	margin-right: 10px;
	display: flex;
	flex-direction: column;
	align-items: center;
}
.price {
	font-family: "Sen";
	font-style: normal;
	font-weight: 800;
	font-size: 32px;
	line-height: 38px;
	color: #181c2e;
	margin: 0;
}
.time {
	font-family: "Sen";
	font-style: normal;
	font-weight: 400;
	font-size: 15px;
	line-height: 24px;
	text-transform: capitalize;
	color: #a0a5ba;
	margin: 0;
}

.driver {
	display: flex;
	margin-right: auto;

	margin-top: 10px;
}

.line {
	width: 100%;
	height: 1px;
	background-color: #a0a5ba;
}

.name {
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 20px;
	line-height: 24px;
	/* identical to box height */

	text-transform: capitalize;

	color: #181c2e;
}

.delivery-steps {
	display: flex;
	flex-direction: column;
	align-items: center;
	margin-bottom: 10px;
	margin-right: auto;
	margin-left: 20px;
}

.step {
	display: flex;
	align-items: center;
	padding: 10px;
	width: 200px;
}

.step-icon {
	border-radius: 50%;
	display: flex;
	justify-content: center;
	align-items: center;
	margin-right: 10px;
}

.step-label {
	font-family: "Sen";
	font-style: normal;
	font-weight: 400;
	font-size: 13px;
	line-height: 16px;
	color: #a0a5ba;
}

.active {
	color: #cc6151;
}

.time {
	display: flex;
	flex-direction: column;
	align-items: center;
}

.estimate-time {
	font-family: "Sen";
	font-style: normal;
	font-weight: 800;
	font-size: 30px;
	line-height: 36px;
	/* identical to box height */
	margin-top: 30px;
	margin-bottom: 5px;

	color: #181c2e;
}

.image {
	width: 100%;
	max-width: 100px;
	height: 100%;
	max-height: 100px;
}

.top {
	display: flex;
}

.bottom {
	margin-left: 10px;
}

.items {
	font-family: "Sen";
	font-style: normal;
	font-weight: 700;
	font-size: 13px;
	line-height: 16px;
	/* identical to box height */

	text-transform: capitalize;

	color: #646982;
	margin: 2px;
}

.title {
	font-family: "Sen";
	font-style: normal;
	font-weight: 400;
	font-size: 18px;
	line-height: 22px;
	text-transform: capitalize;
	color: #181c2e;
}

.subtitle {
	font-family: "Sen";
	font-style: normal;
	font-weight: 400;
	font-size: 14px;
	line-height: 17px;
	/* identical to box height */

	text-transform: capitalize;

	color: #a0a5ba;
	margin-top: 0;
}

.map {
	height: 600px;
}

.order {
	display: flex;
	flex-direction: column;
	margin-right: auto;
}

.container {
	position: relative;
	height: 100vh;
	width: 100vw;
}

.background-component {
	height: 100%;
	width: 100%;
	background-color: lightblue;
}

.overlay-component {
	position: absolute;
	/* height: 73%; */
	max-width: 300px;
	background: #ffffff;
	box-shadow: 0px -2px 40px rgba(58, 119, 153, 0.15);
	border-radius: 24px 24px 0px 0px;
	cursor: ns-resize;
	display: flex;
	padding: 30px;
	flex-direction: column;
	align-content: center;
	align-items: center;
	justify-content: flex-start;
	width: 80vw;
    min-width: 400px;
	z-index: 100;
	padding-bottom: 10px;
	padding-top: 15px;
}
.search-bar-routerlink {
  text-decoration: none;
}

input {
  display: flex;
  background: #f0f5fa;
  border-radius: 10px;
  height: 4em;
  font-family: "Sen";
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 17px;
  border: 0;
  align-items: center;
  width: 291px;
  color: #a0a5ba;
  margin-bottom: 8px;
}
</style>
