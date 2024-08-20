<template>
  <div class="clientes-container">
    <h1 class="clientes-title">Lista de Clientes</h1>
    <div v-if="clientes.length" class="table-wrapper">
      <table class="clientes-table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nombre</th>
            <th>Email</th>
            <th>Fecha de Registro</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="cliente in clientes" :key="cliente.id_cliente">
            <td>{{ cliente.id_cliente }}</td>
            <td>{{ cliente.nombre }}</td>
            <td>{{ cliente.email }}</td>
            <td>{{ cliente.fecha_registro }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <p v-else class="no-clients-message">No se encontraron clientes.</p>
    <p v-if="error" class="error-message">{{ error }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListaClientes",
  data() {
    return {
      clientes: [],
      error: null,
    };
  },
  async created() {
    try {
      const response = await axios.get("http://localhost:3306/api/clientes");
      this.clientes = response.data;
    } catch (error) {
      this.error = "Error al obtener los clientes";
      console.error(error);
    }
  },
};
</script>

<style scoped>
.clientes-container {
  padding: 20px;
  background-color: #f4f4f4;
}

.clientes-title {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

.table-wrapper {
  margin: 0 auto;
  max-width: 100%;
  overflow-x: auto;
}

.clientes-table {
  width: 100%;
  border-collapse: collapse;
}

.clientes-table th,
.clientes-table td {
  padding: 12px;
  border: 1px solid #ddd;
}

.clientes-table th {
  background-color: #0a641a;
  color: #fff;
}

.no-clients-message {
  text-align: center;
  color: #333;
}

.error-message {
  text-align: center;
  color: #e74c3c;
}
</style>
