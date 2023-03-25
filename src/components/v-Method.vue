<template>
    <div class="method">
        <div class="method__title">
            <div class="method__name">{{ name }}</div>
            <div class="method__time" v-if="calculate">calc</div>
        </div>
        <div class="method__options">
            <v-select class="method__select" @selectOption="optionSelect($event, 'selectedOption')"
                      v-model:selectedOption="selectedOption"
                      :options="array"
                      style-type="select"></v-select>
            <button class="method__button" @click="handle_function_call()">Расчитать
            </button>
<!--            <button class="method__button" @click="allSort()">Расчитать всё</button>-->
        </div>
        <div class="method__results" v-if="resultArray.length > 0">
            <table>
                <thead>
                    <tr>
                        <td>Величина массива</td>
                        <td>Время выполнения</td>
                    </tr>
                </thead>
                <tbody>
                    <tr class="method__result" v-for="result in resultArray" :key="result.timeValue">
                        <td>{{ result.arrayCount }}</td>
                        <td>{{ result.timeValue }}ms</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import VSelect from "@/components/v-Select";

export default {
    components: {VSelect},
    data() {
        return {
            calculate: false,
            selectedOption: 0,
            resultArray: []
        }
    },
    props: {
        array: {
            type: Array
        },
        name: {
            type: String
        },
        method: {
            type: String
        }
    },
    methods: {
        handle_function_call() {
            this.calculate = true;
            this.resultArray = []
            this[this.method](this.array[this.selectedOption])
            this.calculate = false;
        },
        optionSelect(option, select) {
            this[select] = option;
        },
        allSort() {
            this.resultArray = []
            for (let arr in this.array) {
                setTimeout(() => {
                    this[this.method](this.shuffleArray(this.array[arr]))
                }, 500)
            }
        },
        selectionSort(array) {
            this.shuffleArray(array)
            let startTime = performance.now();
            for (let i = 0; i < array.length; i++) {
                for (let j = i + 1; j < array.length; j++) {
                    if (array[i] > array[j]) {
                        [array[i], array[j]] = [array[j], array[i]]
                    }
                }
            }
            let endTime = performance.now();
            this.resultArray.push({arrayCount: array.length, timeValue: (endTime - startTime).toFixed(2)})
        },

        insertionSort(array) {
            this.shuffleArray(array);
            let startTime = performance.now();
            for (let i = 1, l = array.length; i < l; i++) {
                const current = array[i];
                let j = i;
                while (j > 0 && array[j - 1] > current) {
                    array[j] = array[j - 1];
                    j--;
                }
                array[j] = current;
            }
            let endTime = performance.now();
            this.resultArray.push({arrayCount: array.length, timeValue: (endTime - startTime).toFixed(2)})
        },

        mergeSort(array) {
            this.shuffleArray(array);

            function merge(arr1, arr2) {
                let i = 0;
                let j = 0;
                let results = [];
                while (i < arr1.length && j < arr2.length) {
                    if (arr2[j] > arr1[i]) {
                        results.push(arr1[i]);
                        i++;
                    } else {
                        results.push(arr2[j])
                        j++
                    }
                }
                while (i < arr1.length) {
                    results.push(arr1[i]);
                    i++;
                }
                while (j < arr2.length) {
                    results.push(arr2[j]);
                    j++;
                }
                return results
            }

            function mergeSort(array) {
                if (array.length <= 1) return array;

                let mid = Math.floor(array.length / 2);
                let left = mergeSort(array.slice(0, mid));
                let right = mergeSort(array.slice(mid));
                return merge(left, right);
            }

            let startTime = performance.now();
            mergeSort(array)
            let endTime = performance.now();
            this.resultArray.push({arrayCount: array.length, timeValue: (endTime - startTime).toFixed(2)})
        },

        heapSort(array) {
            this.shuffleArray(array);
            const maxHeapify = (arr, n, i) => {
                let largest = i;
                let l = 2 * i + 1; //left child index
                let r = 2 * i + 2; //right child index
                //If left child is smaller than root
                if (l < n && arr[l] > arr[largest]) {
                    largest = l;
                }
                // If right child is smaller than smallest so far
                if (r < n && arr[r] > arr[largest]) {
                    largest = r;
                }
                // If smallest is not root
                if (largest !== i) {
                    let temp = arr[i];
                    arr[i] = arr[largest];
                    arr[largest] = temp;

                    // Recursively heapify the affected sub-tree
                    maxHeapify(arr, n, largest);
                }
            }
            // main function to do heap sort
            const heapS = (arr, n) => {
                // Build heap (rearrange array)
                for (let i = n / 2 - 1; i >= 0; i--) {
                    maxHeapify(arr, n, i);
                }

                // One by one extract an element from heap
                for (let i = n - 1; i >= 0; i--) {
                    // Move current root to end
                    let temp = arr[0];
                    arr[0] = arr[i];
                    arr[i] = temp;

                    // call max heapify on the reduced heap
                    maxHeapify(arr, i, 0);
                }
            }
            let startTime = performance.now();
            heapS(array, array.length)
            let endTime = performance.now();
            this.resultArray.push({arrayCount: array.length, timeValue: (endTime - startTime).toFixed(2)})
        },

        quickSort(array) {
            this.shuffleArray(array);

            function QuickSort(List) {
                if (List.length <= 1) {
                    return List;
                }
                const pivot = List[List.length - 1];
                const leftList = [];
                const rightList = [];

                for (let i = 0; i < List.length - 1; i++) {
                    if (List[i] < pivot) {
                        leftList.push(List[i]);
                    } else {
                        rightList.push(List[i])
                    }
                }

                return [...QuickSort(leftList), pivot, ...QuickSort(rightList)];
            }

            let startTime = performance.now();
            QuickSort(array);
            let endTime = performance.now();
            this.resultArray.push({arrayCount: array.length, timeValue: (endTime - startTime).toFixed(2)})
        },

        bucketSort(array) {
            this.shuffleArray(array);

            function insertionSort(array) {
                let length = array.length;

                for (let i = 1; i < length; i++) {
                    let temp = array[i];
                    let j
                    for (let j = i - 1; j >= 0 && array[j] > temp; j--) {
                        array[j + 1] = array[j];
                    }
                    array[j + 1] = temp;
                }

                return array;
            }

            function bucketSort(array, bucketS) {
                if (array.length === 0) {
                    return array;
                }
                // Declaring vars
                let i, minValue = array[0], maxValue = array[0]
                let bucketSize = bucketS || 5;
                // Setting min and max values
                array.forEach(function (currentVal) {
                    if (currentVal < minValue) {
                        minValue = currentVal;
                    } else if (currentVal > maxValue) {
                        maxValue = currentVal;
                    }
                })
                // Initializing buckets
                let bucketCount = Math.floor((maxValue - minValue) / bucketSize) + 1;
                let allBuckets = new Array(bucketCount);

                for (i = 0; i < allBuckets.length; i++) {
                    allBuckets[i] = [];
                }
                // Pushing values to buckets
                array.forEach(function (currentVal) {
                    allBuckets[Math.floor((currentVal - minValue) / bucketSize)].push(currentVal);
                });
                // Sorting buckets
                array.length = 0;

                allBuckets.forEach(function (bucket) {
                    insertionSort(bucket);
                    bucket.forEach(function (element) {
                        array.push(element)
                    });
                });

                return array;
            }

            let startTime = performance.now();
            bucketSort(array);
            let endTime = performance.now();
            this.resultArray.push({arrayCount: array.length, timeValue: (endTime - startTime).toFixed(2)})
        },


        // Рандомизация значений в массиве
        shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }
    }
}
</script>

