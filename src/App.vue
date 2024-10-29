<template>
  <div class="container">
    <h2>Cadastro de Times de Futebol</h2>
    <!-- Formulário para adicionar um novo time -->
    <form @submit.prevent="adicionarTime">
      <div>
        <label for="nome">Nome do Time:</label>
        <input
          type="text"
          v-model="novoTime.nome"
          placeholder="Digite o nome do time"
        />
      </div>
      <div>
        <label for="cidade">Cidade:</label>
        <input
          type="text"
          v-model="novoTime.cidade"
          placeholder="Digite a cidade do time"
        />
      </div>
      <div>
        <label for="anoFundacao">Ano de Fundação:</label>
        <input
          type="number"
          v-model="novoTime.anoFundacao"
          placeholder="Digite o ano de fundação"
        />
      </div>
      <button type="submit">Cadastrar Time</button>
    </form>

    <!-- Exibição de mensagem caso a lista esteja vazia -->
    <div v-if="times.length === 0" class="mensagem-vazia">
      <p>Nenhum time cadastrado.</p>
    </div>

    <!-- Lista de times cadastrados -->
    <ul v-else>
      <li v-for="(time, index) in times" :key="index">
        <strong>{{ time.nome }}</strong> - {{ time.cidade }} (Fundado em: {{ time.anoFundacao }})
        <button @click="removerTime(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      novoTime: {
        nome: '',
        cidade: '',
        anoFundacao: ''
      },
      times: []
    };
  },
  methods: {
    adicionarTime() {
      // Validação simples dos campos
      if (!this.novoTime.nome || !this.novoTime.cidade || !this.novoTime.anoFundacao) {
        alert('Por favor, preencha todos os campos.');
        return;
      }

      // Adiciona o time à lista de times
      this.times.push({ ...this.novoTime });

      // Limpa os campos após o cadastro
      this.novoTime.nome = '';
      this.novoTime.cidade = '';
      this.novoTime.anoFundacao = '';
    },
    removerTime(index) {
      // Remove o time da lista
      this.times.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

button {
  margin-top: 10px;
  padding: 5px 10px;
  background-color: #3498db;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  padding: 10px;
  background-color: #f0f0f0;
  border-radius: 5px;
}

.mensagem-vazia {
  margin-top: 20px;
  font-style: italic;
  color: #666;
}
</style>
