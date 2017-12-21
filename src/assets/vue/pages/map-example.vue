<template>
	<f7-page>
		<f7-navbar title="Map Example" back-link="Back" sliding></f7-navbar>
		<f7-block inner>
			<f7-grid>
  				<f7-col width="40">
  					<f7-button raised color="red" @click="createRandomMarker()">Add Marker</f7-button>
  				</f7-col>
  				<br><br>
  				<f7-col width="100">
					<GmapMap
						style="
							height: 600px; width: 100%;
						    margin: 0px;
						    padding: 0px;"
						ref="map"
						:zoom="2"
						:center="{lat: -25.363, lng: 131.044}">
						<GmapMarker
							v-for="(marker, index) in markers"
							:key="index"
							:position="marker.position">
						</GmapMarker>
					</GmapMap>
  				</f7-col>
  			</f7-grid>
  			<br>
		</f7-block>
	</f7-page>
</template>

<script>

export default {
	data () {
		return {
		  markers: [{
            position: {
              lat: -25.363,
              lng: 131.044
            }
          }]
		}
	},
	watch: {
		markers(markers) {
		}
	},
	methods: {
		getRandomInRange(from, to, fixed) {
			return (Math.random() * (to - from) + from).toFixed(fixed) * 1;
		},
		createRandomMarker() {
			var marker = {
				position: {
					lat: this.getRandomInRange(-80, 80, 3),
					lng: this.getRandomInRange(-80, 80, 3)
				}
			}
			this.markers.push(marker)
		}
	}
}
</script>