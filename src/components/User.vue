<template>
    <div className="user">
        <button @click="deleteUser(index)">Удалить пользователя</button>
        <h3>{{ user.name }}</h3>
        <p>{{ user.email }} - {{ user.pass }}</p>

    </div>
</template>

<style scoped>
.user {
    padding: 20px;
    background-color: #e3e3e3;
    width: 20%;
    border: 1px solid silver;
    margin-bottom: 20px;
    border-radius: 20px;
}

button {
    background-color: darkmagenta;
    color: #fff;
    padding: 10px 16px;
    border-radius: 10px;
    border: none;
    font-weight: bold;
    cursor: pointer;
    float: right;
}
</style>

<script>
// import { defineComponent} from "vue";

export default {
    props: {
        user: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        },
        deleteUser: {
            type: Function,
            required: true
        }
    }

}
</script>