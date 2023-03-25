<template>
    <div class="wrapper">
        <v-method name="Selection Sort" :array="array" method="selectionSort"></v-method>
        <v-method name="Insertion Sort" :array="array" method="insertionSort"></v-method>
        <v-method name="Merge Sort" :array="array" method="mergeSort"></v-method>
        <v-method name="Heap Sort" :array="array" method="heapSort"></v-method>
        <v-method name="Quick Sort" :array="array" method="quickSort"></v-method>
        <v-method name="Bucket Sort" :array="array" method="bucketSort"></v-method>
    </div>
    <v-footer></v-footer>
</template>

<script>

import VFooter from "@/components/v-Footer";
import VMethod from "@/components/v-Method";

export default {
    name: 'App',
    components: {VMethod, VFooter},
    data() {
        return {
            array: [
                [...Array(100).keys()],
                [...Array(200).keys()],
                [...Array(300).keys()],
                [...Array(400).keys()],
                [...Array(500).keys()],
                [...Array(600).keys()],
                [...Array(700).keys()],
                [...Array(800).keys()],
                [...Array(900).keys()],
                [...Array(1000).keys()],
                [...Array(2000).keys()],
                [...Array(3000).keys()],
                [...Array(4000).keys()],
                [...Array(5000).keys()],
                [...Array(6000).keys()],
                [...Array(7000).keys()],
                [...Array(8000).keys()],
                [...Array(9000).keys()],
                [...Array(10000).keys()],
                [...Array(20000).keys()],
                [...Array(30000).keys()],
                [...Array(40000).keys()],
                [...Array(50000).keys()],
                [...Array(60000).keys()],
                [...Array(70000).keys()],
                [...Array(80000).keys()],
                [...Array(90000).keys()],
                [...Array(100000).keys()],
                [...Array(200000).keys()],
                [...Array(300000).keys()],
                [...Array(400000).keys()],
                [...Array(500000).keys()],
                [...Array(600000).keys()],
                [...Array(700000).keys()],
                [...Array(800000).keys()],
                [...Array(900000).keys()],
            ]
        }
    },
}
</script>

<style lang="scss">
.wrapper {
    max-width: 1140px;
    margin: 0 auto;
    padding: 1rem;
}
</style>
