<template>
  <div id="app">
    <!-- Formulario de configuración con fondo de color -->
    <div class="form-container">
      <!-- Color de fondo -->
      <label>
        Color de fondo
        <input type="text" v-model="backgroundColor" />
      </label>

      <!-- Color de texto -->
      <label>
        Color de texto
        <input type="text" v-model="textColor" />
      </label>

      <!-- Mostrar texto -->
      <label>
        Mostrar texto
        <input type="checkbox" v-model="showText" />
      </label>

      <!-- Borde -->
      <label>
        Borde
        <input type="range" min="0" max="50" v-model="borderRadius" />
      </label>

      <!-- Contenido textual -->
      <label>
        Contenido textual
        <textarea v-model="textContent"></textarea>
      </label>

      <!-- Tipografía -->
      <label>
        Tipografía
        <select v-model="fontFamily">
          <option v-for="font in fonts" :key="font" :value="font">{{ font }}</option>
        </select>
      </label>

      <!-- Opacidad -->
      <label>
        Opaco
        <input type="checkbox" v-model="opaque" />
      </label>

      <!-- Tamaño de letra -->
      <fieldset>
        <legend>Tamaño de letra</legend>
        <label>
          <input type="radio" value="small" v-model="fontSize" /> Pequeño
        </label>
        <label>
          <input type="radio" value="medium" v-model="fontSize" /> Mediano
        </label>
        <label>
          <input type="radio" value="large" v-model="fontSize" /> Grande
        </label>
      </fieldset>
    </div>

    <!-- Figura de vista previa -->
    <div class="preview" :style="previewStyle" :class="{ opaque: opaque }">
      <span v-if="showText" :style="{ fontSize: computedFontSize }">{{ textContent }}</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      backgroundColor: "green",
      textColor: "white",
      showText: true,
      borderRadius: 10,
      textContent: "Awesome Vue.js",
      fontFamily: "sans-serif",
      opaque: false,
      fontSize: "medium",
      fonts: ["sans-serif", "serif", "cursive"],
    };
  },
  computed: {
    previewStyle() {
      return {
        backgroundColor: this.backgroundColor,
        color: this.textColor,
        borderRadius: `${this.borderRadius}px`,
        fontFamily: this.fontFamily,
      };
    },
    computedFontSize() {
      // Define el tamaño de letra basado en la selección
      switch (this.fontSize) {
        case "small":
          return "12px";
        case "medium":
          return "16px";
        case "large":
          return "20px";
        default:
          return "16px";
      }
    },
  },
};
</script>

<style>
#app {
  display: flex;
  gap: 20px;
  padding: 20px;
  background-color: #ffffff;
  color: rgb(10, 10, 10);
  font-family: sans-serif;
}

.form-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 10px;
  background-color: #3c3c3c; /* Fondo de color para el formulario */
  padding: 20px;
  border-radius: 10px;
}

.preview {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #8fbc8f;
  border-radius: 10px;
  padding: 20px;
  min-width: 200px;
  min-height: 200px;
  transition: all 0.3s ease;
}

.preview.opaque{
  opacity: 0.5;
}
</style>
