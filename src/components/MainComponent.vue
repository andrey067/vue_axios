<template>
    <div>
        <main class="container p-4 mx-auto">
            <div class="grid grid-cols-2 gap-6">
                <div class="col-span-2">
                    <div class="bg-gray-800 rounded-md overflow-hidden">
                        <div class="border-b border-gray-700 px-4 py-3 flex items-center justify-between">
                            <div>Data</div>
                            <div id="status" :class="statusElClass"></div>
                        </div>

                        <div class="p-4">
                            <div class="overflow-y-auto h-96">
                                <pre class="text-left">{{ dados }}</pre>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-gray-800 rounded-md overflow-hidden">
                    <div class="border-b border-gray-700 px-4 py-3">
                        Headers
                    </div>

                    <div class="p-4">
                        <div class="overflow-y-auto h-96">
                            <pre class="text-left">{{ headers }}</pre>
                        </div>
                    </div>
                </div>

                <div class="bg-gray-800 rounded-md overflow-hidden">
                    <div class="border-b border-gray-700 px-4 py-3">
                        Config
                    </div>

                    <div class="p-4">
                        <div class="overflow-y-auto h-96">
                            <pre class="text-left">{{ config }}</pre>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import responseData from '@/models/ResponseData'

export default defineComponent({
    name: "MainComponent",
    props: {
        request: {}
    },
    data: () => ({
        statusElClass: ''
    }),
    methods: {
        fomateclass(status: number) {
            this.statusElClass = 'inline-flex items-center px-2.5 py-0.5 rounded-md text-sm font-medium';
            if (status >= 500) {
                this.statusElClass += ' bg-red-100 text-red-800';
            } else if (status >= 400) {
                this.statusElClass += ' bg-yellow-100 text-yellow-800';
            } else if (status >= 200) {
                this.statusElClass += ' bg-green-100 text-green-800';
            }
        }
    },
    computed: {
        dados: function () {
            let responsedataformatado = this.request as responseData;
            this.fomateclass(responsedataformatado.status)

            return JSON.stringify(responsedataformatado.data, null, 2);
        },
        headers: function () {
            let responsedataformatado = this.request as responseData;
            return JSON.stringify(responsedataformatado.headers, null, 2);
        },
        config: function () {
            let responsedataformatado = this.request as responseData;
            return JSON.stringify(responsedataformatado.config, null, 2);
        }
    }
})
</script>

<style scoped>
</style>