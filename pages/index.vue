<template>
    <div class="py-4">
        <div class="container">
            <div class="title border-bottom d-flex align-items-center py-4">

                <div class="d-flex">
                    <h5>Task</h5>
                    <div class="form-check form-switch mx-3">
                        <label class="form-check-label" for="toggleShow">
                            Show Finished Task
                        </label>
                        <input
                            class="form-check-input"
                            type="checkbox"
                            role="switch"
                            id="toggleShow"
                            checked
                            v-model="showIfDone"
                        >
                    </div>
                </div>

                <div class="d-flex align-items-center ms-auto">

                    <div class="d-flex align-items-center px-2">
                        <span class="me-2">View As</span>
                        <button
                            class="btn btn-secondary py-1 px-3"
                            @click="isGrid = !isGrid"
                        >
                            {{ isGrid ? 'Grid' : 'List' }}
                        </button>
                    </div>

                    <div class="dropdown d-flex align-items-center px-2">
                        <button class="btn btn-primary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
                            Pilih Kategori
                        </button>
                        <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                            <li><a class="dropdown-item" href="#" @click.prevent="sort()">All</a></li>
                            <li v-for="(task, i) in data_category" :key="i">
                                <a
                                    class="dropdown-item"
                                    href="#"
                                    @click.prevent="sort(data_category[i])"
                                >
                                    {{ data_category[i] }}
                                </a>
                            </li>
                        </ul>
                    </div>

                    <div class="d-flex align-items-center px-2">
                        <input
                            type="text"
                            class="form-control"
                            placeholder="Search"
                            v-model="searchQuery"
                        >
                    </div>
                </div>
            </div>

            <div class="list-task row">
                <div class="text-center py-5" v-if="resultQuery.length == 0">
                    Query not found
                </div>
                <CardItem
                    v-for="(task, i) in resultQuery"
                    :key="i"
                    :task="task"
                    :isGrid="isGrid"
                    :showIfDone="showIfDone"
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
            data_category: ['frontend','backend','database'],
            tasks: [
                {
                    title: 'Event Card',
                    description: 'Buat komponen event card',
                    category: 'frontend',
                    isDone: false,
                },
                {
                    title: 'Event Modal',
                    description: 'Buat komponen event modal',
                    category: 'frontend',
                    isDone: false,
                },
                {
                    title: 'Penyesuaian desain',
                    description: 'Perbaiki desain halaman sesuai figma',
                    category: 'frontend',
                    isDone: false,
                },
                {
                    title: 'Event Controller',
                    description: 'Buat event controller',
                    category: 'backend',
                    isDone: false,
                },
                {
                    title: 'Event Model',
                    description: 'Buat event model',
                    category: 'backend',
                    isDone: false,
                },
                {
                    title: 'Perbaikan Database',
                    description: 'Tambahkan kolom end date pada tabel event',
                    category: 'database',
                    isDone: false,
                },
            ],
            searchQuery: '',
            sortQuery: '',
            isGrid: false,
            showIfDone: true,
            isCreating: false,
        }
    },
    methods:{
        sort(cat){
            this.searchQuery= null
            this.sortQuery = cat
        }
    },
    computed: {
        resultQuery() {
            if (this.searchQuery) {
                this.sortQuery= null
                return this.tasks.filter((item) => {
                    return this.searchQuery
                    .toLowerCase()
                    .split(" ")
                    .every((v) => item.title.toLowerCase().includes(v));
                });
            } else {
                if (this.sortQuery) {
                    return this.tasks.filter((item) => {
                        return this.sortQuery
                        .toLowerCase()
                        .split(" ")
                        .every((v) => item.category.toLowerCase().includes(v));
                    });
                }else{
                    console.log(this.tasks);
                    return this.tasks
                }
            }
        }
    }
}
</script>

<style>

</style>
