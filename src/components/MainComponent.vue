<template>
    <div>
        <main class="container p-4 mx-auto">
            <div class="grid grid-cols-2 gap-6">
                <div class="col-span-2">
                    <div class="bg-gray-800 rounded-md overflow-hidden">
                        <div class="border-b border-gray-700 px-4 py-3 flex items-center justify-between">
                            <div>Data</div>
                            {{renderOutput}}
                            <div id="status"></div>
                        </div>

                        <div class="p-4">
                            <div class="overflow-y-auto h-96">
                                <pre><code id="data" class="language-js line-numbers"></code></pre>
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
                            <pre><code id="headers" class="language-js line-numbers"></code></pre>
                        </div>
                    </div>
                </div>

                <div class="bg-gray-800 rounded-md overflow-hidden">
                    <div class="border-b border-gray-700 px-4 py-3">
                        Config
                    </div>

                    <div class="p-4">
                        <div class="overflow-y-auto h-96">
                            <pre><code id="config" class="language-js line-numbers"></code></pre>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
// import responseData from '@/models/ResponseData'

export default defineComponent({
    name: "MainComponent",
    props: {
        request: {}
    },
    methods: {
        // renderOutput(response: responseData) {
        // Status
        //const status = response.status;
        // statusEl.removeAttribute('class');
        // let statusElClass = 'inline-flex items-center px-2.5 py-0.5 rounded-md text-sm font-medium';
        // if (status >= 500) {
        //     statusElClass += ' bg-red-100 text-red-800';
        // } else if (status >= 400) {
        //     statusElClass += ' bg-yellow-100 text-yellow-800';
        // } else if (status >= 200) {
        //     statusElClass += ' bg-green-100 text-green-800';
        // }

        // statusEl.innerHTML = status;
        // statusEl.className = statusElClass;

        // Data
        // dataEl.innerHTML = JSON.stringify(response.data, null, 2);
        // Prism.highlightElement(dataEl);

        // Headers
        // headersEl.innerHTML = JSON.stringify(response.headers, null, 2);
        // Prism.highlightElement(headersEl);

        // Config
        // configEl.innerHTML = JSON.stringify(response.config, null, 2);
        // Prism.highlightElement(configEl);
        //},
    },
    computed: {
        renderOutput() {
            console.log(this.request)
            return '';
        }
    }
})
</script>

<style scoped>
</style>