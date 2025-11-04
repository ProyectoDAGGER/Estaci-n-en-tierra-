# Estaci-n-en-tierra-
La presente documentación detalla el desarrollo y funcionamiento de una estación en tierra diseñada para monitorear el sistema de drones Dagger, el cual opera con inteligencia artificial en enjambres para la detección de objetos. Este proyecto ha sido concebido para proporcionar a los usuarios una herramienta integral de supervisión y control

Diseño de Interfaz
Vue.js y el Framework Quasar: Una Visión General
Vue.js es un framework progresivo de JavaScript para construir interfaces de usuario. Creado por Evan You y
lanzado en 2014, Vue.js se centra en la capa de vista del modelo-vista-controlador (MVC) y es conocido por su
facilidad de integración con otros proyectos y bibliotecas.
Características Principales de Vue.js
• Reactividad: Sistema que actualiza automáticamente la interfaz cuando cambian los datos.
• Componentes: Arquitectura basada en componentes reutilizables y modulares.
• Data Binding: Enlace de datos bidireccional para sincronizar el modelo con la vista.
• Directivas: Herramientas como v-bind, v-model, v-if para manipular el DOM.
• Ecosistema Rico: Herramientas como Vue CLI, Vue Router y Vuex.
• Fácil Integración: Adaptable a proyectos existentes y fácil de combinar con otras bibliotecas

Quasar es un framework de desarrollo de aplicaciones basado en Vue.js que permite crear aplicaciones
web, móviles y de escritorio con una única base de código. Quasar amplía las capacidades de Vue.js
proporcionando un conjunto completo de herramientas y componentes.Características Principales de Quasar

Multiplataforma: Desarrollo para web, móviles (Cordova o Capacitor) y escritorio (Electron).
• Componentes de UI: Amplia biblioteca de componentes personalizables y listos para usar.
• Rendimiento: Optimizaciones para carga diferida y administración eficiente del estado.
• CLI Poderoso: Herramientas para generar proyectos, manejar dependencias y compilar código.
• Internacionalización: Soporte integrado para crear aplicaciones multilingües.
• Documentación y Comunidad: Excelente documentación y una comunidad activa que ofrece soporte y
recursos.

<!DOCTYPE html>
<html>
<head>
<title><%= productName %></title>
<meta charset="utf-8">
<meta name="description" content="<%= productDescription %>">
<meta name="format-detection" content="telephone=no">
<meta name="msapplication-tap-highlight" content="no">
<meta name="viewport" content="user-scalable=no, initial-scale=1, maximumscale=
1, minimum-scale=1, width=device-width<% if (ctx.mode.cordova ||
ctx.mode.capacitor) { %>, viewport-fit=cover<% } %>">
<link rel="icon" type="image/png" sizes="128x128" href="icons/
favicon-128x128.png">
<link rel="icon" type="image/png" sizes="96x96" href="icons/favicon-96x96.png">
<link rel="icon" type="image/png" sizes="32x32" href="icons/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="icons/favicon-16x16.png">
<link rel="icon" type="image/ico" href="favicon.ico">
</head>
<body>
<!-- quasar:entry-point -->
</body>
</html>

Desde el codigo en html llamado Index se realiza el llamado al los archivos.js o JavaScript y junto a ello en la
etiqueta de <body></body> se anexa la estructura de Quasar

<template>
<q-page>
<div
style="
background-color: gray;
width: 10%;
height: 30%;
position: absolute;
margin-left: 90%;
text-align: right;
padding: 0.3%;
border-radius: 0 0 10px 10px;

"
>
<!-- Botones en el lado derecho -->
<q-btn
flat
icon="photo_camera"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
@click="accionBoton1"
label="Camara"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="Ubicacion"
/>
<q-btn
flat
icon="info"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="Informacion del drone dagger"
/>
</div>
<div
style="
background-color: gray;
width: 10%;
height: 55%;
position: absolute;
padding: 0.3%;
border-radius: 0 0 10px 10px;
"
>
<!-- Botones en el lado derecho -->
<q-btn
flat

icon="photo_camera"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
@click="accionBoton1"
label="Video"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="Bateria"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="Motores"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="radio"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="estructura del drone"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="Seguridad"
/>
<q-btn
flat
icon="pin_drop"
@click="accionBoton2"
style="
background-color: rgb(255, 255, 255);
width: 100%;
margin-bottom: 5%;
"
label="Parametros"
/>
</div>
<div id="map"></div>
</q-page>
</template>
<script>
import mapboxgl from "mapbox-gl";
export default {
mounted() {
// Configura la clave de acceso de Mapbox
mapboxgl.accessToken =
"pk.eyJ1IjoiamxhcmExMjMiLCJhIjoiY2xzdXk2eGxqMmJrdjJxdGdxcG5nNTduZCJ9.-
wQcOTVQSYzV_e0lCrauag";
// Crea una instancia del mapa
const map = new mapboxgl.Map({
container: "map", // el ID del contenedor en tu template
//style: 'mapbox://styles/mapbox/streets-v11', // puedes cambiar el estilo
center: [-74.5, 40], // coordenadas iniciales del centro del mapa
zoom: 9, // nivel de zoom inicial
});
// Obtén la ubicación actual del usuario
navigator.geolocation.getCurrentPosition(
(position) => {
const { latitude, longitude } = position.coords;
// Agrega un marcador en la ubicación actual
console.log([longitude, latitude]);
new mapboxgl.Marker().setLngLat([longitude, latitude]).addTo(map);
// Centra el mapa en la ubicación actual
map.flyTo({ center: [longitude, latitude], zoom: 13 });
},
(error) => {
console.error("Error al obtener la ubicación:", error);
}
);
},
};
</script>
<style scoped>
#map {
height: 100vh;
/* Establece la altura al 100% del viewport */
}
</style>

<img width="850" height="363" alt="image" src="https://github.com/user-attachments/assets/97a93181-eb61-406c-a6de-8b4676f1a12d" />

