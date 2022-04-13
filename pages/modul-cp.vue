<template>
    <div class="py-4">
        <div class="container">
            <div class="title border-bottom d-flex align-items-center py-2">
            <h5>Task</h5>
            <div class="d-flex align-items-center ms-auto">
                <input
                    type="text"
                    class="form-control"
                    placeholder="Search"
                    v-model="searchQuery"
                >
                    <div class="d-flex align-items-center justify-content-end w-100">
                        <span class="me-2">View As</span>
                        <button
                            class="btn btn-outline-secondary py-1 px-3"
                            @click="isGrid = !isGrid"
                        >
                            {{ isGrid ? 'Grid' : 'List' }}
                        </button>
                    </div>
                </div>
            </div>
            <div class="list-task row">
            <CardItem
                v-for="(task, i) in resultQuery"
                :key="i"
                :task="task"
                :isGrid="isGrid"
            />
            </div>
        </div>
    </div>
</template>

<script>

import CardItem from "@/components/Card/CardItem.vue"

export default {
    components: {
        CardItem
    },
    data() {
        return {
            tasks: [
                {
                    title: 'Task 1',
                    description: 'ini deskripsi',
                    isDone: false,
                },
                {
                    title: 'Task 2',
                    description: 'ini deskripsi 2',
                    isDone: false,
                },
                {
                    title: 'Task 3',
                    description: ' ini deskripsi 3',
                    isDone: false,
                }
            ],
            searchQuery: '',
            isCreating: false,
            isGrid: false,
        }
    },
    computed: {
        resultQuery() {
            if (this.searchQuery) {
                return this.tasks.filter((item) => {
                    return this.searchQuery
                    .toLowerCase()
                    .split(" ")
                    .every((v) => item.title.toLowerCase().includes(v));
                });
            } else {
                console.log(this.tasks);
                return this.tasks
            }
        }
    }
};
</script>
