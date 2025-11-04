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


<!DOCTYPE html>
<html>
  <head>
    <title><%= productName %></title>
    <meta charset="utf-8">
    <meta name="description" content="<%= productDescription %>">
    <meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width">
    <link rel="icon" type="image/png" sizes="128x128" href="icons/favicon-128x128.png">
  </head>
  <body>
    <!-- quasar:entry-point -->
  </body>
</html>


<template>
  <q-page>
    <div style="background-color: gray; width: 10%; height: 30%; position: absolute; margin-left: 90%;">
      <q-btn flat icon="photo_camera" label="Camara" @click="accionBoton1"/>
      <q-btn flat icon="pin_drop" label="Ubicacion" @click="accionBoton2"/>
      <q-btn flat icon="info" label="Informacion del drone dagger" @click="accionBoton2"/>
    </div>

    <div style="background-color: gray; width: 10%; height: 55%; position: absolute;">
      <q-btn flat icon="photo_camera" label="Video" @click="accionBoton1"/>
      <q-btn flat icon="pin_drop" label="Bateria" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="Motores" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="radio" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="estructura del drone" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="Seguridad" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="Parametros" @click="accionBoton2"/>
    </div>

    <div id="map"></div>
  </q-page>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  mounted() {
    mapboxgl.accessToken = "pk.eyJ1IjoiamxhcmExMjMiLCJhIjoiY2xzdXk2eGxqMmJrdjJxdGdxcG5nNTduZCJ9.-wQcOTVQSYzV_e0lCrauag";
    const map = new mapboxgl.Map({
      container: "map",
      center: [-74.5, 40],
      zoom: 9,
    });
    navigator.geolocation.getCurrentPosition((pos) => {
      const { latitude, longitude } = pos.coords;
      new mapboxgl.Marker().setLngLat([longitude, latitude]).addTo(map);
      map.flyTo({ center: [longitude, latitude], zoom: 13 });
    });
  },
};
</script>

<style scoped>
#map {
  height: 100vh;
}
</style>
##Implementa los botones y el mapa de Mapbox:

<template>
  <q-page>
    <div style="background-color: gray; width: 10%; height: 30%; position: absolute; margin-left: 90%;">
      <q-btn flat icon="photo_camera" label="Camara" @click="accionBoton1"/>
      <q-btn flat icon="pin_drop" label="Ubicacion" @click="accionBoton2"/>
      <q-btn flat icon="info" label="Informacion del drone dagger" @click="accionBoton2"/>
    </div>

    <div style="background-color: gray; width: 10%; height: 55%; position: absolute;">
      <q-btn flat icon="photo_camera" label="Video" @click="accionBoton1"/>
      <q-btn flat icon="pin_drop" label="Bateria" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="Motores" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="radio" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="estructura del drone" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="Seguridad" @click="accionBoton2"/>
      <q-btn flat icon="pin_drop" label="Parametros" @click="accionBoton2"/>
    </div>

    <div id="map"></div>
  </q-page>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  mounted() {
    mapboxgl.accessToken = "pk.eyJ1IjoiamxhcmExMjMiLCJhIjoiY2xzdXk2eGxqMmJrdjJxdGdxcG5nNTduZCJ9.-wQcOTVQSYzV_e0lCrauag";
    const map = new mapboxgl.Map({
      container: "map",
      center: [-74.5, 40],
      zoom: 9,
    });
    navigator.geolocation.getCurrentPosition((pos) => {
      const { latitude, longitude } = pos.coords;
      new mapboxgl.Marker().setLngLat([longitude, latitude]).addTo(map);
      map.flyTo({ center: [longitude, latitude], zoom: 13 });
    });
  },
};
</script>

<style scoped>
#map {
  height: 100vh;
}
</style>
El repositorio explica que la estación en tierra usa ROSBridge Suite para comunicar la interfaz web con ROS/MAVROS, lo que permite visualizar y controlar datos de vuelo desde el entorno gráfico (tipo QGroundControl o MissionPlanner, pero con integración nativa a ROS).


dagger-groundstation/
│
├── public/
│   ├── index.html
│   └── icons/
│       └── favicon-128x128.png
│
├── src/
│   ├── main.js
│   ├── App.vue
│   └── components/
│       └── MapInterface.vue
│
├── package.json
└── quasar.config.js

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Dagger Ground Station</title>

    <!-- Mapbox CSS -->
    <link
      href="https://api.mapbox.com/mapbox-gl-js/v2.15.0/mapbox-gl.css"
      rel="stylesheet"
    />

    <link rel="icon" type="image/png" href="icons/favicon-128x128.png" />
  </head>
  <body>
    <div id="q-app"></div>
    <!-- Quasar App Entry -->
  </body>
</html>

import { createApp } from "vue";
import { Quasar } from "quasar";
import App from "./App.vue";
import "./style.css";

