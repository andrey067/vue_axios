<template>
    <div>
        <section class="border-b border-gray-800">
            <div class="container p-4 mx-auto flex items-center justify-between">
                <div>
                    <button id="get" type="button" @click="get()"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-purple-700 bg-purple-100 hover:bg-purple-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500">
                        GET
                    </button>

                    <button id="post" type="button"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-green-700 bg-green-100 hover:bg-green-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500">
                        POST
                    </button>

                    <button id="put" type="button"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-blue-700 bg-blue-100 hover:bg-blue-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                        PUT
                    </button>

                    <button id="patch" type="button"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-yellow-700 bg-yellow-100 hover:bg-yellow-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-yellow-500">
                        PATCH
                    </button>

                    <button id="delete" type="button"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-red-700 bg-red-100 hover:bg-red-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500">
                        DELETE
                    </button>

                    <button id="multiple" type="button"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Múltiplos
                    </button>

                    <button id="transform" type="button"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Transform
                    </button>

                    <button id="error" type="button"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Error handling
                    </button>

                    <button id="cancel" type="button"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Cancel
                    </button>
                </div>

                <div>
                    <button id="clear" type="button"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Limpar
                    </button>
                </div>
            </div>
        </section>
        <MainComponent :request="respostaRequest" />
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import apiClient from '@/services/apiclient';
import MainComponent from './MainComponent.vue';
import ResponseData from '@/models/ResponseData';


export default defineComponent({
    name: "SectionComponent",
    data: () => ({
        respostaRequest: {} as ResponseData
    }),
    methods: {
        get() {
            apiClient.get("/posts").then((response: ResponseData) => {
                console.log("response", response);
                this.respostaRequest = response;
            });
        }
    },
    components: { MainComponent }
})
</script>

<style scoped>
</style>