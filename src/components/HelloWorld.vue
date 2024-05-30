<script setup>
import { ref, onMounted } from 'vue';

defineProps({
  msg: String,
});

const count = ref(0);

onMounted(async () => {
  //build dữ liệu
  // gọi api từng cục dữ liệu + ghi kết quả ra file
  //fetch()
});

async function sendRequest(data) {
  const headers = new Headers();
  headers.append(
    'Token',
    'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Im1pc2EiLCJpc3MiOiI2NjFiZjkwN2JmZmJiNjNmYWYwYzFiNWEiLCJleHAiOjE3MTcxMTc0Mzh9.VN_lqUk9j2r4oYOna41H1c2L2GJJJu0-4q9YU8Lgqdo'
  );
  headers.append('Username', 'misa');
  headers.append(
    'Cookie',
    'AUTH_BEARER_default=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpYXQiOjE3MTcwMzI5NzgsImp0aSI6ImMzdnkvQXhiaTlTckFOekVaK216NVNROHdENFdEZkxEYU5tQjJuKzdFbmM9IiwiaXNzIjoiZHRpLmhjbS5lZHUudm4iLCJuYmYiOjE3MTcwMzI5NzgsImV4cCI6MTcxNzAzNjU3OCwiZGF0YSI6ImNzcmZUb2tlbnxzOjY0OlwiZWVmMDBmZTEwMjQxNGZlOGY1OTFmOWI3Njc0YmY0NjgzNjIwMzRlMjA2MDExYzQxNDFhMzUwY2VlOGMyMWY0YVwiO2d1ZXN0SWR8czozMjpcIjA1MmE0NTVkMTZmZGUyYjcwMTFhYmQyZmZhZTk4NTdiXCI7In0.oa3zIrw7BvsTy3QsFZOI_hrUe1tNW0cd0J1CWaafCpWbZ2idzYD68tVet4pnU92MIRZVT40K89G9OlvJ_CK1Cw; be=8'
  );
  const myRequest = new Request(
    'https://dti.hcm.edu.vn/sync-data/lms/sendEquipmentInfo',
    {
      method: 'POST',
      headers: headers,
      body: JSON.stringify(data),
    }
  );

  const response = await fetch(myRequest);
  console.log(response);

  let finalResponse = {
    sendData: data,
  };

  if (!response.ok) {
    throw new Error('Network response was not OK');
  } else {
    const json = await response.json();
    finalResponse.apiResponse = json;
    console.log('json', json);
  }

  return finalResponse;
}

async function sendRequest2x() {
  //
  try {
    Object.entries(cc);
    const v = getData('1042683', 2, arrBudgetCode, arrCode);
    console.log('v', v);
  } catch (error) {
    console.error(error);
  }

  const headers = new Headers();
  headers.append(
    'Token',
    'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Im1pc2EiLCJpc3MiOiI2NjFiZjkwN2JmZmJiNjNmYWYwYzFiNWEiLCJleHAiOjE3MTcxMTc0Mzh9.VN_lqUk9j2r4oYOna41H1c2L2GJJJu0-4q9YU8Lgqdo'
  );
  headers.append('Username', 'misa');
  headers.append(
    'Cookie',
    'AUTH_BEARER_default=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpYXQiOjE3MTcwMzI5NzgsImp0aSI6ImMzdnkvQXhiaTlTckFOekVaK216NVNROHdENFdEZkxEYU5tQjJuKzdFbmM9IiwiaXNzIjoiZHRpLmhjbS5lZHUudm4iLCJuYmYiOjE3MTcwMzI5NzgsImV4cCI6MTcxNzAzNjU3OCwiZGF0YSI6ImNzcmZUb2tlbnxzOjY0OlwiZWVmMDBmZTEwMjQxNGZlOGY1OTFmOWI3Njc0YmY0NjgzNjIwMzRlMjA2MDExYzQxNDFhMzUwY2VlOGMyMWY0YVwiO2d1ZXN0SWR8czozMjpcIjA1MmE0NTVkMTZmZGUyYjcwMTFhYmQyZmZhZTk4NTdiXCI7In0.oa3zIrw7BvsTy3QsFZOI_hrUe1tNW0cd0J1CWaafCpWbZ2idzYD68tVet4pnU92MIRZVT40K89G9OlvJ_CK1Cw; be=8'
  );
  const myRequest = new Request(
    'https://dti.hcm.edu.vn/sync-data/lms/sendEquipmentInfo',
    {
      method: 'POST',
      headers: headers,
      body: JSON.stringify({
        data: {
          hasDeviceInformatics: 2,
        },
        schoolCode: '7900004011xxxx111',
      }),
    }
  );

  const response = await fetch(myRequest);
  console.log(response);

  let finalResponse = {};

  if (!response.ok) {
    throw new Error('Network response was not OK');
    finalResponse.success = false;
  } else {
    const json = await response.json();
    finalResponse.success = true;
    finalResponse.apiResponse = json;

    console.log('json', json);
  }

  return finalResponse;
}

