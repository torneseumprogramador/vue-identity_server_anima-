<template>
  <div>
    <h1>Lista de Administradores</h1>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>Email</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="administrator in administrators" :key="administrator.id">
          <td>{{ administrator.id }}</td>
          <td>{{ administrator.name }}</td>
          <td>{{ administrator.email }}</td>
          <td>
            <button class="btn btn-danger" @click="deleteAdministrator(administrator.id)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      administrators: [],
    };
  },
  async created() {
    await this.fetchAdministrators();
  },
  methods: {
    async fetchAdministrators() {
      try {
        const response = await axios.get('http://localhost:5218/api/administrators', {
          headers: {
            Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ2YWx1ZSI6IntcIklkXCI6MSxcIk5hbWVcIjpcIkRhbmlsb1wiLFwiRW1haWxcIjpcImRhbmlsb0B0ZXN0ZS5jb21cIn0iLCJuYmYiOjE2ODk2NzQ0NjQsImV4cCI6MTY5MDI3OTI2NCwiaWF0IjoxNjg5Njc0NDY0fQ.1TExhgnFHabmSQEK56zyksZOk4z-cBJsiq4A5lG9m7M',
          },
        });
        this.administrators = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async deleteAdministrator(id) {
      try {
        await axios.delete(`http://localhost:5218/api/administrators/${id}`, {
          headers: {
            Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ2YWx1ZSI6IntcIklkXCI6MSxcIk5hbWVcIjpcIkRhbmlsb1wiLFwiRW1haWxcIjpcImRhbmlsb0B0ZXN0ZS5jb21cIn0iLCJuYmYiOjE2ODk2NzQ0NjQsImV4cCI6MTY5MDI3OTI2NCwiaWF0IjoxNjg5Njc0NDY0fQ.1TExhgnFHabmSQEK56zyksZOk4z-cBJsiq4A5lG9m7M',
          },
        });
        await this.fetchAdministrators();
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style>
.table {
  margin-top: 20px;
}
</style>