const app = createApp(App);
app.use(Quasar, { plugins: {} });
app.mount("#q-app");

<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-primary text-white flex items-center q-px-md">
      <h5 class="q-ma-none">Estación de Tierra - Dagger</h5>
    </q-header>

    <q-page-container>
      <MapInterface />
    </q-page-container>
  </q-layout>
</template>

<script>
import MapInterface from "./components/MapInterface.vue";

export default {
  name: "App",
  components: { MapInterface },
};
</script>

<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-primary text-white flex items-center q-px-md">
      <h5 class="q-ma-none">Estación de Tierra - Dagger</h5>
    </q-header>

    <q-page-container>
      <MapInterface />
    </q-page-container>
  </q-layout>
</template>

<script>
import MapInterface from "./components/MapInterface.vue";

export default {
  name: "App",
  components: { MapInterface },
};
</script>

<template>
  <q-page class="relative-position bg-grey-2">
    <!-- Panel lateral derecho -->
    <div
      class="fixed-top-right q-pa-sm"
      style="width: 220px; top: 80px; right: 20px; background: rgba(255,255,255,0.9); border-radius: 12px;"
    >
      <div class="q-mb-sm text-bold">Controles del Dron</div>

      <q-btn label="Cámara" icon="photo_camera" color="primary" glossy class="full-width q-mb-sm" @click="accionBoton('camara')" />
      <q-btn label="Ubicación" icon="pin_drop" color="primary" glossy class="full-width q-mb-sm" @click="accionBoton('ubicacion')" />
      <q-btn label="Video" icon="videocam" color="primary" glossy class="full-width q-mb-sm" @click="accionBoton('video')" />
      <q-btn label="Batería" icon="battery_full" color="primary" glossy class="full-width q-mb-sm" @click="accionBoton('bateria')" />
      <q-btn label="Motores" icon="memory" color="primary" glossy class="full-width q-mb-sm" @click="accionBoton('motores')" />
      <q-btn label="Seguridad" icon="security" color="primary" glossy class="full-width q-mb-sm" @click="accionBoton('seguridad')" />
      <q-btn label="Parámetros" icon="tune" color="primary" glossy class="full-width" @click="accionBoton('parametros')" />
    </div>

    <!-- Mapa principal -->
    <div id="map" class="full-width" style="height: 100vh;"></div>
  </q-page>
</template>

<script>
import mapboxgl from "mapbox-gl";
import ROSLIB from "roslib";

export default {
  name: "MapInterface",
  data() {
    return {
      map: null,
      ros: null,
    };
  },
  mounted() {
    this.initMap();
    this.connectROS();
  },
  methods: {
    initMap() {
      mapboxgl.accessToken =
        "pk.eyJ1IjoiamxhcmExMjMiLCJhIjoiY2xzdXk2eGxqMmJrdjJxdGdxcG5nNTduZCJ9.-wQcOTVQSYzV_e0lCrauag";

      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11",
        center: [-74.08175, 4.60971], // Bogotá por defecto
        zoom: 12,
      });

      navigator.geolocation.getCurrentPosition(
        (pos) => {
          const { latitude, longitude } = pos.coords;
          new mapboxgl.Marker({ color: "red" })
            .setLngLat([longitude, latitude])
            .addTo(this.map);
          this.map.flyTo({ center: [longitude, latitude], zoom: 15 });
        },
        (err) => console.error("Error obteniendo ubicación:", err)
      );
    },

    connectROS() {
      // Conexión a ROSBridge (ajusta la IP según tu red)
      this.ros = new ROSLIB.Ros({
        url: "ws://localhost:9090",
      });

      this.ros.on("connection", () => {
        console.log("✅ Conectado a ROSBridge");
      });

      this.ros.on("error", (error) => {
        console.error("❌ Error al conectar a ROSBridge:", error);
      });

      this.ros.on("close", () => {
        console.warn("⚠️ Conexión a ROSBridge cerrada");
      });
    },

    accionBoton(tipo) {
      console.log(`Botón presionado: ${tipo}`);
      // Ejemplo: Publicar en ROS cuando se presiona un botón
      if (this.ros && this.ros.isConnected) {
        const topic = new ROSLIB.Topic({
          ros: this.ros,
          name: "/dagger/command",
          messageType: "std_msgs/String",
        });
        const msg = new ROSLIB.Message({ data: tipo });
        topic.publish(msg);
      }
    },
  },
};
</script>

<style scoped>
#map {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>

{
  "name": "dagger-groundstation",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "quasar dev",
    "build": "quasar build"
  },
  "dependencies": {
    "mapbox-gl": "^2.15.0",
    "quasar": "^2.16.0",
    "roslib": "^1.3.0",
    "vue": "^3.4.0"
  }
}
npm install -g @quasar/cli
npm install
quasar dev
http://localhost:9000


