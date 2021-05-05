<template>
  <div id="map"></div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import "leaflet-easybutton/src/easy-button.js";
import "leaflet-easybutton/src/easy-button.css";
export default {
  name: "Map",
  data() {
    return {
      map: null,
      zoom: 13,
      Lat: -6.892894218251732,
      Lng: 107.62338276015929,
      changeSymbol: null,
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.map = new L.Map(document.querySelector("#map"), {
        center: new L.LatLng(this.Lat, this.Lng),
        zoom: 13,
      });

      let osmLayer = new L.tileLayer(
        "//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
        {
          noWrap: true,
        }
      );
      osmLayer.addTo(this.map);

      let layersControl = new L.control.layers({
        OSM: osmLayer,
      });

      this.map.addControl(layersControl);

      let milButton = L.easyButton(
        '<img src="images/cus.svg" style="width:16px" class="cus">',
        function () {
          this.changeSymbol = "Cus";
          console.log(this.changeSymbol);
          cusButton.enable();
          milButton.disable();
        }
      );

      let cusButton = L.easyButton(
        '<img src="images/mil.svg" style="width:16px" class="mil">',
        function () {
          this.changeSymbol = "Mil";
          console.log(this.changeSymbol);
          cusButton.disable();
          milButton.enable();
        }
      );

      let symbolBar = L.easyBar([milButton, cusButton]);
      symbolBar.addTo(this.map);
      milButton.disable();  
    },
  },
};
</script>

<style>
#map {
  height: 50vh;
  width: 80vh;
  border-radius: 10px;
  margin: 0 auto;
}

#map img.mil {
  margin-top: -10px;
}

#toggle-check-and-x {
  width: 200px;
  height: 100px;
  transition-duration: 0.3s;
}
#toggle-check-and-x.x-mark-active {
  background-color: red;
}
#toggle-check-and-x.check-mark-active {
  background-color: green;
}
</style>