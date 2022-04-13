<template>
    <div class="py-4">
        <div class="container">
            <div class="title border-bottom">
              <h5 class="red">Task</h5>
            </div>
            <div class="list-task">
                <div class="item-task d-flex align-items-center border-bottom pt-3 pb-4">
                    <input type="checkbox" name="status" id="task" class="me-2">
                    <div class="title-task">Tugas 1</div>
                </div>
            </div>
            <div class="action py-2">
                <a href="#" class="add-button">Add Task</a>
            </div>
            <br>
            <h5>{{ msg }}</h5>
            <p>{{ topic }}</p>
            <p v-once>{{msg}}</p>
            <p>Menggunakan kurung kurawal:  {{ rawHtml }}</p>
            <p>Menggunakan v-html direvtive: <span v-html="rawHtml"></span></p>
            <div>
                <button v-bind:disabled="isButtonDisabled">Button</button>
                <br>
                {{ number + 1 }}
                <br>
                {{ msg.split('').reverse().join('') }}\
                <br>
                {{ ok ? 'YES' : 'NO' }}
                <br>
                {{  }}
                <br>
                <div v-bind:id="'list-' + id"></div>
                <br>
                <p v-if="seen">Now you see me</p>
                <br>
                <a v-bind:href="url">href</a>
                <br>
                <a href="#" @click.prevent="doSomething"> on click</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'modul4',
    methods:{
        doSomething(){
            alert('Hari Rabu')
        }
    },
    data(){
        return{
            msg:'selamat datang di surabaya',
            topic:'pertamax naik 1000',
            rawHtml:`
                <div class="py-2">
                    <a href="#" class="add-button">Add task</a>
                </div>
            `,
            isButtonDisabled:true,
            number:100,
            ok:false,
            id:13,
            seen:true,
        }
    }
}
</script>

<style>
/* .red{
  color: blue;
} */
</style>
