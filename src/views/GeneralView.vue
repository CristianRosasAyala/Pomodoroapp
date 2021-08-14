<template>
    <div>
        <modal-vue :modal="modal" @clicked="closeModal" />
    <div class=" h-screen w-screen flex flex-col pt-2 items-center  bg-red-400">
        <img src="@/assets/trophy.svg" class=" absolute top-5 left-5 w-8 sm:w-12 bg-yellow-200 rounded opacity-80 border-2 border-yellow-400 cursor-pointer" alt="" @click="modal=true">
        
        <img class="relative " src="@/assets/tomato.png" width="300" height="200" alt="">
        <div class=" absolute top-36 border-2 rounded p-3 mx-16 pt-1">
        <p class="text-5xl font-bold text-gray-200">{{time.minutes}} : <span v-show="time.seconds<10">0</span>{{time.seconds}}</p>
        </div>
        
        <transition
            
            leave-active-class="animated bounceOutRight"
            enter-active-class="animated tada"
            leave-to-class="animated tada"
        >
        <div class="flex " v-if="rounds != 4 && (accRestTime===0||accRestTime===300)">
            <button  :class="playC" :disabled="playb" @click="start">
                <svg width="70" height="70" viewBox="0 0 125 125" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M62.5 125C79.076 125 94.9732 118.415 106.694 106.694C118.415 94.9732 125 79.076 125 62.5C125 45.924 118.415 30.0268 106.694 18.3058C94.9732 6.5848 79.076 0 62.5 0C45.924 0 30.0268 6.5848 18.3058 18.3058C6.5848 30.0268 0 45.924 0 62.5C0 79.076 6.5848 94.9732 18.3058 106.694C30.0268 118.415 45.924 125 62.5 125ZM59.0234 40.375C57.8469 39.59 56.4793 39.1392 55.0665 39.0705C53.6538 39.0019 52.2489 39.3181 51.0018 39.9854C49.7547 40.6526 48.7122 41.6459 47.9854 42.8593C47.2586 44.0727 46.8748 45.4606 46.875 46.875V78.125C46.8748 79.5394 47.2586 80.9273 47.9854 82.1407C48.7122 83.3541 49.7547 84.3474 51.0018 85.0146C52.2489 85.6819 53.6538 85.9981 55.0665 85.9295C56.4793 85.8608 57.8469 85.41 59.0234 84.625L82.4609 69C83.5309 68.2865 84.4082 67.32 85.015 66.1861C85.6218 65.0522 85.9392 63.786 85.9392 62.5C85.9392 61.214 85.6218 59.9478 85.015 58.8139C84.4082 57.68 83.5309 56.7135 82.4609 56L59.0234 40.375Z" fill="black" fill-opacity="0.4"/>
                </svg>
            </button>
            <button  :class="pauseC" @click="pause">
                <svg width="70" height="70" viewBox="0 0 141 141" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M70.5 8.8125C36.4342 8.8125 8.8125 36.4342 8.8125 70.5C8.8125 104.566 36.4342 132.188 70.5 132.188C104.566 132.188 132.188 104.566 132.188 70.5C132.188 36.4342 104.566 8.8125 70.5 8.8125ZM59.4844 91.4297C59.4844 92.0355 58.9887 92.5312 58.3828 92.5312H51.7734C51.1676 92.5312 50.6719 92.0355 50.6719 91.4297V49.5703C50.6719 48.9645 51.1676 48.4688 51.7734 48.4688H58.3828C58.9887 48.4688 59.4844 48.9645 59.4844 49.5703V91.4297ZM90.3281 91.4297C90.3281 92.0355 89.8324 92.5312 89.2266 92.5312H82.6172C82.0113 92.5312 81.5156 92.0355 81.5156 91.4297V49.5703C81.5156 48.9645 82.0113 48.4688 82.6172 48.4688H89.2266C89.8324 48.4688 90.3281 48.9645 90.3281 49.5703V91.4297Z" fill="black" fill-opacity="0.4"/>
                </svg>
            </button>
            <button :class="stopC" @click="stop"><svg width="70" height="70"  viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M60 120C75.913 120 91.1742 113.679 102.426 102.426C113.679 91.1742 120 75.913 120 60C120 44.087 113.679 28.8258 102.426 17.5736C91.1742 6.32141 75.913 0 60 0C44.087 0 28.8258 6.32141 17.5736 17.5736C6.32141 28.8258 0 44.087 0 60C0 75.913 6.32141 91.1742 17.5736 102.426C28.8258 113.679 44.087 120 60 120ZM45 37.5C43.0109 37.5 41.1032 38.2902 39.6967 39.6967C38.2902 41.1032 37.5 43.0109 37.5 45V75C37.5 76.9891 38.2902 78.8968 39.6967 80.3033C41.1032 81.7098 43.0109 82.5 45 82.5H75C76.9891 82.5 78.8968 81.7098 80.3033 80.3033C81.7098 78.8968 82.5 76.9891 82.5 75V45C82.5 43.0109 81.7098 41.1032 80.3033 39.6967C78.8968 38.2902 76.9891 37.5 75 37.5H45Z" fill="black" fill-opacity="0.4"/>
                </svg>
            </button>
        </div>
        <div v-else class=" text-3xl text-center">
            <p >Rest for a while...</p>
            <br>
            <p>Recharhing energy... ⚡ {{restTimeCalculation}}</p>
        </div>
        </transition>

        

        <h2 class=" text-5xl mb-10 mt-10">Score: {{time.timeAcc}}</h2>

        
        <transition
            enter-active-class="animated tada"
            leave-to-class="animated tada"
            leave-active-class="animated bounceOutRight"
        >
            <div v-show="rounds === 4">
                <input type="text" class="shadow appearance-none border rounded py-2 px-3 text-grey-darker " v-model.trim="name" autofocus>
                <button class="rounded px-3 py-2 m-1 border-b-4 border-l-2 shadow-lg bg-red-700 border-red-900 text-white" @click="register" >Registrarme!</button>
            </div>
        </transition>
        
        <br>
        <span class=" absolute top-5 right-10 text-4xl text-gray-600"> {{rounds}}</span>
        
        
        
        

    
    </div>
    </div>

