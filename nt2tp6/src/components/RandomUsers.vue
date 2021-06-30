<template>

  <section class="src-components-random-users">

    <div class="jumbotron">
      <p class="alert alert-danger" v-if="this.errors"> {{ this.errors}} </p>
      <TableUsers v-bind:usersToShow="this.usersToShow" v-bind:options="{hasAge: true, hasPhone: false}" v-on:deleted="refreshPage()" />
    </div>

  </section>

</template>

<script lang="js">

  import TableUsers from './TableUsers';


  export default  {
    name: 'src-components-random-users',
    components: {
      TableUsers
    },
    props: [],
    async mounted () {

      try {
        let users = await this.axios(this.urlToFetch);
        console.log('Fetched users:', users.data);
        this.usersToShow = users.data;
      } catch (error) {
        console.log('Error D:', error);
      }

    },
    data () {
      return {
        urlToFetch: 'https://60b54a9dfe923b0017c83dfb.mockapi.io/api/users/user',
        usersToShow: {},
        errors: undefined
      }
    },
    methods: {
      refreshPage(){
          this.axios(this.urlToFetch)
          .then(rsp =>{
            this.usersToShow = rsp.data;
          })
          .catch(err => {
            console.log('Error', err);
          });

      }
    },
    computed: {
      
    }
}


</script>

<style scoped lang="css">

</style>
