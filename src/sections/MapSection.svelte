<!-- I used ChatGPT to help guide me through importing the MapBox API and helping it zoom into the two different counties. -->
<script lang="ts">
    import { onMount } from 'svelte'; 
    import mapboxgl from 'mapbox-gl'; 

    export let zoomTarget: {
        center: [number, number];
        zoom: number;
    }; // { center: [lng, lat], zoom: number }

    let map: mapboxgl.Map; 
    let mapLoaded = false;

    mapboxgl.accessToken = 'pk.eyJ1Ijoic2l5YWdvc3dhbWkiLCJhIjoiY21kNmRoM3loMDd3aTJrcTJldWs0cWN4eCJ9.8jt8P9tkvth7tnssIhiDrg';
    onMount(() => {
        map = new mapboxgl.Map({
            container: 'map',
            style: 'mapbox://styles/mapbox/light-v11',
            center: zoomTarget.center, 
            zoom: zoomTarget.zoom,
        });

        map.on('load', () => {
            mapLoaded = true;
        });
    });

    $: if(map && mapLoaded && zoomTarget?.center && zoomTarget?.zoom !== undefined){
        console.log("flying to: ", zoomTarget);
        map.flyTo({
            center: zoomTarget.center,
            zoom: zoomTarget.zoom,
            speed: 0.8, 
            curve: 1.4, 
            essential: true
        });
    }
</script>

<style>
    #map {
        width: 100%; 
        height: 100vh; 
        position: sticky; 
        top: 0; 
        z-index: 0;
    }
</style>

<div id = "map"></div>