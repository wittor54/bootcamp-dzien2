<template>
    <div>
        <h1 class="text-blue-600">Wpisy Bloga:</h1>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="bg-blue-600 rounded text-white p-4">refresh</button>
        </div>

        <div class="grid mx-6 gap-4 my-4">
            <div v-for="(wpis, index) in wpisy" class="drop-shadow-xl bg-stone-300 p-4">
                <p>id: {{index}}</p>
                <p>{{wpis}}</p>
            </div>
            <div class="flex justify-center flex-col">>
                <input v-model="nowyBlog" class="border-2 border-blue-600 p-4" type="text">
                <button  class="bg-blue-600 rounded text-white p-4" @click="dodajWpisy">dodaj</button>
            </div>
        </div>
    </div>
</template>

<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';

export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async dodajWpisy() {
            await dzien2_backend.dodaj_wpis(this.nowyBlog);
        },
        async pobierzWpisy() {
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        }
    },
    async mounted(){
        this.pobierzWpisy()
    }
}
</script>