<template>
  <li>
    <h2>{{ name }} {{ FriendIsFavorite === 'true' ? '♥' : ''}} </h2>
    <button @click="toggleFavorite" > Toggle {{ FriendIsFavorite ? 'favorite' : 'unfavorite'}}</button>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show'}} details</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
    <button @click="$emit('delete', id)">delete</button>
  </li>
</template>

<script>
export default {
  emits: ['delete'],
  // props: [
  //   'name',
  //   'phoneNumber',
  //   'emailAddress',
  //   'isFavorite'
  // ],

props: {
  id:{
    type: String,
    required: true
  },
  name: {
    type: String,
    required: true
  },
  phoneNumber: {
    type: String,
    required: true
  },
  emailAddress: {
    type: String,
    required: true
  },
  isFavorite: {
    type: String,
    required: false,
    default: 'false',
    validator: function(value){
      return value === 'true' || 'false'
    }
  },
},
  data() {
    return {
      detailsAreVisible: false,
      friend: {
        id: "manuel",
        name: "Manuel Lorenz",
        phone: "0123 45678 90",
        email: "manuel@localhost.com",
      },
      FriendIsFavorite: this.isFavorite
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },

    toggleFavorite(){
      if(this.FriendIsFavorite === 'true'){
        this.FriendIsFavorite ='false'
      }else{
        this.FriendIsFavorite = 'true'
      }
    },

    deleteFriend(id){
      this.friends = this.friends.filter(friend => friend.id != id)
    }
  }
};
</script>