<style scoped lang="scss">
.method {
    align-items: center;
    border-radius: 10px;
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.1), 0 10px 10px rgba(0, 0, 0, 0.2);
    padding: 2rem;
    max-width: 60%;
    margin: 5rem auto;

    &__title {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    &__name {
        font-size: 2rem;
        margin-bottom: 2rem;
    }

    &__options {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    &__select {
        width: 10rem;
        height: 3rem;
        font-size: 1.5rem;
    }

    &__button {
        cursor: pointer;
        background: #cde4f5;
        border-radius: 20px;
        font-size: 1.3rem;
        border: none;
        padding: 0.8rem 1rem;
        transition: 0.4s;

        &:hover {
            border-radius: 20px;
            background: #a8d1f0;
        }
    }

    &__results {
        margin-top: 1rem;
        border-top: 1px solid grey;

        table {
            margin-top: 1rem;
            border: 2px solid grey;
            border-collapse: collapse;

            th, td {
                padding: 0.5rem;
                border: 1px solid grey;
            }
        }
    }
}

@media (max-width: 900px) {
    .method {
        &__name {
            font-size: 1.5rem;
        }

        &__options {
            flex-direction: column;
        }

        &__select {
            width: 100%;
        }

        &__button {
            width: 100%;
            font-size: 1rem;
            margin-top: 1rem;
        }
    }
}
</style>