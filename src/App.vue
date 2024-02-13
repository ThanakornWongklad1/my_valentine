<script setup>
import { IconHeartFilled, IconChevronLeft } from '@tabler/icons-vue';
import { ref } from 'vue';
import QrcodeVue from 'qrcode.vue'


const openMessage = ref(false);
const page = ref('');
const qrcodeData = ref()

const food = ref()
const moreFood = ref()
const sumFood = ref()
const state1 = ref(false)
const submitFood = () => {
    if (food.value !== undefined) {
        if (food.value === 'อื่นๆ') {
            console.log(moreFood.value)
            if (moreFood.value !== undefined && moreFood.value !== '') {
                sumFood.value = moreFood.value
            } else {
                sumFood.value = 'อะไรก็ได้'
            }
        }
        else {
            sumFood.value = food.value
        }
        state1.value = true
    }
    console.log(sumFood.value)
}

const activity = ref()
const moreActivity = ref()
const sumActivity = ref()
const state2 = ref(false)
const submitActivity = () => {
    if (activity.value !== undefined) {
        if (activity.value === 'อื่นๆ') {
            console.log(moreActivity.value)
            if (moreActivity.value !== undefined && moreActivity.value !== '') {
                sumActivity.value = moreActivity.value
            } else {
                sumActivity.value = 'อะไรก็ได้'
            }
        }
        else {
            sumActivity.value = activity.value
        }
        state2.value = true
    }
    console.log(sumActivity.value)
}

const place = ref()
const morePlace = ref()
const sumPlace = ref()
const state3 = ref(false)

const submitPlace = () => {
    if (place.value !== undefined) {
        if (place.value === 'อื่นๆ') {
            console.log(morePlace.value)
            if (morePlace.value !== undefined && morePlace.value !== '') {
                sumPlace.value = morePlace.value
            } else {
                sumPlace.value = 'ไปไหนก็ได้'
            }
        }
        else {
            sumPlace.value = place.value
        }
        state3.value = true
        qrcodeData.value = `food=${sumFood.value}&activity=${sumActivity.value}&place=${sumPlace.value}`
    }
    console.log(sumPlace.value)
}


</script>
 
