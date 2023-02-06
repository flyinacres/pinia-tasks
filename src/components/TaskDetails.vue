<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons">
            <!-- Selecting this class type relates the string name to an icon -->
            <i class="material-icons">delete</i>
            <i class="material-icons">favorites</i>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['task']
    }
</script>