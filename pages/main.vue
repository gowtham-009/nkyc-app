<template>
 
    <div v-if="currentForm === 'div1'">
    <NKYCList @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div2'">
    <PAN_d @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div3'">
    <PAN_1 @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div4'">
    <EKYC @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div5'">
    <AADHARPAN @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div6'">
    <AADHARPANotp @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div7'">
    <DIGILOCK @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div8'">
    <DIGILOCKSUBMISSION @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'div9'">
    <PANCONFIRMATION @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'submission'">
    <SUBMISSIONFORM :data="data" @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'married'">
    <MARRIEDSTATUS  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'occupation'">
    <OCCUPATION  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'income'">
    <INCOME  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'nominee'">
    <NOMINEE  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'bank1'">
    <BANK1  @updateDiv="handleUpdateDiv" />
  </div>


  <div v-if="currentForm === 'bank4'">
    <BANK4 :data="data"  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'photosign1'">
    <PHOTOSIGN1  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'takephoto'">
    <TAKEPHOTO  @updateDiv="handleUpdateDiv"  />
  </div>

  <div v-if="currentForm === 'photoproceed'">
    <PHOTOPROCEED :data="data"  @updateDiv="handleUpdateDiv" />
   
  </div>

  <div v-if="currentForm === 'signature'">
    <SIGNATURE   @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'signupload'">
    <SIGNUPLOAD :data="data" @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'signdraw'">
    <SIGNDRAWING :data="data" @updateDiv="handleUpdateDiv" />
  </div>
 
  <div v-if="currentForm === 'thankyou'">
    <THANKINGYOU @updateDiv="handleUpdateDiv" />
  </div>
</template>

<script setup>
import NKYCList from '~/components/NKYC_Forms/nkyclist.vue'
import PAN_d from '~/components/NKYC_Forms/pandetails/pan-d.vue'
import PAN_1 from '~/components/NKYC_Forms/pandetails/pan_1.vue'
import EKYC from '~/components/NKYC_Forms/pandetails/e-kyc.vue'
import AADHARPAN from '~/components/NKYC_Forms/pandetails/aadharpan.vue'
import AADHARPANotp from '~/components/NKYC_Forms/pandetails/aadharotp.vue'
import DIGILOCK from '~/components/NKYC_Forms/pandetails/digilock.vue'
import DIGILOCKSUBMISSION from '~/components/NKYC_Forms/pandetails/digilock_submission.vue'
import PANCONFIRMATION from '~/components/NKYC_Forms/pandetails/panconfirmation.vue'
import SUBMISSIONFORM from '~/components/NKYC_Forms/submissionpage.vue'
import MARRIEDSTATUS from '~/components/NKYC_Forms/profiledetails/marridestatus.vue'
import OCCUPATION from '~/components/NKYC_Forms/profiledetails/occupationstatus.vue'
import INCOME from '~/components/NKYC_Forms/profiledetails/incomestatus.vue'
import NOMINEE from '~/components/NKYC_Forms/profiledetails/nominee.vue'
import BANK1 from '~/components/NKYC_Forms/bankdetails/bank1.vue'


import BANK4 from '~/components/NKYC_Forms/bankdetails/bank4.vue'
import PHOTOSIGN1 from '~/components/NKYC_Forms/photo&sign/photosign.vue'
import TAKEPHOTO from '~/components/NKYC_Forms/photo&sign/takephoto.vue'
import PHOTOPROCEED from '~/components/NKYC_Forms/photo&sign/pictureproceed.vue'
import SIGNATURE from '~/components/NKYC_Forms/photo&sign/signature.vue'
import SIGNUPLOAD from '~/components/NKYC_Forms/photo&sign/signuploaded.vue'
import SIGNDRAWING from '~/components/NKYC_Forms/photo&sign/signdraw.vue'
import THANKINGYOU from '~/components/thankyou.vue'

const currentDiv = ref('');
const currentForm = ref('div1'); 
const data = ref({});

const handleUpdateDiv = (value,  newData={}) => {
currentDiv.value = value;
currentForm.value=currentDiv.value
data.value = newData;





};

</script>

<style >

</style>