<template>
    <div class="body w-full h-svh bg-gradient-to-r from-[#ffebf9] to-[#ffdff6]">
        <div v-show="page === ''">
            <div class="text-center text-rose-500 pt-10" style="letter-spacing: 4px; font-size: 28px;">Will you be my
                valentine?
            </div>
            <div class="flex flex-col pt-24 md:pt-36">
                <div class="note bg-amber-100 mx-4 rounded-lg shadow-xl p-4 pb-5" v-show="openMessage">
                    <div class="font-semibold pb-3 text-lg">Hi, My love</div>
                    <div class="indent-5">
                        วาเลนไทน์ปีนี้เค้าอาจจะไม่ได้มีดอกไม้ให้เธอและไปหาเธอไม่ทันวันวาเลนไทน์
                        แต่เค้าตั้งใจทำเว็บนี้ขึ้นมาให้เธอแทน ซึ่งเค้าหวังว่าเธอจะชอบนะ
                        หน้าต่อไปนี้เค้าจะให้เธอเลือกว่าวันที่เค้าไปหาเธออยากให้เค้าพาไปที่ไหน อยากทำอะไร และอยากกินอะไร
                    </div>
                    <div class="pt-2 px-4">to jomjam &lt;3 </div>
                    <div class="flex justify-center mt-10">
                        <button class="px-3 py-2 bg-amber-500 rounded-lg" @click="page = 'page2'">go</button>
                    </div>
                </div>
                <div class="flex justify-center">
                    <div class="text-center absolute top-48">
                        <IconHeartFilled class="icon-pulse text-red-500 mx-auto" size="55"
                            @click="openMessage = !openMessage" />
                        <p v-show="!openMessage">click me!</p>
                    </div>
                </div>
            </div>
            <div class="flex justify-center mt-32" v-show="!openMessage">
                <img src="./assets/cat.gif" alt="" class="w-60 rounded-xl">
            </div>
        </div>
        <div v-show="page === 'page2'">
            <div class="text-center text-rose-500 pt-10" style="letter-spacing: 4px; font-size: 28px;">Will you be my
                valentine?
            </div>
            <div class="p-10 relative">
                <img src="./assets/couple1.jpeg" class="pic w-40 rounded-2xl border-8 border-white">
                <img src="./assets/couple4.jpeg"
                    class="pic w-40 rounded-2xl border-8 border-white absolute right-14 top-52">
                <img src="./assets/couple5.jpeg" class="pic w-36 rounded-2xl border-8 border-white absolute left-16 top-72">
            </div>
            <div class="flex justify-center ">
                <button @click="page = 'page3'"
                    class="w-8/12 py-2 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg absolute bottom-10 text-white">next!</button>
            </div>
        </div>
        <div v-show="page === 'page3'">
            <div class="w-full bg-gradient-to-r from-[#ffb2e8] to-[#fd8fde] py-5  text-white flex rounded-b-2xl">
                <IconChevronLeft class="my-auto text-white mx-5" @click="page = 'page2'" />
                <div class="text-lg font-semibold">What food would you like to eat?</div>
            </div>
            <div class="bg-white mt-5 p-4 ml-5 rounded-b-xl rounded-r-xl w-8/12">
                <div class="font-semibold">pick one or more</div>
                <div class="py-2 flex flex-col">
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="SuperSoup" id="SuperSoup" :disabled="state1"
                            v-model="food"><label for="SuperSoup">Super
                            Soup</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="หมูกระทะ" id="หมูกระทะ" :disabled="state1"
                            v-model="food"><label for="หมูกระทะ">หมูกระทะ</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="ชาบู" id="ชาบู" :disabled="state1"
                            v-model="food"><label for="ชาบู">ชาบู</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="พิซซ่า" id="พิซซ่า" :disabled="state1"
                            v-model="food"><label for="พิซซ่า">พิซซ่า</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="ก๋วยเตี๋ยว" id="ก๋วยเตี๋ยว" :disabled="state1"
                            v-model="food"><label for="ก๋วยเตี๋ยว">ก๋วยเตี๋ยว</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="อื่นๆ" id="อื่นๆ" :disabled="state1"
                            v-model="food"><label for="อื่นๆ">อื่นๆ</label>
                    </div>
                    <div class="mb-5 ml-7" v-show="food === 'อื่นๆ'">
                        <input type="text" id="more" class="border rounded-lg p-3 w-full" placeholder="more..."
                            v-model="moreFood" :disabled="state1">
                    </div>

                    <div @click="submitFood()" class="p-3 mt-3 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg">
                        submit
                    </div>
                </div>
            </div>
            <div v-show="state1" class="flex justify-end">
                <div class="bg-white p-4 mr-5 mt-5 rounded-b-xl rounded-l-xl">I wanna eat {{ sumFood }} with u</div>
            </div>
            <div class="flex justify-center" v-show="state1">
                <button @click="page = 'page4'"
                    class="w-8/12 py-2 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg absolute bottom-10 text-white">next!</button>
            </div>
        </div>
        <div v-show="page === 'page4'">
            <div class="w-full bg-gradient-to-r from-[#ffb2e8] to-[#fd8fde] py-5  text-white flex rounded-b-2xl">
                <IconChevronLeft class="my-auto text-white mx-5" @click="page = 'page3'" />
                <div class="text-lg font-semibold">What would you like to do with me?</div>
            </div>
            <div class="bg-white mt-5 p-4 ml-5 rounded-b-xl rounded-r-xl w-8/12">
                <div class="font-semibold">pick one or more</div>
                <div class="py-2 flex flex-col">
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="ดูซีรี่ย์" id="ดูซีรี่ย์" :disabled="state2"
                            v-model="activity"><label for="ดูซีรี่ย์">ดูซีรี่ย์</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="ออกกำลังกาย" id="ออกกำลังกาย" :disabled="state2"
                            v-model="activity"><label for="ออกกำลังกาย">ออกกำลังกาย</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="ทำอาหาร" id="ทำอาหาร" :disabled="state2"
                            v-model="activity"><label for="ทำอาหาร">ทำอาหาร</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="ทำเค้กวันครบรอบ" id="ทำเค้กวันครบรอบ"
                            :disabled="state2" v-model="activity"><label for="ทำเค้กวันครบรอบ">ทำเค้กวันครบรอบ</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="อื่นๆ" id="อื่นๆ" :disabled="state2"
                            v-model="activity"><label for="อื่นๆ">อื่นๆ</label>
                    </div>
                    <div class="mb-5 ml-7" v-show="activity === 'อื่นๆ'">
                        <input type="text" id="more" class="border rounded-lg p-3 w-full" placeholder="more..."
                            v-model="moreActivity" :disabled="state2">
                    </div>

                    <div @click="submitActivity()" class="p-3 mt-3 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg">
                        submit
                    </div>
                </div>

            </div>
            <div v-show="state2" class="flex justify-end">
                <div class="bg-white p-4 mr-5 mt-5 rounded-b-xl rounded-l-xl">I wanna {{ sumActivity }} with u</div>
            </div>
            <div class="flex justify-center" v-show="state2">
                <button @click="page = 'page5'"
                    class="w-8/12 py-2 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg absolute bottom-10 text-white">next!</button>
            </div>
        </div>
        <div v-show="page === 'page5'">
            <div class="w-full bg-gradient-to-r from-[#ffb2e8] to-[#fd8fde] py-5  text-white flex rounded-b-2xl">
                <IconChevronLeft class="my-auto text-white mx-5" @click="page = 'page3'" />
                <div class="text-lg font-semibold">What would you like to go with me?</div>
            </div>
            <div class="bg-white mt-5 p-4 ml-5 rounded-b-xl rounded-r-xl w-8/12">
                <div class="font-semibold">pick one or more</div>
                <div class="py-2 flex flex-col">
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="หาดวอน" id="หาดวอน" :disabled="state3"
                            v-model="place"><label for="หาดวอน">หาดวอน</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="parkin" id="parkin" :disabled="state3"
                            v-model="place"><label for="parkin">parkin</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="mi-xue" id="mi-xue" :disabled="state3"
                            v-model="place"><label for="mi-xue">mi-xue</label>
                    </div>
                    <div class="flex my-1">
                        <input class="mx-2 my-auto" type="radio" value="อื่นๆ" id="อื่นๆ" :disabled="state3"
                            v-model="place"><label for="อื่นๆ">อื่นๆ</label>
                    </div>
                    <div class="mb-5 ml-7" v-show="place === 'อื่นๆ'">
                        <input type="text" id="more" class="border rounded-lg p-3 w-full" placeholder="more..."
                            v-model="morePlace" :disabled="state3">
                    </div>

                    <div @click="submitPlace()" class="p-3 mt-3 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg">
                        submit
                    </div>
                </div>

            </div>
            <div v-show="state3" class="flex justify-end">
                <div class="bg-white p-4 mr-5 mt-5 rounded-b-xl rounded-l-xl">I wanna go {{ sumPlace }} with u</div>
            </div>
            <div class="flex justify-center" v-show="state3">
                <button @click="page = 'page6'"
                    class="w-8/12 py-2 bg-gradient-to-r from-[#ffc1ec] to-[#fd8fde] rounded-lg absolute bottom-10 text-white">next!</button>
            </div>
        </div>
        <div v-show="page === 'page6'">
            <div id="thankyou" class="text-center text-rose-500 pt-10" style="letter-spacing: 4px; font-size: 28px;">
                Thank you for being my girlfriend
            </div>
            <div class="flex justify-center">
                <QrcodeVue :value="qrcodeData" :size="180" level="Q" class="absolute top-48" />
                <div class="absolute top-96">Capture this and sent to your boyfriend.</div>
            </div>
            <!-- flower -->
            <div class="flex justify-center pt-32">
                <div class="flower">
                    <div class="f-wrapper">
                        <div class="flower__line"></div>
                        <div class="f">
                            <div class="flower__leaf flower__leaf--1"></div>
                            <div class="flower__leaf flower__leaf--2"></div>
                            <div class="flower__leaf flower__leaf--3"></div>
                            <div class="flower__leaf flower__leaf--4"></div>
                            <div class="flower__leaf flower__leaf--5"></div>
                            <div class="flower__leaf flower__leaf--6"></div>
                            <div class="flower__leaf flower__leaf--7"></div>
                            <div class="flower__leaf flower__leaf--8 flower__fall-down--yellow"></div>
                        </div>
                    </div>

                    <div class="f-wrapper f-wrapper--2">
                        <div class="flower__line"></div>
                        <div class="f">
                            <div class="flower__leaf flower__leaf--1"></div>
                            <div class="flower__leaf flower__leaf--2"></div>
                            <div class="flower__leaf flower__leaf--3"></div>
                            <div class="flower__leaf flower__leaf--4"></div>
                            <div class="flower__leaf flower__leaf--5"></div>
                            <div class="flower__leaf flower__leaf--6"></div>
                            <div class="flower__leaf flower__leaf--7"></div>
                            <div class="flower__leaf flower__leaf--8 flower__fall-down--pink"></div>
                        </div>
                    </div>

                    <div class="f-wrapper f-wrapper--3">
                        <div class="flower__line"></div>
                        <div class="f">
                            <div class="flower__leaf flower__leaf--1"></div>
                            <div class="flower__leaf flower__leaf--2"></div>
                            <div class="flower__leaf flower__leaf--3"></div>
                            <div class="flower__leaf flower__leaf--4"></div>
                            <div class="flower__leaf flower__leaf--5"></div>
                            <div class="flower__leaf flower__leaf--6"></div>
                            <div class="flower__leaf flower__leaf--7"></div>
                            <div class="flower__leaf flower__leaf--8 flower__fall-down--purple"></div>
                        </div>
                    </div>
                    <div class="flex justify-center">
                        <div class="flower__glass flex"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
 
