<template>
    <div class="task">
        <input class="task__input" v-model="newValue" :readonly="onEdit" type="text">
        <div class="buttons">
            <button @click="edit" v-if="onEdit" class="btn btn--edit">Редактировать</button>
            <button @click="save(value)" v-else class="btn btn--save">Сохранить</button>
            <button @click="removeTask(newValue)" class="btn btn--delete">Удалить</button>
        </div>
    </div>
</template>

<script>
export default {
    props: ['value', 'removeTask', 'editTask'],
    data(){
        return {
            onEdit: true,
            oldValue: this.value,
            newValue: this.value
        }
    },
    methods: {
        edit(){
            this.onEdit = false
        },
        save(){
            this.onEdit = true
            this.editTask(this.oldValue, this.newValue)
            this.oldValue = this.newValue
        }
    }
}
</script>

<style scoped>
.task {
    padding: 15px;
    display: flex;
    justify-content: space-between;
    border: 1px solid #41B883;
}

.task__input {
    padding: 10px;
    width: 900px;
}

.buttons {
    display: flex;
    gap: 10px;
}

.btn {
    width: 150px;
}
.btn--edit {
    background-color: #4161b8;
}

.btn--save {
    background-color: #acb841;
}

.btn--delete {
    background-color: #b84141;
}
</style>