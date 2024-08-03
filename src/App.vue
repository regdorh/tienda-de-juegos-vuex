<template>
  <h1>Tienda 32 Bits</h1>
  <h3>Lista de juegos</h3>
  <div class="filter">

  </div>
  <table class="table">
    <thead>
      <th>Código</th>
      <th>Portada</th>
      <th>Nombre</th>
      <th>Stock</th>
      <th>Precio</th>
      <th>Acciones</th>
    </thead>
    <tbody>
      <tr v-for="(juego, i) in juegos" :key="i">
        <td>{{ juego.codigo }}</td>
        <td><img :src="juego.cover" alt=""> </td>
        <td class="game-name">{{ juego.nombre }}</td>
        <td>{{ juego.stock }}</td>
        <td>${{ Number(juego.precio).toLocaleString() }}</td>
        <td>
          <button @click="decrementar(i)">-</button>
          <button @click="incrementar(i)">+</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  name: 'App',
  computed: {
    ...mapState(['juegos']),
  },
  methods: {
    ...mapActions(['incrementar', 'decrementar']),
  },
}
</script>

<style>
*{
  margin:0;
  padding: 0;
  outline: 0;
}

.filter{
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  z-index: 1;
  background-color: #FFE53B;
  background-image: linear-gradient(147deg, #FFE53B 0%, #FF2525 74%);
}

table{
  position: absolute;
  z-index: 2;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
  width: 60%; 
  border-collapse: collapse;
  border-spacing: 0;
  box-shadow: 0 2px 15px rgba(64,64,64,.7);
  border-radius: 12px 12px 0 0;
  overflow: hidden;

}

table img {
  height: 50px;
}

td , th{
  padding: 15px 20px;
  text-align: center;
 

}

th{
  background-color: #FF2525;
  color: #fafafa;
  font-family: "Crimson Text", serif;
  font-weight: 700;
  font-style: normal;

}

tr{
  width: 100%;
  background-color: #fafafa;
  font-family: "Crimson Text", serif;
  font-weight: 600;
  font-style: normal;
}

tr:nth-child(even){
  background-color: #eeeeee;
}

tr:hover {
  background-color: #f5f5f5;
  transform: scale(1.02);
  box-shadow: 2px 2px 12px rgba(0, 0, 0, 0.2), -1px -1px 8px rgba(0, 0, 0, 0.2);
}

button {
  margin: 10px;
  padding: 5px;
  border: none;
  outline: none;
  color: #FFF;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 12px;
}

button::after {
  content: "";
  z-index: -1;
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #333;
  left: 0;
  top: 0;
  border-radius: 10px;
}

/* glow */
button::before {
  content: "";
  background: linear-gradient(
    45deg,
    #FF0000, #FF7300, #FFFB00, #48FF00,
    #00FFD5, #002BFF, #FF00C8, #FF0000
  );
  position: absolute;
  top: -2px;
  left: -2px;
  background-size: 600%;
  z-index: -1;
  width: calc(100% + 4px);
  height:  calc(100% + 4px);
  filter: blur(8px);
  animation: glowing 20s linear infinite;
  transition: opacity .3s ease-in-out;
  border-radius: 10px;
  opacity: 0;
}

@keyframes glowing {
  0% {background-position: 0 0;}
  50% {background-position: 400% 0;}
  100% {background-position: 0 0;}
}

/* hover */
button:hover::before {
  opacity: 1;
}

button:active:after {
  background: transparent;
}

button:active {
  color: #000;
  font-weight: bold;
}
</style>