<style scoped>
.body {
    background-color: #ffd778;
}

.icon-pulse {
    animation: pulse 1s infinite;
}

@keyframes pulse {
    0% {
        transform: scale(1);
        transform: sca;
    }

    50% {
        transform: scale(1.2);
    }

    100% {
        transform: scale(1);
    }
}

.pic {
    animation: pulse 5s infinite;
}

@keyframes pulse {
    0% {
        transform: scale(1);
    }

    50% {
        transform: scale(1.1);
    }

    100% {
        transform: scale(1);
    }
}

.note {
    animation: fadeIn 1s;
}

@keyframes fadeIn {
    0% {
        transform: scaleY(0);
    }

    100% {
        transform: scaleY(1);
    }
}

#thankyou {
    position: relative;
    /* Adjust based on layout needs */
    margin-bottom: 400px;
    font-size: 50px;
}

.flower {
    position: relative;
}

.flower__glass {
    width: 30vmin;
    height: 100px;
    background-image: var(--color-glass);
    clip-path: polygon(0 0, 100% 0, 85% 100%, 15% 100%);
    opacity: .8;
    position: relative;
}

.flower__glass::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    background-color: #182843;
    width: 100%;
    height: 100%;
}

.flower__glass::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    background-image: var(--color-water);
    width: 100%;
    height: 100%;

}

