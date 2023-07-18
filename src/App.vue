<template>
    <div class="flex w-full h-screen justify-center items-center">
        <div class="w-full max-w-xl">
            <h1 class="font-bold text-5xl text-center text-indigo-700">Simple Quiz</h1>
            <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-8">
                <div v-if="idx<count">
                    <p class="text-2xl font-bold">
                        {{ ques[idx]['que'] }}
                    </p>
                    <label 
                        :for="key" 
                        class="block mt-4 text-lg border border-gray-300 rounded-lg py-2 px-6"
                        :class="{'hover:bg-gray-100 cursor-pointer': selectedAns==''},
                                {'bg-red-200' : selectedAns == key},
                                {'bg-green-200': key==ques[idx]['ans'] && selectedAns!=''}"
                        v-for="option,key in ques[idx]['options']" >
                        <input 
                            type = "radio"
                            v-bind:id = "key"
                            class = "hidden" 
                            v-bind:value = "key"
                            v-on:change = answered($event) 
                            v-model = "selectedAns"
                            :disabled = "selectedAns != ''"
                        /> 
                            {{ option }}
                    </label>
                    <div class="mt-6 flow-root gap-1">
                        <button class="btn"
                            v-show = "selectedAns != '' && idx< count-1"
                            @click = "nextQue()"> <!-- Vue on-click --> 
                            Next 
                        </button> 
                        <button class="btn"
                            v-if = "selectedAns != '' && idx==count- 1"
                            @click="showResult()">
                            Finish      
                        </button> 
                    </div>
                </div>
                <div v-else>
                    <h2 class="text-bold text-3xl">Result</h2>
                    <div class="flex justify-start space-x-4 mt-6">
                        <p>Correct Answers: <span class="text-2xl text-green-700 font bold">
                            {{ correctAns }}
                        </span></p>
                        <p>Wrong Answers: <span class="text-2xl text-red-700 font bold">
                            {{ wrongAns }}
                        </span></p>
                    </div>
                    <button class="btn"
                        @click="resetQuiz()">
                        Play Again     
                    </button> 
                </div>
            </div>
        </div>
       </div>
</template>

<style scoped>
    .btn {
        @apply float-right px-5 py-2 bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full;
    }
</style>

<script>
export default {
    data(){
        return {
            count: 10, // Count of total number of question
            idx: 0, // index to iterate
            correctAns: 0,
            wrongAns: 0,
            selectedAns:'',
            ques:[
                {
                    que:"What is capital of India?",
                    options:{a:"Mumbai",b:"Ahmedabad",c:"Jaipur",d:"Delhi"},
                    ans:'d'
                },
                {
                    que:"Which one is not a leap year?",
                    options:{a:"2020",b:"3000",c:"2000",d:"2048"},
                    ans:'b'
                },
                {
                    que:"Which is fastestt executable language?",
                    options:{a:"C++",b:"JavaScript",c:"Python",d:"Dart"},
                    ans:'a'
                },
                {
                    que:"Home Minister of India : ",
                    options:{a:"Rahul Gandhi",b:"Narendra Modi",c:"Amit Shah",d:"Arvind Kejariwal"},
                    ans:'c'
                },
                {
                    que:"Which among the following headstreams meets the Ganges in last?",
                    options:{a:"Alaknanda",b:"Pindar",c:"Mandakini",d:"Bhagirathi"},
                    ans:'d'
                },
                {
                    que:"The metal whose salts are sensitive to light is?",
                    options:{a:"Zinc",b:"Silver",c:"Copper",d:"Aluminum"},
                    ans:'b'
                },
                {
                    que:"Patanjali is well known for the compilation of –",
                    options:{a:"Yoga Sutra",b:"Panchatantra",c:"Brahma Sutra",d:"Ayurveda"},
                    ans:'a'
                },
                {
                    que:"River Luni originates near Pushkar and drains into which one of the following?",
                    options:{a:"Rann of Kachchh",b:"Arabian Sea",c:"Gulf of Cambay",d:"Lake Sambhar"},
                    ans:'a'
                },
                {
                    que:"Which one of the following rivers originates in Brahmagiri range of Western Ghats?",
                    options:{a:"China",b:"India",c:"Russia",d:"France"},
                    ans:'c'
                },
                {
                    que:"Tsunamis are not caused by",
                    options:{a:"Hurricanes",b:"Earthquakes",c:"Undersea landslides",d:"Volcanic eruptions"},
                    ans:'a'
                }
            ]
        }
    },
    methods: {
        answered(e){
            this.selectedAns = e.target.value
            if (this.selectedAns==this.ques[this.idx]['ans'])
                this.correctAns++
            else this.wrongAns++
            console.log(this.correctAns+" "+this.wrongAns)
        },
        nextQue(){
            this.idx++
            this.selectedAns = ''
        },
        showResult(){
            this.idx++
        },
        resetQuiz(){
            this.idx = 0
            this.selectedAns = ''
            this.correctAns = 0
            this.wrongAns = 0
        }
    }
};
</script>