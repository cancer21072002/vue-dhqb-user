<template>
  <div>
    <H1>LIST USERS</H1>

    <signupUser :edit="userEdit" @submit="clickAdd"/>
    <table>
      <tr>
        <th>ID</th>
        <th>Your name</th>
        <th>Age</th>
        <th>Phone</th>
        <th>Email</th>
        <th>Gender</th>
        <th>Date</th>
        <th>Address</th>
        <th>Pass</th>
        <th>Action</th>
    
      </tr>
      <tr v-for="(item, index) in students" :key="index">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.age }}</td>
        <td>{{ item.phone }}</td>
        <td>{{ item.email }}</td>
        <td>{{ item.gender }}</td>
        <td>{{ item.date }}</td>
        <td>{{ item.address }}</td>
        <td>{{item.pass}}</td>
        <td>
          <button v-b-modal.modal-prevent-closing @click="clickEdit(item)">Edit</button>
          <button @click="clickDelete(item)">Delete</button>
        </td>
      </tr>
    
    </table>
  </div>
</template>

<script >
import signupUser from "./signupUser.vue"
export default {
  components: {
    signupUser
  },

  data () {
    return {
      userEdit:{},
      students: [
        {
          id:1,
          name: "Shouwa Genroku Rakugo Shinjuu",
          age: 12,
          phone: 9839988,
          email: "a24@gmail.com",
          gender: "Nam",
          date: "21/06/1999",
          address: "nha so 07, Van Phúc , ha Đong",
          pass:"a123"
        },
        {
          id: 2,
          name: "Shouwa Genroku Rakugo Shinjuu",
          age: 12,
          phone: 9839988,
          email: "a24@gmail.com",
          pass: "a123",
          gender: "Nam",
          date: "21/06/1999",
          address: "nha so 07, Van Phúc , ha Đong"
        },
        {
          id: 3,
          name: "Shouwa Genroku Rakugo Shinjuu",
          age: 12,
          phone: 9839988,
          pass: "a123",
          email: "a24@gmail.com",
          gender: "Nữ",
          date: "21/06/1999",
          address: "nha so 07, Van Phúc , ha Đong"
        },
        {
          id: 4,
          name: "Shouwa Genroku Rakugo Shinjuu",
          age: 12,
          pass: "a123",
          phone: 9839988,
          email: "a24@gmail.com",
          gender: "Nữ",
          date: "21/06/1999",
          address: "nha so 07, Van Phúc , ha Đong"
        },
        

      ],


    }
  },

  methods: {
    clickAdd (item) {
      let index= this.students.findIndex((c)=>c.id===item.id)
      if(index>=0){
        this.students.splice(index,1,item)
      }else{
        this.students.push(item);
      }
      return
      
    },

    clickDelete (itemDelete) {
      // console.log(itemDelete);
      // console.log(this.students.length);
      for(var i = 0; i < this.students.length; i++) {
        console.log(i);
        if (itemDelete.id === this.students[i].id)
         {
          console.log("before:" + this.students.length);
          this.students.splice(i,1)
          console.log("after:" + this.students.length);
        }
      }
    },

    clickEdit (itemEdit) {
      this.userEdit = itemEdit;
      console.log(itemEdit);
    }
  }
}
</script>

<style >
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
th{
  background-color: #0e81f5;
  
}

td,
th {
  border: 4px solid #070707;
  text-align: left;
  padding: 15px;
}


</style>