.f-wrapper {
    position: absolute;
    left: 45%;
    bottom: 2vmin;
}

.f-wrapper--2 {
    left: 50%;
    bottom: 5%;
    transform-origin: 10% left;
    transform: rotate(20deg);
}

.f-wrapper--3 {
    left: 30%;
    bottom: 5%;
    transform-origin: 10% left;
    transform: rotate(-10deg);
}

.f-wrapper--3 .flower__line {
    height: 45vmin;
    position: relative;
}

.f-wrapper--3 .flower__line::after {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    width: 6vmin;
    height: 6vmin;
    transform: translate(-69%, -30%) rotate(-5deg);
    border-radius: 10vmin 10vmin 0 0;
    border: 2vmin solid #104d4e;
    border-bottom: transparent;
    border-left: transparent;
}

.f-wrapper--3 .flower__line::before {
    content: '';
    position: absolute;
    left: -40%;
    top: -1%;
    width: 6vmin;
    height: 2vmin;
    transform-origin: right;
    transform: translate(-100%, -80%) rotate(-20deg);
    background-color: #104d4e;
    border-radius: 2vmin;
}

.f-wrapper--3 .flower__line {
    background-image: linear-gradient(to top, #142544, #104d4e);
}


.f-wrapper--2 .flower__line {
    height: 45vmin;
}

.f-wrapper--2 .f {
    transform: translateX(-50%) rotate(20deg);
}

.f-wrapper--3 .f {
    transform: translate(-350%, -50%) rotate(-120deg);
}

.f-wrapper--2 .flower__leaf:not(:first-child) {
    width: 3.8vmin;
    height: 10vmin;
    background-image: linear-gradient(to bottom, #ff43b6, #c22887, #1a233a 99%);
}

.f-wrapper--3 .flower__leaf:not(:first-child) {
    width: 3.8vmin;
    height: 10vmin;
    background-image: linear-gradient(to bottom, #ad2be0, #712291, #1a233a 99%);
}

.f-wrapper--3 .flower__leaf--1 {
    width: 8vmin;
    height: 10vmin;
    bottom: 2vmin;
    background-color: #ad2be0;
}

.f-wrapper--2 .flower__leaf--1 {
    width: 8vmin;
    height: 10vmin;
    bottom: 2vmin;
    background-color: #de118b;
}

.f-wrapper--2 .f .flower__leaf--8 {
    width: 10vmin;
    height: 9vmin;
    bottom: 3vmin;
    left: -30%;
    transform: rotate(-50deg);
    background-image: linear-gradient(to left bottom, #ff43b6, #4d1337);
    ;
}

.f-wrapper--3 .f .flower__leaf--8 {
    width: 10vmin;
    height: 9vmin;
    left: -10% !important;
    background-image: linear-gradient(to left bottom, #ad2be0, #712291);
    ;
}

.flower__line {
    width: 2vmin;
    height: 56vmin;
    background-image: linear-gradient(to left top, #82fdff 20%, #142544, #104d4e);
    border-radius: 4vmin;
}

.f {
    position: absolute;
    top: 1vmin;
    left: 50%;
    transform: translateX(-50%) rotate(-10deg);
    width: 2vmin;
    height: 2vmin;
}


.flower__leaf {
    position: absolute;
    left: 50%;
    bottom: 2vmin;
    transform: translateX(-50%);
    width: 5vmin;
    height: 14vmin;
    background-image: linear-gradient(to bottom, #ffa085, #fa7373, #1a233a 99%);

    clip-path: ellipse(50% 50% at 50% 50%);
    transform-origin: center bottom;
    animation: open-flower 2s 1s backwards;
}

.flower__leaf--1 {
    width: 10vmin;
    height: 12vmin;
    bottom: 3vmin;
    border-radius: 50% 50% 50% 50% / 80% 80% 20% 20%;
    background-color: #e24f5f;
    background-image: none;
    animation: open-flowe--middle 1.4s 1s backwards;
}

.flower__leaf--2 {
    transform: translateX(-50%) rotate(-30deg);
}

.flower__leaf--3 {
    transform: translateX(-50%) rotate(-50deg);
}

.flower__leaf--4 {
    transform: translateX(-50%) rotate(-70deg);
}

.flower__leaf--5 {
    transform: translateX(-50%) rotate(30deg);
}

.flower__leaf--6 {
    transform: translateX(-50%) rotate(50deg);
}

.flower__leaf--7 {
    transform: translateX(-50%) rotate(70deg);
}

.flower__leaf--8 {
    width: 13vmin;
    height: 11vmin;
    bottom: 6vmin;
    left: -30%;
    border-radius: none;
    clip-path: none;
    border-radius: 10vmin 2vmin 10vmin 2vmin;
    transform: rotate(-55deg);
    background-image: linear-gradient(to left bottom, #ffa085, #eb8b8b, #492f2f 98%);
}

.flower__fall-down--yellow {
    animation: flower-fall-down-yellow 8s 1.2s linear forwards;
}

.flower__fall-down--pink {
    animation: flower-fall-down-pink 5s 1.2s linear forwards;
}

.flower__fall-down--purple {
    bottom: 4vmin;
    animation: flower-fall-down-purple 6s 1.2s linear forwards, flower-falling 6s 7.2s linear infinite;
}


@keyframes open-flower {
    0% {
        transform: translateX(-50%) rotate(0);
    }
}

@keyframes open-flowe--middle {
    0% {
        opacity: 0;
        transform: translateX(-50%) scale(0);
    }
}

@keyframes flower-fall-down-pink {

    0% {
        transform: rotate(-55deg);
    }

    50% {
        transform: rotateX(-100deg);
    }

    100% {
        transform: translate(2vmin, 28vmin);
    }

}

@keyframes flower-fall-down-yellow {

    0% {
        transform: rotate(-55deg);
    }

    50% {
        bottom: 3vmin;
        transform: rotateX(-100deg);
    }

    100% {
        transform: translate(2vmin, 70vmin) rotate(150deg);
    }

}

@keyframes flower-fall-down-purple {

    0% {
        transform: rotate(-50deg);
    }

    25% {
        bottom: 1vmin;
        transform: rotateX(-100deg);
        perspective: 0px;
    }

    50% {
        perspective: 0px;
        transform: translate(-30vmin, 2vmin) rotate(90deg);
    }

    75% {
        perspective: 0px;
        transform: translate(-34vmin, -2vmin);
    }

    100% {
        transform-origin: center;
        transform: translate(-34vmin, -2vmin) rotateY(-80deg) rotateX(35deg);
    }

}

@keyframes flower-falling {

    0%,
    100% {
        transform-origin: center;
        transform: translate(-34vmin, -2vmin) rotateY(-80deg) rotateX(35deg);
    }

    25% {
        transform-origin: center;
        transform: translate(-34.4vmin, -2vmin) rotateY(-84deg) rotateX(35deg);
    }

    50% {
        transform-origin: center;
        transform: translate(-32vmin, -4.2vmin) rotateY(-80deg) rotateX(35deg);
    }

    75% {
        transform-origin: center;
        transform: translate(-36vmin, 1.1vmin) rotateY(-80deg) rotateX(35deg);
    }
}
</style>