<template>
  <div id="app">
    <header><strong>Vue nutri</strong></header>
    <div v-if="loading">
      <h1>Carregando ....</h1>
    </div>
    <article v-else v-for="n in nutri" :key="n.id" class="post">
      <strong class="titulo">
        {{ n.titulo }}
        <img :src="n.capa" /><br>
        <span class="categoria">Categoria: {{ n.categoria }}</span><br>
        <p class="subtitulo">{{ n.subtitulo }}</p>
        <a class="botao" href="#">Acessar</a>
      </strong>
    </article>
  </div>
</template>

<script>
import api from './services/api';
export default {
  name: 'App',
  data() {
    return {
      nutri: [],
      loading: true
    }
  },
  async created() {
    const response = await api.get('?api=posts');
    this.nutri = response.data;
    console.log(this.nutri);
    this.loading = false;
  }
}
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 35px;
  width: 100%;
  height: 60px;
  background-color: #4cb9e3;
  color: #FFF;


}

.post {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 700px;
  background-color: #FFF;
  border-radius: 7px;
  margin: 8px;
  padding: 10px;
}

.titulo {
  font-size: 25px;
  margin-top: 10px;
  margin-bottom: 25px;
}

.categoria {
  padding-top: 15px;
  font-weight: bold;
}

.botao {
  height: 40px;
  background: none;
  border-radius: 5px;
  border: 2px solid #4c89e3;
  color: #4c89e3;
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
  font-size: 18px;
  transition: all 0.5s;

}

.botao:hover {
  background: #4c89e3;
  color: #FFF;
}
</style>>
