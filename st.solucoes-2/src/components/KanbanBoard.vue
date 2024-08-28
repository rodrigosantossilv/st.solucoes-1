<template>
    <div class="container-fluid p-3">
      <!-- Cabeçalho -->
      <b-header class="bg-primary text-white p-3">
        <img src="_img/ST.KABAN.png" class="imagem-ajustada" alt="Descrição da Imagem">
        <h1 class="text-center">Dashboard</h1>
      </b-header>
  
      <!-- Estrutura principal com o Dashboard e Kanban -->
      <div class="d-flex">
        <!-- Sidebar (Dashboard) -->
        <b-sidebar class="bg-secondary text-white p-3" position="start" variant="dark">
          <h2>Opções</h2>
          <b-nav vertical>
            <b-nav-item @click="showAll">Todos</b-nav-item>
            <b-nav-item @click="showColumn('Pendente')">Pendentes</b-nav-item>
            <b-nav-item @click="showColumn('Andamento')">Andamentos</b-nav-item>
            <b-nav-item @click="showColumn('Concluido')">Concluídos</b-nav-item>
          </b-nav>
        </b-sidebar>
  
        <!-- Kanban Board -->
        <div class="kanban-board d-flex justify-content-around flex-grow-1 p-3">
          <b-card class="kanban-column" v-show="showPendente" dropzone>
            <h3 class="kanban-header bg-danger text-white p-2 text-center">Pendente</h3>
            <b-card v-for="chamado in chamadosFiltrados('Pendente')" :key="chamado.id" class="kanban-item bg-light p-3 my-2" draggable @dragstart="drag($event, chamado.id)">
              <p>{{ chamado.assunto }}</p>
            </b-card>
          </b-card>
  
          <b-card class="kanban-column" v-show="showAndamento" dropzone>
            <h3 class="kanban-header bg-primary text-white p-2 text-center">Andamento</h3>
            <b-card v-for="chamado in chamadosFiltrados('Andamento')" :key="chamado.id" class="kanban-item bg-light p-3 my-2" draggable @dragstart="drag($event, chamado.id)">
              <p>{{ chamado.assunto }}</p>
            </b-card>
          </b-card>
  
          <b-card class="kanban-column" v-show="showConcluido" dropzone>
            <h3 class="kanban-header bg-success text-white p-2 text-center">Concluído</h3>
            <b-card v-for="chamado in chamadosFiltrados('Concluido')" :key="chamado.id" class="kanban-item bg-light p-3 my-2" draggable @dragstart="drag($event, chamado.id)">
              <p>{{ chamado.assunto }}</p>
            </b-card>
          </b-card>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'KanbanBoard',
    data() {
      return {
        chamados: [
          {
            id: 1,
            assunto: "pendentes",
            status: "Pendente",
            dataAbertura: "10/05/2022"
          },
          {
            id: 2,
            assunto: "Assunto 1",
            status: "Andamento",
            dataAbertura: "10/05/2022"
          },
          {
            id: 3,
            assunto: "Assunto",
            status: "Concluido",
            dataAbertura: "10/05/2022"
          }
        ],
        showPendente: true,
        showAndamento: true,
        showConcluido: true,
      };
    },
    methods: {
      showAll() {
        this.showPendente = true;
        this.showAndamento = true;
        this.showConcluido = true;
      },
      showColumn(column) {
        this.showPendente = column === 'Pendente';
        this.showAndamento = column === 'Andamento';
        this.showConcluido = column === 'Concluido';
      },
      chamadosFiltrados(status) {
        return this.chamados.filter(chamado => chamado.status === status);
      },
      drag(event, id) {
        event.dataTransfer.setData('text/plain', id);
      },
    },
  };
  </script>
  
  <style>
  /* Adicione seus estilos customizados aqui */
  .kanban-board {
    min-height: 500px;
  }
  
  .kanban-column {
    flex: 1;
    margin: 0 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
  
  .kanban-header {
    font-size: 1.2em;
  }
  
  .kanban-item {
    margin-bottom: 10px;
    cursor: move;
  }
  /* Reset básico */
body, html {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    font-family: Arial, sans-serif;
}

/* Cabeçalho */
header {
    width: 100%;
    background: #0575E6;
    display: flex;
    align-items: center; /* Alinha a imagem e o texto verticalmente */
    padding: 10px; /* Adiciona algum espaço interno */
    box-sizing: border-box; /* Inclui o padding e border na largura e altura */
}

/* Contêiner para a imagem e o texto */
.header-content {
    display: flex;
    align-items: center; /* Alinha a imagem e o texto verticalmente no centro */
}

/* Ajuste da imagem no cabeçalho */
.imagem-ajustada {
    width: 90px; /* Ajuste o tamanho conforme necessário */
    height: auto; /* Mantém a proporção da imagem */
    margin-right: 10px; /* Espaço entre a imagem e o texto */
}

/* Estilo do título no cabeçalho */
header h1 {
    color: white; /* Define a cor do texto */
    margin: 0; /* Remove a margem padrão */
    font-size: 1.5rem; /* Ajuste o tamanho da fonte conforme necessário */
}

/* Sidebar (Dashboard) */
.sidebar {
    width: 250px;
    min-height: 100vh;
    background: linear-gradient(to bottom, #0575E6, #02298A, #021B79);
}

/* Kanban Board */
.kanban-board {
    display: flex;
    flex-grow: 1;
    gap: 20px;
}

/* Kanban Column */
.kanban-column {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* Kanban Header */
.kanban-header {
    width: 100%;
    font-size: 1.5rem;
    text-align: center;
    border-radius: 8px;
}

/* Kanban Item */
.kanban-item {
    width: 100%;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
}

  </style>
  