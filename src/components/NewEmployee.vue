<template>
  <div id="new-employee">
    <h3>
      <i class="fas fa-user-plus left"></i> Добавить сотрудника
    </h3>
    <div class="row">
      <form @submit.prevent="saveEmployee" class="col s12">
        <div class="row">
          <div class="input-field col s12">
            <input type="text" v-model="employee_id" required>
            <label>
              <i class="fas fa-user-tie left"></i>ID# сотрудника
            </label>
          </div>
        </div>
        <div class="row">
          <div class="input-field col s12">
            <input type="text" v-model="name" required>
            <label>
              <i class="fas fa-user-circle left"></i></i>Имя
            </label>
          </div>
        </div>
        <div class="row">
          <div class="input-field col s12">
            <input type="text" v-model="dept" required>
            <label>
              <i class="fas fa-building left"></i>Отдел
            </label>
          </div>
        </div>
        <div class="row">
          <div class="input-field col s12">
            <input type="text" v-model="position" required>
            <label>
              <i class="far fa-address-card left"></i>Должность
            </label>
          </div>
        </div>
        <button type="submit" class="btn blue">
          <i class="fas fa-plus left"></i>Добавить
        </button>
        <router-link to="/" class="btn grey">
          <i class="fas fa-ban left"></i>Отмена
        </router-link>
      </form>
    </div>
  </div>
</template>

<script>
  import db from './firebaseInit';

  export default {
    name: 'new-employee',
    data () {
      return {
        employee_id: null,
        name: null,
        dept: null,
        position: null
      }
    },
    methods: {
      saveEmployee () {
        db.collection('employees').add({
          employee_id: this.employee_id,
          name: this.name,
          dept: this.dept,
          position: this.position
        })
        .then(docRef => {
          this.$router.push('/')
        })
        .catch(error => console.log(err))
      }
    }
  }
</script>

<style>
   
        
</style>
