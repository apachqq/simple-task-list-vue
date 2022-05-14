<template>
    <div class="card">
        <h1 :style="{color: inputValue.length < 5 ? 'darkred' : 'darkblue',
                        fontSize: inputValue.length < 5 ? '2rem' : '1.8rem'}">{{ title }}</h1>
        <div class="form-control">
            <input type="text" :placeholder="placeholderString" v-model="inputValue" @keypress.enter="addNewNote"/>
        </div>
        <button class="btn" @click="addNewNote">Добавить</button>
        <hr/>
        <ul class="list" v-if="notes.length !== 0">
            <transition-group name="post-list">
                <li class="list-item" v-for="(note, idx) in notes" :key="idx">
                    <span :class="['bold', {'primary' : note.length > 5}]">{{ toUpperCase(note) }}</span>
                    <button class="btn danger" v-on:click="removeNote(idx)">Удалить</button>
                </li>
            </transition-group>
            <hr/>
            <li>
                <strong>Общее количество: {{ notes.length }}</strong> | Удвоенное: {{ doubleCountComputed }}
            </li>
        </ul>
        <div v-else>Заметок пока нет. Добавьте первую</div>
    </div>
</template>

<script>
    import AppMixin from '@/mixins/AppMixin'

    export default {
        mixins: [AppMixin]
    }
</script>

<style>
    .list {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    .list-item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0.5rem 0;
    }

    .post-list-item {
        display: inline-block;
        margin-right: 10px;
    }

    .post-list-enter-active,
    .post-list-leave-active {
        transition: all 0.3s ease;
    }

    .post-list-enter-from,
    .post-list-leave-to {
        opacity: 0;
        transform: translateX(130px);
    }
</style>
