<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer">
                <i class="pi pi-angle-left text-3xl"></i>
            </span>
            <ThemeSwitch />
        </div>

        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">

            <!-- Marital Status -->
            <div class="w-full mt-4 px-2">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Add nominee
                </p>
                <p class="text-md mt-1 text-gray-500 font-normal leading-6">
                    Relationship with nominee
                </p>
                <div class="w-full flex flex-col gap-2 mt-3">
                    <Button @click="visible = true"
                        class="w-full py-3 primary_color text-white">
                    {{ nomineetext }}
                    </Button>

                    <p v-if="skip" class="text-center text-md text-blue-600 mt-2">Skip now</p>
                </div>
            </div>
            <Dialog class="p-0" v-model:visible="visible" modal  header="Add Nominee" :style="{ width: '25rem' }">

                <Name v-model="name" class="mt-2" />
                <Namemode  v-model:relationship="selectedRelationship" class="mt-2" />
                <DOB v-model="dob" class="mt-2" />
                <Aadharpan v-model="aadharpan" class="mt-2" />
                <Address v-model="address" class="mt-2" />
              
             

                <div class="w-full mt-3">
                    <Button :disabled="!selectedRelationship || !name || !dob || !aadharpan || !address " label="Save" @click="nomineesave()" class="primary_color w-full text-white py-2"></Button>
                </div>
            </Dialog>


            <div class="w-full">
                <Button @click="handleButtonClick"
                    class="primary_color wave-btn w-full text-white  py-4 text-xl border-0">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>



        </div>


    </div>



</template>

<script setup>
import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';
import Namemode from '~/components/nomineeinputs/dropdown.vue';
import Name from '~/components/nomineeinputs/nameinput.vue';
import DOB from '~/components/forminputs/dateinput.vue'
import Aadharpan from '~/components/nomineeinputs/aadharpaninput.vue';
import Address from '~/components/nomineeinputs/address.vue';


const skip=ref(true);
const visible = ref(false);
const emit=defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");
const nomineetext = ref("Add Nominee");

const selectedRelationship = ref(null);
const name = ref('');
const dob = ref('');
const aadharpan = ref('');
const address = ref('');


const back = () => {
    emit('updateDiv', 'income');
};


onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const nomineesave=()=>{
    console.log("Nominee Details:")
    console.log("Relationship: ",selectedRelationship.value)
    console.log("Name: ",name.value)
    console.log("DOB: ",dob.value)
    console.log("Aadhar/PAN: ",aadharpan.value)
    console.log("Address: ",address.value)


    nomineetext.value='Nominee Saved'
    visible.value=false
    skip.value=false
}

const handleButtonClick=()=>{
    isAnimating.value = true;
    setTimeout(() => {
        isAnimating.value = false;
        buttonText.value = "Continue";
        emit('updateDiv', 'submission','2');
    }, 2000); // Adjust the duration as needed
};
</script>
<style>
.p-dialog-header{
    padding: 1% !important;
}
</style>