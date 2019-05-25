<template>
    <div>
        <section class="todoapp">
            <header class="header">
                <h1>todos</h1>
                <input :ref=" 'taskInput' " @keydown.enter="addTask()" class="new-todo" autofocus autocomplete="off" placeholder="چه کاری میخواهی انجام بدهی ؟">
            </header>

            
            <section class="main">
                <input class="toggle-all" type="checkbox">
                <ul class="todo-list">

                    <li v-for=" (task, index) in tasks " :class="['todo']" :key="index">
                        <div class="view">
                            <input v-model="task.completed" class="toggle" type="checkbox" :checked=" task.completed == true ? 'checked' : '' ">
                            <label>{{ task.title }}</label>
                            <button @click="removeTask(index)" class="destroy"></button>
                        </div>
                        <input class="edit" type="text">
                    </li>

                </ul>
            </section>


            <footer class="footer">
                <span class="todo-count">
                    <strong>{{ tasks.length }}</strong> مورد
                </span>
                <ul class="filters">
                    <li><a @click.prevent="allTasks()" href="#/all" >همه</a></li>
                    <li><a href="#/active" >فعال</a></li>
                    <li><a @click.prevent="completedTasks()" href="#/completed" >انجام شده</a></li>
                </ul>
                <button @click="removeCompletedTasks()" class="clear-completed">
                    پاک کردن انجام شده ها
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
            tasks: [
                
            ],
            temp: [],
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
        completedTasks(){
            this.tasks = this.tasks.filter( (task) => {
                return task.completed == true;
            } );            
        },
        allTasks(){
            this.tasks = this.temp;
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

            // console.log(uncompletedTasks);
            
            
            // this.tasks.forEach((element, index) => {
            //    if ( element.completed == true )
            //    {
            //        this.tasks.splice(index, 1);
            //        console.log("A");
            //    }
            // });

            this.temp = this.tasks;
        },
    },
}
</script>