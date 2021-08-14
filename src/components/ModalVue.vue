<template>
  <transition 
        enter-active-class="ease-out duration-300"
        enter-class="opacity-0"
        enter-to-class="opacity-100"
        leave-active-class="ease-in duration-100"
        leave-class="opacity-100"
        leave-to-class="opacity-0"
    >
        <div class="fixed z-10 inset-0 overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true" v-show="modal">
            <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
                <!--
                Background overlay, show/hide based on modal state.

                Entering: "ease-out duration-300"
                    From: "opacity-0"
                    To: "opacity-100"
                Leaving: "ease-in duration-200"
                    From: "opacity-100"
                    To: "opacity-0"
                -->
                <div class="fixed inset-0 bg-gray-300 bg-opacity-75 transition-opacity" aria-hidden="true"></div>

                <!-- This element is to trick the browser into centering the modal contents. -->
                <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

                <!--
                Modal panel, show/hide based on modal state.

                Entering: "ease-out duration-300"
                    From: "opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                    To: "opacity-100 translate-y-0 sm:scale-100"
                Leaving: "ease-in duration-200"
                    From: "opacity-100 translate-y-0 sm:scale-100"
                    To: "opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                -->
                <transition
                enter-active-class="ease-out duration-300"
                enter-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                enter-to-class="opacity-100 translate-y-0 sm:scale-100"
                leave-active-class="ease-in duration-200"
                leave-class="opacity-100 translate-y-0 sm:scale-100"
                leave-to-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                >
                <div class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full" v-show="modal" >
                <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                    <div class="sm:flex sm:items-start">
                    <div class="mx-auto flex-shrink-0 flex items-center justify-center h-12 w-12 rounded bg-yellow-400 sm:mx-0 sm:h-10 sm:w-10">
                        <!-- Heroicon name: outline/exclamation -->
                        <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="-2 -2 104 104" xml:space="preserve"><path d="M80.944,16C81.908,6.669,82,0,82,0H18.001c0,0,0.091,6.669,1.056,16C12.352,16,0,16,0,16v3
                            c0,36.992,26.842,46.346,35.799,48.435c3.146,3.326,6.846,5.603,11.201,6.321V81c0,7-15,13-21,13c-1.656,0-3,1.344-3,3s1.344,3,3,3
                            h24h24c1.656,0,3-1.344,3-3s-1.344-3-3-3c-6,0-21-6-21-13v-7.244c4.355-0.719,8.057-2.994,11.203-6.321
                            C73.162,65.344,100,55.99,100,19v-3C100,16,86.229,16,80.944,16z M6.066,22h13.697c1.598,12.098,4.637,26.756,10.402,37.428
                            C20.676,55.47,7.123,45.693,6.066,22z M55.729,26.102L59.271,37L50,30.265L40.729,37l3.541-10.898L35,19.367h11.459L50,8.469
                            l3.541,10.898H65L55.729,26.102z M69.836,59.428c5.766-10.672,8.805-25.331,10.4-37.428h13.697
                            C92.877,45.693,79.324,55.471,69.836,59.428z"/>
                        </svg>
                    </div>
                    <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                        <h3 class="text-4xl leading-6 font-medium text-gray-900" id="modal-title">
                            Hall of fame
                        </h3>
                        <div class="pt-3 ">
                                <div class="pt-1 w-full bg-white flex items-center justify-between space-x-6 rounded-lg shadow-md cursor-default">
                                    <div>
                                    <h1 class=" text-2xl font-bold text-gray-700 mb-1 mx-2">NAME</h1>
                                    </div>
                                    <div>
                                    <h1 class=" text-2xl font-bold md:ml-48 mb-1 mx-2">SCORE</h1>
                                    </div>
                                </div>
                        </div>
                        <br>
                        <div>
                        <ul class="text-sm text-gray-600" v-for="(user, index) in users" :key="index">
                            <li class=" mb-1">
                                <div class=" items-center ">
                                <div class="pt-1 w-full   bg-white flex items-center justify-between space-x-6 rounded-lg shadow-md hover:scale-105 transition transform duration-500 cursor-default">
                                    <div>
                                    <h1 class=" text-2xl font-bold text-gray-700 mb-1 mx-2">{{user.name}}</h1>
                                    </div>
                                    <div>
                                    <h1 class=" text-2xl font-bold text-gray-700 mb-1 mx-2">{{score(user.times)}}</h1>
                                    </div>
                                    
                                    
                                </div>
                                </div>
                            </li>
                        </ul>
                        </div>
                    </div>
                    </div>
                </div>
                <div class="0 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
                    <button @click="clicked" type="button" class="w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 bg-red-600 text-base font-medium text-white hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500 sm:ml-3 sm:w-auto sm:text-sm">
                    Agree
                    </button>
                    
                </div>
                </div>
                </transition>
            </div>
        </div>
    </transition>
</template>

<script>
import axios from 'axios'

export default {
    beforeUpdate () {
        this.getData();
    },
    data() {
        return {
            users: [],
        }
    },
    props: {
        modal: {
            type: Boolean,
            
        },
    },
    methods: {
        clicked() {
            this.$emit('clicked', false)
        },
        async getData(){
            try {
                let data = await axios.get('https://pomodoro-5cbff-default-rtdb.firebaseio.com/USERS.json')
                let dataDB = await data.data
                this.users = dataDB
                
            } catch (error) {
                
            }
        },
        score(value) {
            let tiempo = 0
            value.map(times => tiempo +=times.timeAcc)
            console.log(value)
            return tiempo
        }
    },
}
</script>

<style>

</style>