const apiResponseExample = {
  status: 'SUCCESS',
  message: 'Cập nhật thành công',
};

const apiResponseFailure = {
  status: 'FAIL',
  message: 'Mã trường không hợp lệ',
};

// list kết quả
const responseObjectSave = {};
// lưu messge ko tìm thấy data - dữ liệu gửi lên api
const errorListBuildData = [];

async function sendAllRequests() {
  for (const [key, value] of Object.entries(cc)) {
    let data;
    try {
      data = getData(key, value, arrBudgetCode, arrCode);
    } catch (error) {
      errorListBuildData.push(error);
      console.error(error);
      continue;
    }

    const response = await sendRequest(data);
    //ghi vao object
    responseObjectSave[data.schoolCode] = response;
  }
  console.log('responseObjectSave:', responseObjectSave);
  console.log('errorListBuildData:', errorListBuildData);
}

function getData(key, value, arrBudgetCode = [], arrSchoolCode = []) {
  const budgetCodeIndex = arrBudgetCode.findIndex((item) => item == key);
  if (budgetCodeIndex == -1) {
    let message = `Không tìm thấy budgetCode với giá trị mapping ${key}`;
    throw new Error(message);
  }

  const schoolCode = arrSchoolCode[budgetCodeIndex];
  if (!schoolCode) {
    let message = `Không tìm thấy schoolCode với giá trị mapping ${key} và budgetCode ${arrBudgetCode[budgetCodeIndex]}`;
    throw new Error(message);
  }

  return {
    data: {
      hasDeviceInformatics: value,
    },
    schoolCode: schoolCode,
  };
}

const cc = {
  1001956: 0,
  1003700: 0,
  1003701: 0,
  1003702: 0,
  1006376: 0,
  1006382: 2,
  1008063: 2,
  1008124: 0,
  1010342: 0,
  1014727: 0,
  1014981: 0,
  1015952: 2,
  1016211: 0,
  1032621: 0,
  1035432: 0,
  1035494: 0,
  1035599: 0,
  1037221: 0,
  1037222: 0,
  1037383: 0,
  1037384: 2,
  1038540: 0,
  1038764: 0,
  1038766: 0,
  1038773: 0,
  1039166: 0,
  1039169: 2,
  1039986: 0,
  1039987: 0,
  1040014: 0,
  1040081: 0,
  1040082: 0,
  1040223: 0,
  1040247: 0,
  1040248: 0,
  1040251: 0,
  1042466: 0,
  1042552: 0,
  1042554: 0,
  1042683: 2,
  1042734: 0,
  1042857: 0,
  1042858: 0,
  1043921: 0,
  1043924: 2,
  1045805: 0,
  1046613: 0,
  1046615: 0,
  1046616: 0,
  1046617: 0,
  1046716: 0,
  1046742: 0,
  1046743: 0,
  1046744: 0,
  1049798: 0,
  1050023: 0,
  1052360: 0,
  1052865: 0,
  1058082: 0,
  1058084: 0,
  1058491: 0,
  1058492: 0,
  1058527: 0,
  1060559: 0,
  1060563: 0,
  1060564: 0,
  1060634: 2,
  1060635: 0,
  1060778: 0,
  1060858: 2,
  1061104: 0,
  1061105: 0,
  1068660: 0,
  1068661: 0,
  1069842: 0,
  1069843: 0,
  1069844: 0,
  1071559: 0,
  1072912: 0,
  1073003: 0,
  1073929: 2,
  1076001: 0,
  1076003: 0,
  1076008: 0,
  1076866: 0,
  1080927: 0,
  1086001: 0,
  1086050: 0,
  1086051: 0,
  1086114: 2,
  1104035: 0,
  1104505: 0,
  1105244: 0,
  1105299: 0,
  1109454: 0,
  1110106: 0,
  1110143: 0,
  1110153: 0,
  1114361: 0,
  1114460: 0,
  1118191: 2,
  1118192: 0,
  1120603: 0,
  1120604: 0,
  1122500: 0,
  1125719: 0,
  1125803: 0,
  1125808: 0,
  1127196: 0,
  1127428: 2,
  1129109: 0,
  1129141: 0,
  1129175: 2,
  1129198: 0,
};

