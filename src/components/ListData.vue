<template>
    <transition-group tag="ul" name="list">
        <li v-for="user in users" :key="user"
        @click="removeUser(user)">{{ user }}</li>
    </transition-group>
    <div>
        <input type="text" v-model="inputUser">
        <button @click="addUser">Add user</button>
    </div>
</template>

<script>
    export default {
        name: 'ListData',
        data(){
            return{
                users: ['abc', 'def', 'pqr', 'xyz'],
                inputUser: '',
            };
        },
        methods: {
            addUser(){
                this.users.push(this.inputUser);
                this.inputUser = '';
            },
            removeUser(param){
                let ind = this.users.findIndex(user => {
                    return user === param;
                });
                this.users.splice(ind, 1);
            },
        },
    }
</script>

<style scoped>
ul{
    list-style: none;
    margin: 1rem 0;
    padding: 0;
}

li{
    border: 1px solid #ccc;
    padding: 1rem;
    text-align: center;
}

.list-enter-from, .list-leave-to{
  opacity: 0;
  transform: translateX(-30px);
}

.list-enter-active, .list-leave-active{
  transition: all 0.3s ease-out;
}

.list-enter-to, .list-leave-from{
  opacity: 1;
  transform: translateX(30px);
}

.list-move{
    transition: all 2s ease;
}
</style>