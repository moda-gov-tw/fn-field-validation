<template>
  <UContainer class="fn-field-validation-container">
    <UCard>
      <div class="space-y-4">
        <UFormGroup
          label="name"
          name="name"
          :hint="nameValid ? '' : nameErrorMsg"
        >
          <UInput
            v-model="form.name"
            variant="outline"
            :color="nameValid ? 'gray' : 'red'"
            placeholder="please input"
          />
        </UFormGroup>
        <UFormGroup label="ID" name="ID" :hint="idValid ? '' : idErrorMsg">
          <UInput
            v-model="form.id"
            variant="outline"
            :color="idValid ? 'gray' : 'red'"
            placeholder="please input"
          />
        </UFormGroup>
        <UFormGroup
          label="file"
          name="file"
          :hint="fileValid ? '' : fileErrorMsg"
        >
          <UInput
            type="file"
            size="sm"
            icon="i-heroicons-folder"
            :color="fileValid ? 'gray' : 'red'"
            accept="jpg,png,xls,xlsx,odt,ods,doc,docx,pdf"
            @change="handleFileUpload"
          />
        </UFormGroup>
        <UButton
          label="submit"
          block
          @click.stop="submit"
          :disabled="btnDisabled"
        />
      </div>
    </UCard>
    <UNotifications color="primary" :id="6" :timeout="300000" />
  </UContainer>
</template>

<script lang="ts">
import _ from "lodash";
export default {
  name: "fn-field-validation",
  setup() {
    const form = ref({ name: "", id: "", file: null });
    const nameValid = ref(true);
    const idValid = ref(true);
    const fileValid = ref(true);
    const nameErrorMsg = ref(
      "請輸入正確姓名格式，如：「王小明」、「王·小明」、「王•小明」、「WANG,SIAO-MING」"
    );
    const idErrorMsg = ref("請輸入正確的身分證號或居留證號");
    const fileErrorMsg = ref(
      "單一檔案不可超過2MB, 檔案須為以下格式：jpg,png,xls,xlsx,odt,ods,doc,docx,pdf"
    );
    const toast = useToast();

    const btnDisabled = computed(
      () =>
        _.trim(form.value.name) === "" &&
        _.trim(form.value.id) === "" &&
        form.value.file === null
    );

    const aboriName = (name: string): boolean => {
      return /^[\u4E00-\u9FFF\uD800-\uDFFF]+[·•][\u4E00-\u9FFF\uD800-\uDFFF]+$/.test(
        name
      );
    };
    const chName = (name: string): boolean => {
      return /^[\u4E00-\u9FFF\uD800-\uDFFF]+$/.test(name);
    };
    const enName = (name: string): boolean => {
      return /^[a-zA-Z]+[,]{1}[a-zA-Z]+[-]{0,1}[a-zA-Z]*$/.test(
        name ? name.replace(/\s/g, "") : ""
      );
    };
    const aboriChEnName = (name: string): boolean => {
      let valid = false;
      name = _.trim(name);
      if (name === "") return true;
      if (_.includes(name, "•") || _.includes(name, "·")) {
        valid = aboriName(name);
      } else {
        if (chName(name)) valid = true;
        if (enName(name)) valid = true;
      }
      return valid;
    };

    const validNationalId = (id: string): boolean => {
      if (!/^[a-zA-Z]{1}[1-2]{1}[0-9]{8}$/.test(id)) return false;
      const locationMap = [
        10, 11, 12, 13, 14, 15, 16, 17, 34, 18, 19, 20, 21, 22, 35, 23, 24, 25,
        26, 27, 28, 29, 32, 30, 31, 33,
      ];
      const digit =
        locationMap[id.toUpperCase().charCodeAt(0) - "A".charCodeAt(0)];
      let checksum = 0;
      checksum += Math.floor(digit / 10);
      checksum += (digit % 10) * 9;
      for (let i = 1, p = 8; i <= 8; i++, p--) {
        checksum += parseInt(id.charAt(i)) * p;
      }
      checksum += parseInt(id.charAt(9));
      return !(checksum % 10);
    };
    const validNewResidentPermitId = (id: string): boolean => {
      const locationMap = [
        10, 11, 12, 13, 14, 15, 16, 17, 34, 18, 19, 20, 21, 22, 35, 23, 24, 25,
        26, 27, 28, 29, 32, 30, 31, 33,
      ];
      const digit =
        locationMap[id.toUpperCase().charCodeAt(0) - "A".charCodeAt(0)];
      let checksum = 0;
      checksum += Math.floor(digit / 10);
      checksum += (digit % 10) * 9;
      for (let i = 1, p = 8; i <= 8; i++, p--) {
        checksum += parseInt(id.charAt(i)) * p;
      }
      checksum += parseInt(id.charAt(9));
      return !(checksum % 10);
    };
    const validOldResidentPermitId = (id: string): boolean => {
      const convert = "ABCDEFGHJKLMNPQRSTUVXYWZIO";
      const weights = [1, 9, 8, 7, 6, 5, 4, 3, 2, 1, 1];
      id =
        String(convert.indexOf(id[0]) + 10) +
        String((convert.indexOf(id[1]) + 10) % 10) +
        id.slice(2);
      let checkSum = 0;
      for (let i = 0; i < id.length; i++) {
        const c = parseInt(id[i]);
        const w = weights[i];
        checkSum += c * w;
      }
      return !(checkSum % 10);
    };
    const nidAndRpid = (id: string): boolean => {
      if (_.trim(id) === "") return true;
      id = id.replace(/\s+/g, "");
      if (/^[a-zA-Z]{1}[1-2]{1}[0-9]{8}$/.test(id)) return validNationalId(id);
      else if (/^[a-zA-Z]{1}[8-9]{1}[0-9]{8}$/.test(id))
        return validNewResidentPermitId(id);
      else if (/^[a-zA-Z]{1}[a-zA-Z]{1}[0-9]{8}$/.test(id))
        return validOldResidentPermitId(id);
      else return false;
    };

    const fileTypes = ref([
      "image/jpeg",
      "image/png",
      "application/vnd.ms-excel",
      "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
      "application/vnd.oasis.opendocument.text",
      "application/vnd.oasis.opendocument.spreadsheet",
      "application/msword",
      "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
      "application/pdf",
    ]);
    const fnfileValid = (file: File): boolean => {
      if (file === null) return true;
      return file.size < 2097153 && _.includes(fileTypes.value, file.type);
    };
    const handleFileUpload = (event: any) => (form.value.file = event[0]);
    const submit = () => {
      nameValid.value = aboriChEnName(form.value.name);
      idValid.value = nidAndRpid(form.value.id);
      fileValid.value = fnfileValid(form.value.file);
      if (nameValid.value && idValid.value && fileValid.value)
        toast.add({ id: "6", title: "所有欄位皆驗證通過" });
    };
    return {
      submit,
      handleFileUpload,
      btnDisabled,
      form,
      nameValid,
      nameErrorMsg,
      idValid,
      idErrorMsg,
      fileValid,
      fileErrorMsg,
    };
  },
};
</script>
