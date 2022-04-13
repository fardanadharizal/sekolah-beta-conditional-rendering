<template>
    <div class="py-4">
        <div class="container">
            <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
                <h5>Task</h5>
                <div class="d-flex align-items-center">
                    <span class="me-2">View As</span>
                    <button
                        class="btn btn-outline-secondary py-1 px-3"
                        @click="isGrid = !isGrid"
                    >
                        {{ isGrid ? 'Grid' : 'List' }}
                    </button>
                </div>
            </div>
            <div class="list-task row">
                <div
                    v-for="t in tasks" :key="t"
                    :class="[
                        'item-task d-flex align-items-start border-bottom pt-3 pb-4',
                        isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12'
                    ]"
                >
                    <input
                        type="checkbox"
                        name="status"
                        id="task"
                        class="me-2 mt-2"
                        :checked="t.isDone"
                        v-model="t.isDone"
                    >
                    <div
                        :class="['d-flex flex-column', t.isDone ?
                        'text-decoration-line-through fst-italic' : '']"
                    >
                        <div class="title-task mb-1">{{ this.count }}</div>
                        <div class="description-task small text-muted">
                            {{ t.description}}
                        </div>
                    </div>
                </div>
            </div>
            <div class="action py-2">
                <a
                    href="!#"
                    class="add-button"
                    v-if="!isCreating"
                    @click.prevent="isCreating = !isCreating"
                >
                    Add Task
                </a>
                <div class="add-card" v-else>
                    <div class="card mb-2">
                        <div class="card-body d-flex flex-column p-0">
                            <input class="form-control border-0 mb-2" placeholder="Title" type="text">
                            <textarea class="form-control border-0 small" placeholder="Description"
                            rows="3"></textarea>
                        </div>
                    </div>
                    <div class="button-wrapper d-flex">
                        <button class="btn btn-primary me-2">Save</button>
                        <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
                    </div>
                </div>
            </div>
            <h1>Styling</h1>
            <div class="static" :class="{ active: isActive, 'text-danger': hasError }">style 1</div>
            <div :class="classObject">style 2</div>
            <div :class="[isActive ? activeClass : '', errorClass]">style3</div>
            <div>
                <a @click="inc">Tambahkan {{ num }}</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods:{
        inc(){
            this.num = this.num+15,
            console.log(this.num)
        }
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
            num:15,
            count:1,
            isCreating:false,
            isActive:true,
            hasError:false,
            classObject:{
                active:true,
                'text-danger':true
            },
            activeClass: 'active',
            errorClass: 'text-danger',
            isGrid: false,
        }
    }
}
</script>

<style>
.active{
    background-color: yellow
}
</style>
