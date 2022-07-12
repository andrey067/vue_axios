<template>
    <div>
        <section class="border-b border-gray-800">
            <div class="container p-4 mx-auto flex items-center justify-between">
                <div>
                    <button id="get" type="button" @click="get()"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-purple-700 bg-purple-100 hover:bg-purple-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500">
                        GET
                    </button>

                    <button id="post" type="button" @click="post()"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-green-700 bg-green-100 hover:bg-green-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500">
                        POST
                    </button>

                    <button id="put" type="button" @click="put()"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-blue-700 bg-blue-100 hover:bg-blue-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                        PUT
                    </button>

                    <button id="patch" type="button" @click="patch()"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-yellow-700 bg-yellow-100 hover:bg-yellow-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-yellow-500">
                        PATCH
                    </button>

                    <button id="delete" type="button" @click="deleted()"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded text-red-700 bg-red-100 hover:bg-red-200 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500">
                        DELETE
                    </button>

                    <button id="multiple" type="button" @click="multipleRequest()"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Múltiplos
                    </button>

                    <button id="transform" type="button" @click="transform()"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Transform
                    </button>

                    <button id="error" type="button" @click="errorhandling"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Error handling
                    </button>

                    <button id="cancel" type="button" @click="cancel()"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Cancel
                    </button>

                    <button id="cancel" type="button" @click="interceptor()"
                        class="inline-flex items-center px-3 py-2 border border-gray-700 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-500 bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        Interceptadores
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
        },
        post() {
            const data = {
                title: 'foo',
                body: 'bar',
                userId: 1
            }
            apiClient.post("/posts", data).then((response) => {
                console.log("response", response);
                this.respostaRequest = response;
            });
        },
        put() {
            const data = {
                title: 'foo2',
                body: 'bar2',
                userId: 1
            }
            apiClient.put("/posts/1", data).then((response) => {
                console.log("response", response);
                this.respostaRequest = response;
            });
        },
        patch() {
            const data = {
                title: 'foo3',
            }
            apiClient.patch("/posts/1", data).then((response) => {
                console.log("response", response);
                this.respostaRequest = response;
            });
        },
        deleted() {
            apiClient.delete("/posts/1").then((response) => {
                console.log("response", response);
                this.respostaRequest = response;
            });
        },
        multipleRequest() {
            Promise.all([
                apiClient.get("/posts"),
                apiClient.get("/users")
            ]).then((response) => {
                console.table(response[0].data)
                console.table(response[1].data)
            })
        },
        transform() {
            const config = {
                transformResponse: [function (data: string) {
                    const payload = JSON.parse(data).map((o: any) => {
                        return {
                            title: o.title
                        }
                    });

                    return payload
                }]
            }
            apiClient.get("/posts", config).then((response) => {
                this.respostaRequest = response;
            })
        },
        errorhandling() {
            apiClient.get("/postsassdas")
                .then((response) => {
                    this.respostaRequest = response;
                })
                .catch((error) => {
                    this.respostaRequest = error.response;
                })

        },
        cancel() {
            const controller = new AbortController();
            const config = {
                signal: controller.signal
            }
            apiClient.get("/posts", config).then((response) => {
                this.respostaRequest = response;
            })
            //Colocar em um buttun para cancelar a request
            controller.abort()
        },
        interceptor() {
            apiClient.interceptors.request.use((config) => {
                console.log(config);
            })
            apiClient.get("/posts").then((response) => {
                this.respostaRequest = response;
            })
        }
    },
    components: { MainComponent }
})
</script>

<style scoped>
</style>