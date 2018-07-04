<template>
  <div id="view-employee">
    <ul class="collection with-header">
      <li class="collection-header">
        <h4>
          <i class="fas fa-user-graduate left"></i> {{ name }}
        </h4>
      </li>
      <li class="collection-item">
        <i class="fas fa-user-tie left"></i>ID:<span class="badge white-text green">{{ employee_id }}</span>
      </li>
      <li class="collection-item">
        <i class="fas fa-building left"></i> Отдел: <span class="badge  white-text  green">{{ dept }}</span>
      </li>
      <li class="collection-item">
        <i class="far fa-address-card left"></i> Должность :<span class="badge  white-text green">{{ position }}</span>
      </li>
    </ul>
    <router-link to="/" class="btn grey">
      <i class="far fa-hand-point-left left"></i> Назад
    </router-link>
    <button class="btn red" @click="deleteEmployee">
      <i class="far fa-trash-alt left"></i> Удалить
    </button>
  </div>
</template>

<script>
  import db from './firebaseInit';

  export default {
    name: 'view-employee',
    data () {
      return {
        employee_id: null,
        name: null,
        dept: null,
        position: null
      }
    },
    beforeRouteEnter (to, from, next) {
      db.collection('employees').where('employee_id', '==', to.params.employee_id).get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            next(vm => {
              vm.employee_id = doc.data().employee_id;
              vm.name = doc.data().name;
              vm.dept = doc.data().dept;
              vm.position = doc.data().position;
            })
          })
        })
    },
    watch: {
      '$route': 'fetchData'
    },
    methods: {
      fetchData () {
        db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get()
          .then(querySnapshot => {
            querySnapshot.forEach(doc => {
              this.employee_id = doc.data().employee_id;
              this.name = doc.data().name;
              this.dept = doc.data().dept;
              this.position = doc.data().position;
            })
          })
      },
      deleteEmployee () {
        if (confirm('Are you sure?')) {
          db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get()
          .then(querySnapshot => {
            querySnapshot.forEach(doc => {
              doc.ref.delete();
              this.$router.push('/');
            })
          })
        }
      }
    }
  }
</script>

<style>
  .badge {
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3)!important;
    border-radius: 20px!important;
  }
</style>
