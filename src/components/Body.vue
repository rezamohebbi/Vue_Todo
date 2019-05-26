<template>
    <div>
        <section class="todoapp">
            <header class="header">
                <h1>اطلاعیه ها</h1>
                <input :ref=" 'taskInput' " @keydown.enter="addTask()" class="new-todo" autofocus autocomplete="off" placeholder="اطلاعیه جدید...">
            </header>

            
            <section class="main">
                <input class="toggle-all" type="checkbox">
                <ul class="todo-list">

                    <li v-for=" (task, index) in temp " :class="{completed: task.completed, editing: editItem == task}" :key="index">
                        <div class="view">
                            <input v-model="task.completed" class="toggle" type="checkbox" :checked=" task.completed == true ? 'checked' : '' ">
                            <label @dblclick="startEditingItem(task)">{{ task.title }}</label>
                            <button @click="removeTask(index)" class="destroy"></button>
                        </div>
                        <input @blur="finishEditing(task, index)" @keydown.enter="finishEditing(task, index)" v-model="task.title" class="edit" type="text">
                    </li>

                </ul>
            </section>


            <footer class="footer">
                <span class="todo-count">
                    <strong>{{ temp.length }}</strong> مورد
                </span>
                <ul class="filters">
                    <li><a @click="doFilter('all')" >همه</a></li>
                    <li><a @click="doFilter('active')" >ناتمام ها</a></li>
                    <li><a @click="doFilter('completed')" >انجام شده</a></li>
                </ul>
                <button @click="removeCompletedTasks()" class="clear-completed">
                    پاک کردن منسوخ شده ها
                </button>
            </footer>
        </section>
    </div>
</template>


<script>


export default {
    name: 'app-body',
    data(){
        return {
            tasks: [],
            temp: [],
            editItem: false
        }
    },
    methods: {
        addTask(){
            let newTask = {title: this.$refs.taskInput.value, completed: false};
            if ( !newTask.title.length < 1 ) {
                this.tasks.push(newTask);
                this.$refs.taskInput.value = '';

                this.temp = this.tasks;
            }
            
        },



        doFilter(visibility){
            if ( visibility == 'all' ) {    

                this.temp = this.tasks;

            }else if( visibility == 'active' ){

                // uncompleted actions
                this.temp = this.tasks.filter( (task) => {
                    return task.completed == false;
                } );

            }else{
                this.temp = this.tasks.filter( (task) => {
                    return task.completed == true;
                } );
            }
        },

        startEditingItem(task){
            this.editItem = task;
        },

        finishEditing(task, index){
            if ( !this.editItem )
            {
                return;
            }
            if ( task.title.length < 1 )
            {
                this.removeTask(index);
            }

            this.editItem = false;
        },




        removeTask(pos){
            this.tasks.filter( (value, index) => {
                if ( pos == index ) {
                    this.tasks.splice(index, 1);
                }
            });

            this.temp = this.tasks;
        },
        removeCompletedTasks(){
            let uncompletedTasks = this.tasks.filter( (value, index) => {
                if ( value.completed == true )
                {
                    this.tasks.splice(index, 1);
                }
            });

            this.temp = this.tasks;
        },
    },
}
</script>