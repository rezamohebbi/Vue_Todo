<template>
    <div>
        <section class="todoapp">
            <header class="header">
                <h1>todos</h1>
                <input class="new-todo"
                autofocus autocomplete="off"
                placeholder="چه کاری میخواهی انجام بدهی ؟">
            </header>

            
            <section class="main">
                <input class="toggle-all" type="checkbox">
                <ul class="todo-list">

                    <li class="todo">
                        <div class="view">
                            <input class="toggle" type="checkbox">
                            <label>گرفتن گواهینامه</label>
                            <button class="destroy"></button>
                        </div>
                        <input class="edit" type="text">
                    </li>

                </ul>
            </section>


            <footer class="footer">
                <span class="todo-count">
                    <strong>12</strong> مورد
                </span>
                <ul class="filters">
                    <li><a href="#/all" >همه</a></li>
                    <li><a href="#/active" >فعال</a></li>
                    <li><a href="#/completed" >انجام شده</a></li>
                </ul>
                <button class="clear-completed">
                    ئاک کردن انجام شده ها
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
                {title: "Go to the bank", completed: true},
                {title: "Go to the gym", completed: false},
            ],
        }
    },
}
</script>