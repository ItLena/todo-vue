<template>
    <h2>Add task</h2>
    <div>
        <form v-on:submit.prevent="addTask">
            <input type="text" placeholder="Add task" v-model="taskName">
            <span v-show="!editMood" class="check">Hight priority<input type="checkbox" name="" id="checkbox" v-model="isImportend"></span>
            <button type="submit">Submit</button>
        </form>
    </div>
    <div v-show="submited">
        <h2>Task list</h2>
        <table>
            <thead>
                <tr>
                    <th>Task</th>
                    <th>Status</th>
                    <th>Edit</th>
                    <th>Delete</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(task, index) in taskList" :key="index">
                    <td>{{ task.name }}</td>
                    <td v-if="task.status">
                        <h3 id="red">Importand!!!</h3>
                    </td>
                    <td v-else>
                        <h3 id="grey">To-do</h3>
                    </td>
                    <td @click="editTask(index)">
                        <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-pencil" width="24"
                            height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none"
                            stroke-linecap="round" stroke-linejoin="round">
                            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                            <path d="M4 20h4l10.5 -10.5a2.828 2.828 0 1 0 -4 -4l-10.5 10.5v4" />
                            <path d="M13.5 6.5l4 4" />
                        </svg>
                    </td>
                    <td @click="deleteTask(index)">
                        <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-trash" width="24"
                            height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none"
                            stroke-linecap="round" stroke-linejoin="round">
                            <path stroke="none" d="M0 0h24v24H0z" fill="none" />
                            <path d="M4 7l16 0" />
                            <path d="M10 11l0 6" />
                            <path d="M14 11l0 6" />
                            <path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
                            <path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
                        </svg>
                    </td>
                </tr>

            </tbody>
        </table>
    </div>
</template>


<script>
export default {

    data() {
        return {
            taskName: '',
            isImportend: false,
            taskList: [],
            editedTask: null,
            editMood: false,
            submited: false
        }
    },
    methods: {
        addTask() {
            if (this.taskName.length === 0) return;
            let task = {
                name: this.taskName,
                status: this.isImportend,
            }

            if (this.editedTask === null) {
                this.taskList.push(task);
            }
            else {
                this.taskList[this.editedTask].name = task.name;
                this.editedTask = null;
                this.editMood = false;
                console.log("Updated", this.taskList)
            }

            this.taskName = null;
            this.isImportend = false;
            this.submited = true;
        },
        deleteTask(index) {
            this.taskList.splice(index, 1)
        },
        editTask(index) {
            this.taskName = this.taskList[index].name;
            this.editedTask = index;
            this.editMood = true;
            console.log("Editerar:", this.taskList)
        }

    }
}
</script>


<style>
#red {
    color: red;
    font-weight: bold;
}

#grey {
    color: grey;
}

.check {
    width: 100%;
    padding: 1em;
    display: flex;
    align-content: center;
}

#checkbox {
    width: auto;
    margin-left: 1em;
    cursor: pointer;
    height: 1.8em;
    width: 1.8em;
}</style>