const arrCode = [
  '7900004006',
  '7900004011',
  '7900004014',
  '7900004022',
  '79000701',
  '79000702',
  '79000703',
  '79000704',
  '79000705',
  '79000706',
  '79000708',
  '79000709',
  '79000710',
  '79000711',
  '79000712',
  '79000713',
  '79000714',
  '79000715',
  '79000716',
  '79000717',
  '79000718',
  '79000719',
  '79000720',
  '79000721',
  '79000722',
  '79000723',
  '79000724',
  '79000725',
  '79000726',
  '79000727',
  '79000728',
  '79000729',
  '79000730',
  '79000731',
  '79000732',
  '79000733',
  '79000734',
  '79000735',
  '79000736',
  '79000737',
  '79000738',
  '79000739',
  '79000740',
  '79000741',
  '79000742',
  '79000743',
  '79000744',
  '79000745',
  '79000746',
  '79000747',
  '79000748',
  '79000749',
  '79000750',
  '79000752',
  '79000753',
  '79000754',
  '79000755',
  '79000756',
  '79000757',
  '79000758',
  '79000759',
  '79000760',
  '79000761',
  '79000762',
  '79000763',
  '79000764',
  '79000765',
  '79000768',
  '79000769',
  '79000784',
  '79000786',
  '79000793',
  '79000794',
  '79000795',
  '79000796',
  '790007A6',
  '790007A7',
  '790007A8',
  '790007A9',
  '790007B0',
  '790007B1',
  '790007B2',
  '790007B3',
  '790007B6',
  '790007B7',
  '790007B8',
  '790007C1',
  '790007C2',
  '790007C3',
  '790007C4',
  '790007C5',
  '790007C6',
  '790007C7',
  '79000802',
  '79000803',
  '79000804',
  '79000805',
  '79000806',
  '79000807',
  '79000820',
  '79000842',
  '79000860',
  '79000861',
  '79000869',
  '79000871',
  '79000875',
  '79000876',
  '79000901',
  '79000902',
  '79000903',
  '79000F01',
  '79000F02',
  '79000F03',
  '79774507',
  '79786701',
];

const arrBudgetCode = [
  '1015952',
  '1042683',
  '1006382',
  '1086114',
  '1072912',
  '1061105',
  '1069843',
  '1008124',
  '1003702',
  '1060559',
  '1042857',
  '1058084',
  '1060635',
  '1040081',
  '1060564',
  '1040014',
  '1037221',
  '1040223',
  '1058491',
  '1016211',
  '1060858',
  '1003701',
  '1042552',
  '1073003',
  '1039987',
  '1060563',
  '1069842',
  '1040248',
  '1052865',
  '1060778',
  '1068660',
  '1042466',
  '1008063',
  '1014981',
  '1046744',
  '1058082',
  '1073929',
  '1042554',
  '1046743',
  '1042734',
  '1037222',
  '1046617',
  '1014727',
  '1058492',
  '1069844',
  '1039166',
  '1068661',
  '1040082',
  '1040251',
  '1046613',
  '1046616',
  '1046742',
  '1039169',
  '1040247',
  '1046615',
  '1038773',
  '1038766.',
  '1038764',
  '1038540',
  '1032621',
  '1043924',
  '1043921',
  '1076003',
  '1035494',
  '1035432',
  '1037383',
  '1037384',
  '1086050',
  '1086051',
  '1104505',
  '1104035',
  '1105299',
  '1105244',
  '1076866',
  '1046716',
  '1110153',
  '1110106',
  '1109454',
  '1110143',
  '1114361',
  '1114460',
  '1118192',
  '1118191',
  '1120603',
  '1120604',
  '1122500',
  '1125803',
  '1125808',
  '1127196',
  '1129141',
  '1129198',
  '1129175',
  '1129109',
  '1003700',
  '1001956',
  '1042858',
  '1058527',
  '1039986',
  '1061104.',
  '1080927',
  '1076001',
  '1045805',
  '1049798',
  '1086001',
  '1035599',
  '1125719',
  '1127428',
  '1052360.',
  '1006376',
  '1036941',
  '1071559',
  '1060634',
  '1076008',
  '1010342',
  '1050023',
];
</script>

<template>
  <button @click="sendAllRequests">Bấm để gửi</button>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Learn more about IDE Support for Vue in the
    <a
      href="https://vuejs.org/guide/scaling-up/tooling.html#ide-support"
      target="_blank"
      >Vue Docs Scaling up Guide</a
    >.
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