</template>

<script>
import axios from 'axios'
import ModalVue from '../components/ModalVue.vue'



export default {
  components: { ModalVue },
  
  
    created () {
        
        console.log('hi')
    },
    data() {
        return {
            show: true,
            time: {
                seconds: 0,
                minutes: 25,
                timeAcc: 0,
            },
            name: '',
            times: [],
            rounds: 0,
            disabledButton: false,
            interval: 0,
            
            playb: false,
            pauseb: false,
            stopb: false,
            restTime: 0,
            accRestTime: 0,
            modal: false,

            

        }
    },
    computed: {
        playC() {
            return (this.playb===false) ? ` text-white font-bold py-2 px-4 rounded mx-2` : ` text-white font-bold py-2 px-4 rounded opacity-50 mx-2 cursor-not-allowed`
        },
        pauseC() {
            return (this.pauseb===false) ? `text-white font-bold py-2 px-4 rounded mx-2` : ` text-white font-bold py-2 px-4 rounded opacity-50 mx-2 cursor-not-allowed` 
        },
        stopC() {
            return (this.stopb===false) ? ` text-white font-bold py-2 px-4 rounded mx-2` : ` text-white font-bold py-2 px-4 rounded opacity-50 mx-2 cursor-not-allowed` 
        },
        restTimeCalculation(){
            return this.accRestTime
        }
    },
    methods: {
        closeModal(value){
            this.modal = value
        },
        async agregarUsuario(){
            try {
                const res = axios.put(`https://pomodoro-5cbff-default-rtdb.firebaseio.com/USERS/${this.name}.json`, {name: this.name, times: this.times})
            } catch (error) {
                console.error(error)
            }
        },
        
        rest(){
            
            this.accRestTime = 0
            this.restTime = setInterval(() => {
                if(this.accRestTime<300){
                    this.accRestTime++
                    console.log(this.accRestTime)
                }else{
                    clearInterval(this.restTime)
                    return
                }
            }, 10);
        },
        register(){
            this.agregarUsuario()
            this.times = []
            this.rounds = 0
            this.name = ''

        },
        start() {
            this.playb = true
            this.time.seconds = 59
            this.time.minutes = 24
            this.interval = setInterval(() => {
                this.time.seconds--
                if(this.time.seconds === 0){
                    this.time.seconds = 60
                    this.time.minutes--
                }

                this.time.timeAcc++
                
                if(this.time.timeAcc == 1500){
                    this.rest()
                    console.log('descansando')
                    clearInterval(this.interval)
                    this.times.push({timeAcc: this.time.timeAcc})
                    console.log(this.times)
                    this.time.seconds = 0
                    this.time.minutes = 0
                    this.time.timeAcc = 0
                    this.playb = false
                    if(this.rounds === 4){
                        this.rounds = 0
                        
                    }else{
                        this.rounds++
                    }

                    return
                }
                    
            }, 1000);
            
        },
        pause() {
            this.playb = false
            this.time.timeAcc = 0
            console.log(this.interval)
            clearInterval(this.interval)
        },
        showTime(){
            console.log(this.time)
        },
        stop(){
            clearInterval(this.interval)
            this.rest()
            this.playb = false
            console.log('STOPED')
            this.times.push({timeAcc: this.time.timeAcc})
            this.time.seconds = 0
            this.time.minutes = 0
            this.time.timeAcc = 0
            if(this.rounds === 4){
                this.rounds = 0
                this.playb = false
                this.pauseb = false
                this.stopb = false
            }else{
                this.rounds++
            }

        }
    },
}
</script>

<style>

</style>