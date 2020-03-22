<template>
  <v-container>
       <h3 class="headline mb-0"> {{username}}'s Message History</h3>
       <v-btn
              class="mr-4"
              @click="back"
            >Back</v-btn>
    <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Date/Time</th>
          <th class="text-left">Message</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="message in messages" :key="message._id">
          <td>{{ convertedTime(message.time) }}</td>
          <td>{{ message.message }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
  </v-container>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'History',
  components: {

  },
  data(){
      return{
          messages: []
      }
  },
  methods:{
      convertedTime: function(date){
          let d = new Date(parseInt(date));
          return d.toString();
      },
      back: function(){
          this.$router.push('/');
      }
      

  },
  props: {
      username: String
  },
  mounted(){
    let instance = this, 
      user = this.username,
      token = localStorage.getItem("token");
    this.axios
      .get(`/messages/${user}`, {
        headers: { "x-access-token": token }
      })
      .then(response => {
        console.log(response);
        if (response.status == 200) {
          console.log(response.data)
          instance.messages = response.data.response;
        }
      })
      .catch(err => {
        console.log(err);
      });
  }
}
</script>
