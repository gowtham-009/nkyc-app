<template>
    <div class="primary_color" v-if="contentbox">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black" v-if="panbox"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Upload Pan card
                </p>
                <p class="text-gray-500 leading-6 font-normal text-md mt-3">
                    Click a photo of your PAN card or upload from files
                </p>

                <div class="w-full mt-3 rounded-lg px-3 py-3 bg-blue-50 dark:bg-slate-900">
                    <h2 class="text-blue-900 text-2xl font-medium mt-3 dark:text-gray-400">Please remember:</h2>

                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span><i class="text-xl text-blue-900 pi pi-id-card"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                                Upload only the front-side of your PAN card.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span><i class="text-xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                                Photo size must not exceed 5MB each.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span><i class="text-xl text-blue-900 pi pi-star"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                                Photo must be well-lit and glare-free.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center static w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span><i class="text-xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                                Photo must be clear.
                            </p>
                        </div>
                    </div>
                </div>

            </div>

            <div class="w-full p-1" label="Continue">
                <Button type="button" label="Continue" @click="visibleBottom = true"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  "></Button>
            </div>



        </div>

        <div class="w-full flex flex-col justify-between p-2 bg-white rounded-t-3xl dark:bg-black" v-if="uploadbox"
            :style="{ height: deviceHeight * 0.92 + 'px' }">




            <div class="w-full p-2 mt-4">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    PAN card captured
                </p>

                <p class="text-md leading-5 text-gray-500 font-normal mt-2">
                    Proceed only if the contents of the photo are clearly visible.
                </p>

                <div class="w-full flex justify-center mt-2">
                    <div class="w-2/3 flex justify-center p-1" >
                        <img v-if="imageUrl" :src="imageUrl" alt="Preview" class="preview-img h-80"  />
                       
                    </div>
                </div>
                <div class="w-full mt-2">
                    <p class="text-blue-950 font-normal text-md text-center dark:text-gray-400">Poor photo quality?</p>
                    <p class="text-center font-medium text-blue-600 mt-3 text-xl border-2 py-2 rounded-lg" @click="openFilePicker">Upload from gallery</p>
                </div>
            </div>
            <div class="w-full" >
                <Button type="button" label="Next"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  "></Button>
            </div>
        </div>
    </div>

    <div class="w-full p-2" v-if="camerabox">
        <div v-if="showCamera" class="fixed inset-0 bg-black flex items-center justify-center">
            <video ref="videoRef" autoplay class="w-full h-full object-cover"></video>

            <!-- Canvas for capturing image -->
            <canvas ref="canvasRef" class="hidden"></canvas>

            <!-- Close Button at Top Left -->
            <Button type="button" icon="pi pi-angle-left" @click="backpan()"
                class="absolute bg-gray-50 top-4 left-4 text-black border-0 p-2 rounded" style="z-index: 5;">
            </Button>

            <!-- Four Edge Frames -->
            <div class="absolute inset-0 flex justify-between items-center px-5" style="top: -43%;">
                <div class="w-12 h-12 border-4 border-blue-900 border-b-0 border-r-0"></div>
                <div class="w-12 h-12 border-4 border-blue-900 border-b-0 border-l-0"></div>
            </div>
            <div class="absolute inset-0 flex justify-between items-end pb-20 px-5" style="bottom: 24%;">
                <div class="w-12 h-12 border-4 border-blue-900 border-t-0 border-r-0"></div>
                <div class="w-12 h-12 border-4 border-blue-900 border-t-0 border-l-0"></div>
            </div>

            <!-- Click Photo Button at Bottom Center -->
            <div class="absolute bottom-10 w-full flex justify-center">
                <Button type="button" :label="photoCaptured ? 'Retake' : 'Click Photo'" @click="handleCapture"
                    class="primary_color wave-btn text-white px-20 py-4 text-xl border-0">
                </Button>
            </div>

            <!-- Display Captured Image -->
            <div v-if="photoCaptured" class="absolute bottom-32 w-full flex justify-center">
                <img :src="capturedImage" alt="Captured Image" class="w-full max-w-md" />
            </div>
        </div>
    </div>



    <Drawer v-model:visible="visibleBottom" class="rounded-t-3xl" position="bottom" style="height: auto">
        <Button type="button" label="Open Camera" @click="cameraopen"
            class=" primary_color wave-btn text-white w-full py-4 text-xl border-0">
        </Button>
        <p class="text-center font-medium text-blue-600 mt-3 text-2xl" @click="openFilePicker">Upload from gallery</p>
    </Drawer>

    <input type="file" ref="fileInput" @change="handleFileChange" accept="image/*" class="hidden" />
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue';

const deviceHeight = ref(0);
const visibleBottom = ref(false);
const contentbox = ref(true);  // Initially showing content box
const camerabox = ref(false);  // Initially not showing camera box
const panbox = ref(true); // Initially showing pan box
const uploadbox = ref(false); // Initially not showing upload box
const showCamera = ref(false);
const photoCaptured = ref(false); // To track if the photo is captured
const capturedImage = ref(null); // To store the captured image as a data URL
const videoRef = ref(null);
const canvasRef = ref(null);
let stream = null;

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});

const backpan = () => {

    stopCamera();

    // Show the content box and hide the camera box
    contentbox.value = true;
    camerabox.value = false;

    // Reset any states related to the camera
    photoCaptured.value = false;
    capturedImage.value = null;
};

const cameraopen = async () => {
    showCamera.value = true;
    contentbox.value = false;
    camerabox.value = true;
    visibleBottom.value = false;
    photoCaptured.value = false;
    try {
        stream = await navigator.mediaDevices.getUserMedia({
            video: { facingMode: "environment" },
        });
        if (videoRef.value) {
            videoRef.value.srcObject = stream;
        }
    } catch (error) {
        console.error("Error accessing the camera:", error);
        showCamera.value = false;
    }
};

const stopCamera = () => {
    if (stream) {
        stream.getTracks().forEach(track => track.stop()); // Stop all tracks
    }
    showCamera.value = false; // Hide the camera
    camerabox.value = false; // Hide the camera box
};

const handleCapture = () => {

    if (photoCaptured.value) {
        // If photo is already taken, reopen the camera
        photoCaptured.value = false;
        capturedImage.value = null; // Clear the captured image
        cameraopen();
    } else {
        // Capture the photo
        captureImage();
    }
};

const captureImage = () => {
    if (videoRef.value && canvasRef.value) {
        const video = videoRef.value;
        const canvas = canvasRef.value;
        const ctx = canvas.getContext('2d');
        // Set canvas size to video size
        canvas.width = video.videoWidth;
        canvas.height = video.videoHeight;
        // Draw the current video frame on the canvas
        ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
        // Convert the canvas to an image
        capturedImage.value = canvas.toDataURL('image/jpeg');
        photoCaptured.value = true;
    }
};

onBeforeUnmount(() => {
    stopCamera();
});
const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'div2');
}

const fileInput = ref(null);
const selectedFile = ref(null);
const imageUrl = ref(null);

const openFilePicker = () => {
    if (fileInput.value) {
        fileInput.value.click();
        visibleBottom.value = false;
       
    }
};

const handleFileChange = (event) => {
    const file = event.target.files[0]; // Get the selected file
    if (file) {
        selectedFile.value = file;
        console.log("Selected file:", file);
        imageUrl.value = URL.createObjectURL(file);
        if(imageUrl.value) {
            uploadbox.value = true;
            panbox.value = false;
        } else {
            uploadbox.value = false;
            panbox.value = true;
        }

    }
};
</script>
