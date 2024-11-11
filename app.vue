<template>
  <section class="container px-0">
    <div class="card">
      <b-card-body>
        <div class="card-body col-12">
          <!-- 案件名稱 -->
          <b-form-row>
            <i-form-group-check
              :label="getCFieldsData('caseName', '案件名稱', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.caseName"
            >
              <b-form-input
                v-model.trim="$v.caseName.$model"
                :state="validateState($v.caseName)"
                lazy
              ></b-form-input>
            </i-form-group-check>
          </b-form-row>
          <!-- 功能網址 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('projectUrl', '功能網址', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.projectUrl"
            >
              <b-form-input
                v-model.trim="$v.projectUrl.$model"
                :state="validateState($v.projectUrl)"
              ></b-form-input>
            </i-form-group-check>
          </b-form-row>
          <!-- 問題主題 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('summary', '問題主題', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.summary"
            >
              <b-form-input
                v-model.trim="$v.summary.$model"
                :state="validateState($v.summary)"
                lazy
              ></b-form-input>
            </i-form-group-check>
          </b-form-row>
          <!-- 問題說明 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('description', '問題說明', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.description"
            >
              <b-form-textarea
                rows="4"
                max-rows="8"
                v-model.trim="$v.description.$model"
                :state="validateState($v.description)"
                placeholder="為確保個人資料安全，請勿在此欄填寫個人資料。"
                lazy
              ></b-form-textarea>
            </i-form-group-check>
          </b-form-row>
          <!-- 上傳附件 -->
          <b-form-row>
            <i-form-group-check
              :label="getCFieldsData('files', '上傳附件', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.files"
            >
              <b-form-file
                class="col-12"
                trim
                multiple
                accept="jpg,png,xls,xlsx,odt,ods,doc,docx,pdf"
                browse-text="選擇檔案"
                placeholder="未選擇任何檔案"
                drop-placeholder="拖曳檔案至此"
                v-model="$v.files.$model"
                :state="validateState($v.files)"
              ></b-form-file>
              <span class="remark-text col-12 p-0"
                >為能加速解決您的問題，請協助提供問題畫面，謝謝！</span
              >
              <span class="remark-text col-12 p-0"
                >可接受檔案格式：jpg,png,xls,xlsx,odt,ods,doc,docx,pdf，檔案請小於2MB內。</span
              >
            </i-form-group-check>
          </b-form-row>
          <!-- 聯絡單位 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('orgName', '聯絡單位', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.orgName"
            >
              <b-form-input
                v-model.trim="$v.orgName.$model"
                :state="validateState($v.orgName)"
                lazy
              ></b-form-input>
            </i-form-group-check>
          </b-form-row>
          <!-- 聯絡人 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('chName', '聯絡人', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.chName"
            >
              <i-hard-word
                v-model.trim="$v.chName.$model"
                :state="validateState($v.chName)"
                lazy
              ></i-hard-word>
            </i-form-group-check>
          </b-form-row>
          <!-- 聯絡電話 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('workTel', '聯絡電話', 'value') + '：'"
              class="col-sm-12"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.workTel"
            >
              <i-tel
                v-model.trim="$v.workTel.$model"
                :state="validateState($v.workTel)"
                showExt
              ></i-tel>
            </i-form-group-check>
          </b-form-row>
          <!-- 聯絡手機 -->
          <b-form-row>
            <i-form-group-check
              :labelStar="form.priority === '緊急'"
              :label="getCFieldsData('mobileTel', '聯絡手機', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.mobileTel"
            >
              <i-tel
                v-model.trim="$v.mobileTel.$model"
                :state="validateState($v.mobileTel)"
                isMobile
                lazy
              ></i-tel>
            </i-form-group-check>
          </b-form-row>
          <!-- 聯絡信箱 -->
          <b-form-row>
            <i-form-group-check
              labelStar
              :label="getCFieldsData('email', '聯絡信箱', 'value') + '：'"
              :class="iFormGroupCheckClass"
              :label-cols="labelCols"
              :content-cols="contentCols"
              :m-label-cols="mLabelCols"
              :m-content-cols="mContentCols"
              :item="$v.email"
            >
              <b-form-input
                v-model.trim="$v.email.$model"
                type="text"
                :state="validateState($v.email)"
                placeholder="xx@xx.xx"
                lazy
              ></b-form-input>
            </i-form-group-check>
          </b-form-row>
          <!-- 請輸入驗證碼 -->
          <i-verification-code
            ref="verificationCode"
            :formData="form"
            :vData="$v"
          ></i-verification-code>
        </div>
      </b-card-body>
      <b-card-body>
        <div class="text-center mt-2">
          <i-button type="save" @click="submit" v-if="showSubmitBtn"></i-button>
          <i-button type="x-circle" @click="reset"></i-button>
        </div>
      </b-card-body>
    </div>
  </section>
</template>

<script lang="ts">
import IButton from "@/shared/buttons/i-button.vue";
import { useValidation, validateState } from "@/shared/form";
import IFormGroupCheck from "@/shared/form/i-form-group-check.vue";
import IVerificationCode from "@/shared/form/i-verification-code.vue";
import ITel from "@/shared/i-tel/i-tel.vue";
import ITable from "@/shared/i-table/i-table.vue";
import { useBvModal } from "@/shared/modal";
import { useNotification } from "@/shared/notification";
import {
  email,
  lineTel,
  maxLength,
  mobileTel,
  required,
  sameAs,
  file,
} from "@/shared/validators";
import { useGetters, useStore } from "@u3u/vue-hooks";
import {
  computed,
  reactive,
  ref,
  watch,
  inject,
  onActivated,
} from "@vue/composition-api";
import {
  BFormRadio,
  BButton,
  BCardBody,
  BFormFile,
  BFormInput,
  BFormRow,
  BFormSelect,
  BFormTextarea,
  BRow,
  BCol,
} from "bootstrap-vue";
import {
  cloneDeep as _cloneDeep,
  size as _size,
  concat as _concat,
  forEach as _forEach,
  includes as _includes,
  keys as _keys,
  trim as _trim,
  filter as _filter,
  uniq as _uniq,
  head as _head,
  isArray as _isArray,
  assign as _assign,
  last as _last,
  split as _split,
  isObject as _isObject,
  orderBy as _orderBy,
  findIndex as _findIndex,
} from "lodash";
import { notificationErrorHandler } from "@/shared/http/http-response-helper";
import NotificationService from "@/shared/notification/notification-service";
import { formatDate } from "@/shared/date/minguo-calendar-utils";
import PwcMantisService from "@/components/pwc/pwcService/pwc-mantis.service";
import { tmpMappingComponent } from "@/components/pwc/pwcService/pwc-mantis.service";
import IHardWord from "@/shared/i-hard-word/i-hard-word.vue";

export default {
  name: "pwc0601",
  components: {
    IButton,
    IFormGroupCheck,
    IVerificationCode,
    ITel,
    ITable,
    IHardWord,
    BButton,
    BRow,
    BCol,
    BFormRadio,
    BCardBody,
    BFormRow,
    BFormSelect,
    BFormInput,
    BFormTextarea,
    BFormFile,
  },
  setup(props, context) {
    const drMode = computed(() => useGetters(["drMode"]).drMode.value);
    const pccMode = computed(() => useGetters(["pccMode"]).pccMode.value);
    const prodMode = computed(() => useGetters(["prodMode"]).prodMode.value);
    const devMode = computed(() => useGetters(["devMode"]).devMode.value);
    const drModeKey = computed(() => useGetters(["drModeKey"]).drModeKey.value);
    const pccModeKey = computed(
      () => useGetters(["pccModeKey"]).pccModeKey.value
    );
    const prodModeKey = computed(
      () => useGetters(["prodModeKey"]).prodModeKey.value
    );
    const devModeKey = computed(
      () => useGetters(["devModeKey"]).devModeKey.value
    );
    const deskTopDevice = computed(
      () => useGetters(["deskTopDevice"]).deskTopDevice.value
    );
    const accountService = inject<() => AccountService>("accountService")();
    const pwcMantisService = new PwcMantisService();
    const isAuth = computed(
      () => useGetters(["authenticated"]).authenticated.value
    );
    const tabClicked = ref({ report: true, review: false });
    const openMenus = computed(() => useGetters(["openMenus"]).openMenus.value);
    const appFlattenMenus = computed(
      () => useGetters(["appFlattenMenus"]).appFlattenMenus.value
    );
    const account = computed(() => useGetters(["account"]).account.value);
    const contactsData = computed(
      () => useGetters(["contactsData"]).contactsData.value
    );
    const $bvModals = useBvModal();
    const notificationService: NotificationService = useNotification();
    const iFormGroupCheckClass = ref("col-sm-12");
    const labelCols = ref("2");
    const contentCols = ref("9");
    const detailContentCols = ref("4");
    const mLabelCols = ref("12");
    const mContentCols = ref("12");
    const mantisProjects = ref({});
    const mantisIssues = ref({});
    const detailData = ref({});
    const detailDataShowFields = ref([
      "priority",
      "caseNo",
      "caseName",
      "class",
      "category",
      "projectUrl",
    ]);
    const customFieldsDefaultData = ref([
      { key: "priority", value: "優先度" },
      { key: "class", value: "類別" },
      { key: "caseNo", value: "案件編號" },
      { key: "caseName", value: "案件名稱" },
      { key: "summary", value: "問題主題" },
      { key: "description", value: "問題說明" },
      { key: "project", value: "功能項目" },
      { key: "projectUrl", value: "功能網址" },
      { key: "files", value: "上傳附件" },
      { key: "orgName", value: "聯絡單位" },
      { key: "chName", value: "聯絡人" },
      { key: "workTel", value: "聯絡電話" },
      { key: "mobileTel", value: "聯絡手機" },
      { key: "email", value: "聯絡信箱" },
      { key: "source", value: "問題來源" },
      { key: "userId", value: "回報人ID" },
    ]);
    const customModeDefaultData = ref([
      { key: drModeKey.value, value: "正式區" },
      { key: pccModeKey.value, value: "練習區" },
      { key: prodModeKey.value, value: "prod" },
      { key: devModeKey.value, value: "dev" },
    ]);
    const fileTypes = ref({
      jpg: "image/jpeg",
      png: "image/png",
      xls: "application/vnd.ms-excel",
      xlsx: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
      odt: "application/vnd.oasis.opendocument.text",
      ods: "application/vnd.oasis.opendocument.spreadsheet",
      doc: "application/msword",
      docx: "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
      pdf: "application/pdf",
    });
    const filesByFileReader = ref([]);
    const statusMapping = ref([
      { id: 10, color: "#fcbdbd", label: "new", name: "new", value: "新問題" },
      {
        id: 20,
        color: "#e3b7eb",
        label: "feedback",
        name: "feedback",
        value: "需要回覆",
      },
      {
        id: 30,
        color: "#ffcd85",
        label: "acknowledged",
        name: "acknowledged",
        value: "已接受",
      },
      {
        id: 40,
        color: "#fff494",
        label: "confirmed",
        name: "confirmed",
        value: "已確認",
      },
      {
        id: 50,
        color: "#c2dfff",
        label: "assigned",
        name: "assigned",
        value: "已分配",
      },
      {
        id: 80,
        color: "#d2f5b0",
        label: "resolved",
        name: "resolved",
        value: "已解決",
      },
      {
        id: 90,
        color: "#c9ccc4",
        label: "closed",
        name: "closed",
        value: "已結束",
      },
    ]);
    const showReportTable = ref(true);
    const showSubmitBtn = ref(true);
    const submitCount = ref(0);
    const validFilesNum = ref(0);

    const formDefault = {
      priority: "一般",
      class: "操作",
      caseNo: "",
      caseName: "",
      project: "",
      projectUrl: "",
      summary: "",
      description: "",
      files: [],
      orgName: "",
      chName: "",
      workTel: "",
      mobileTel: "",
      email: "",
      identifyCodeA: "",
      verificationCode: "",
    };
    const form = reactive(Object.assign({}, formDefault));
    const rules = {
      priority: { required },
      class: { required },
      caseNo: {},
      caseName: {},
      project: { required },
      projectUrl: { required },
      summary: { required },
      description: { required },
      files: {
        file: file(2097152, [
          fileTypes.value.jpg,
          fileTypes.value.png,
          fileTypes.value.xls,
          fileTypes.value.xlsx,
          fileTypes.value.odt,
          fileTypes.value.ods,
          fileTypes.value.doc,
          fileTypes.value.docx,
          fileTypes.value.pdf,
        ]),
      },
      orgName: { required },
      chName: { required },
      workTel: { required, lineTel: lineTel },
      mobileTel: { mobileTel: mobileTel },
      email: { required, email: email, maxLength: maxLength(100) },
      verificationCode: {
        required,
        sameAs: sameAs(
          computed(() => form.identifyCodeA),
          "驗證碼"
        ),
      },
    };
    const { $v, checkValidity, reset } = useValidation(
      rules,
      form,
      formDefault
    );

    const formOptions = reactive({
      project: [],
    });

    const formatStatus = (value) => {
      const filterArr = _filter(statusMapping.value, (s) => s.name === value);
      if (_size(filterArr) !== 1) return "";
      return _head(filterArr).value;
    };

    const table = reactive({
      fields: [
        {
          key: "summary",
          label: "主題",
          sortable: false,
          thClass: "text-left",
          tdClass: "text-left align-middle",
        },
        {
          key: "status",
          label: "狀態",
          sortable: true,
          thClass: "text-center",
          tdClass: "text-center align-middle",
          formatter: (value) => formatStatus(value),
        },
        {
          key: "created_at",
          label: "回報日期",
          sortable: false,
          thClass: "text-center",
          tdClass: "text-center align-middle",
          formatter: (value) => formatDate(new Date(value), "/"),
        },
        {
          key: "updated_at",
          label: "更新日期",
          sortable: false,
          thClass: "text-center",
          tdClass: "text-center align-middle",
          formatter: (value) => formatDate(new Date(value), "/"),
        },
        {
          key: "action",
          label: "動作",
          sortable: false,
          thClass: "text-center",
          tdClass: "text-center align-middle",
        },
      ],
      data: [],
      totalItems: 0,
    });

    const checkIssueStatus = (issue) => {
      let status = -1;
      if (!_includes(_keys(issue), "status")) return status;
      return issue.status.id;
    };

    const getCFieldsData = (key, value, returnKey) => {
      if (_trim(key) === "" && _trim(value) === "") return "";
      let filterArr = [];
      if (_trim(key) !== "" && _trim(value) !== "")
        filterArr = _filter(
          customFieldsDefaultData.value,
          (cf) => cf.key === key && cf.value === value
        );
      else if (_trim(key) !== "" && _trim(value) === "")
        filterArr = _filter(
          customFieldsDefaultData.value,
          (cf) => cf.key === key
        );
      else if (_trim(key) === "" && _trim(value) !== "")
        filterArr = _filter(
          customFieldsDefaultData.value,
          (cf) => cf.value === value
        );
      if (_size(filterArr) !== 1) return "";
      return _head(filterArr)[returnKey];
    };
    const getContactsData = () => {
      if (account.value === null) return;
      if (!_includes(_keys(account.value), "userId")) return;
      if (_trim(account.value.userId) === "") return;
      if (contactsData.value !== null) buildAccountData();
      else {
        accountService
          .getAdmContact(account.value.userId)
          .then((res) => {
            useStore().value.commit("setContactsData", _cloneDeep(res));
            buildAccountData();
          })
          .catch(notificationErrorHandler(notificationService))
          .finally(() => {});
      }
    };
    const getFormData = (data, key) => {
      if (!_isObject(data)) return "";
      if (!_includes(_keys(data), key)) return "";
      return _trim(data[key]);
    };
    const getPostData = () => {
      let obj = {
        valid: false,
        data: {
          category: { id: 1, name: "General" },
          summary: $v.value.summary.$model,
          description: $v.value.description.$model,
        },
      };
      const projectArr = _filter(
        mantisProjects.value,
        (p) => p.name === _trim($v.value.project.$model)
      );
      if (_size(projectArr) === 0) return obj;
      const projectData = getProjectData(projectArr);
      const custom_fieldsData = getCustomFieldsData(projectArr);
      const filesData = getFilesData();
      if (!projectData.valid) return obj;
      else obj.data = _assign(obj.data, { project: projectData.data });
      if (custom_fieldsData.valid)
        obj.data = _assign(obj.data, { custom_fields: custom_fieldsData.data });
      if (filesData.valid)
        obj.data = _assign(obj.data, { files: filesData.data });
      obj.valid = true;
      return obj;
    };
    const getProjectData = (projectArr) => {
      let obj = { valid: false, data: { id: 0, name: "" } };
      const projectObj = _cloneDeep(_head(projectArr));
      if (_size(_keys(projectObj)) === 0) return obj;
      obj.data.id = projectObj.id;
      obj.data.name = projectObj.name;
      obj.valid = true;
      return obj;
    };
    const getCustomFieldsData = (projectArr) => {
      let obj = { valid: false, data: [] };
      const custom_fields = _cloneDeep(_head(projectArr).custom_fields);
      if (!_isArray(custom_fields)) return obj;
      if (_size(custom_fields) === 0) return obj;
      _forEach(custom_fields, (cf) => {
        let cfObj = { field: { id: cf.id, name: cf.name }, value: null };
        const key = _trim(getCFieldsData("", cf.name, "key"));
        if (key === "") return;
        if (key === "source") cfObj.value = getSourceValue();
        else if (key === "userId")
          cfObj.value = account.value === null ? "" : account.value.userId;
        else cfObj.value = _cloneDeep(_trim($v.value[key].$model));
        if (cfObj.value === null) return;
        obj.data.push(cfObj);
      });
      obj.valid = true;
      return obj;
    };
    const getFilesData = () => {
      let obj = { valid: false, data: [] };
      if (_size($v.value.files.$model) === 0) return obj;
      obj.data = _cloneDeep(filesByFileReader.value);
      obj.valid = true;
      return obj;
    };
    const getBase64FileContent = (file) => {
      getBase64File(file).then((data) => {
        const content = _last(_split(data, "base64,"));
        filesByFileReader.value.push({ name: file.name, content: content });
      });
    };
    const getBase64File = (file) => {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve(reader.result);
        reader.onerror = (error) => reject(error);
      });
    };
    const getSourceValue = () => {
      let mode = "";
      if (drMode.value) mode = drModeKey.value;
      if (pccMode.value) mode = pccModeKey.value;
      if (prodMode.value) mode = prodModeKey.value;
      if (devMode.value) mode = devModeKey.value;
      if (_trim(mode) === "") return "";
      const filterArr = _filter(
        customModeDefaultData.value,
        (cv) => cv.key === mode
      );
      if (_size(filterArr) !== 1) return "";
      return _head(filterArr).value;
    };
    const getMantisAllProjects = () => {
      pwcMantisService
        .findAllProjects()
        .then(
          ({ data: projects }) =>
            (mantisProjects.value = _cloneDeep(projects.projects))
        )
        .catch(() => {})
        .finally(() => {});
    };
    const getMantisIssuesByUserId = (userId) => {
      if (_trim(userId) === "") return;
      pwcMantisService
        .findIssuesByUserId(userId)
        .then((res) => {
          mantisIssues.value = _cloneDeep(res);
          getReviewData();
        })
        .catch(() => {})
        .finally(() => {});
    };
    const getProjectUrl = () => {
      form.projectUrl = sessionStorage.getItem("beforeEnterPwc0601");
    };
    const getReviewData = () => {
      if (account.value === null) return;
      table.data = [];
      _forEach(mantisIssues.value, (v) => {
        if (!_includes(_keys(v), "custom_fields")) return;
        const filterArr = _filter(
          v.custom_fields,
          (vf) =>
            vf.field.name === getCFieldsData("userId", "", "value") &&
            vf.value === account.value.userId
        );
        if (_size(filterArr) !== 1) return;
        table.data.push(buildReviewData(v));
      });
      table.data = _orderBy(table.data, ["createdAtNum"], ["asc"]);
      table.totalItems = _size(table.data);
    };
    const getIssueFileByIssueIdAndFileId = (issueId, fileId) => {
      if (_trim(issueId) === "" || _trim(fileId) === "") return;
      pwcMantisService
        .downloadFileByIssueIdAndFileId(issueId, fileId)
        .then((res) => {
          const file = _head(res.files);
          const type = getFileType(file);
          if (type === null) return;
          const a = document.createElement("a");
          a.href = "data:" + type + ";base64," + file.content;
          a.download = file.filename;
          a.click();
        })
        .catch(() => {})
        .finally(() => {});
    };
    const getFileType = (file) => {
      let type = null;
      if (!_isObject(file)) return type;
      if (!_includes(_keys(file), "content_type")) return type;
      type = _head(_split(file.content_type, ";"));
      if (_trim(type) === "") return type;
      return type;
    };

    const buildAccountData = () => {
      const keys = _keys(account.value);
      form.orgName = _includes(keys, "wkutName")
        ? account.value.wkutName
        : getFormData(account.value, "orgName");
      form.chName = getFormData(contactsData.value, "chName");
      form.workTel = getFormData(contactsData.value, "workTel");
      form.mobileTel = getFormData(contactsData.value, "mobileTel");
      form.email = getFormData(contactsData.value, "email");
    };
    const buildCategoryOptions = () => {
      formOptions.project = [
        { text: "全球資訊網", value: "全球資訊網", index: 0 },
      ];
      if (_size(appFlattenMenus.value) === 0 || _size(openMenus.value) === 0)
        return;
      const filterAppMenus = _filter(
        appFlattenMenus.value,
        (av) => av?.meta?.layer === 2
      );
      _forEach(tmpMappingComponent, (tv) => {
        const show = _includes(tv.show, process.env.ENV_PROFILE);
        if (!show) return;
        const appMenuIndex = _findIndex(
          filterAppMenus,
          (omv) => omv?.meta?.label === tv.text
        );
        if (appMenuIndex !== -1)
          formOptions.project.push({
            text: tv.text,
            value: tv.text,
            index: appMenuIndex,
          });
      });
      formOptions.project = _orderBy(formOptions.project, ["index"], ["asc"]);
    };
    const buildReviewData = (data) => {
      let obj = { origin: _cloneDeep(data) };
      _forEach(table.fields, (f) => {
        if (f.key === "summary") obj[f.key] = _cloneDeep(data[f.key]);
        else if (f.key === "status") obj[f.key] = _cloneDeep(data[f.key].name);
        else if (f.key === "created_at" || f.key === "updated_at") {
          obj[f.key] = _cloneDeep(data[f.key]);
          if (f.key === "created_at")
            obj["createdAtNum"] =
              new Date().getTime() - new Date(data[f.key]).getTime();
        } else {
          const filterArr = _filter(
            data.custom_fields,
            (cf) => cf.field.name === f.label
          );
          if (_size(filterArr) === 1) obj[f.key] = _head(filterArr).value;
        }
      });
      return obj;
    };
    const buildDetailAttachmentsData = (origin) => {
      if (!_includes(_keys(origin), "attachments")) return [];
      if (_size(origin.attachments) === 0) return [];
      return _cloneDeep(origin.attachments);
    };
    const buildDetailDownloadsData = (origin) => {
      let arr = [];
      if (!_includes(_keys(origin), "notes")) return arr;
      if (_size(origin.notes) === 0) return arr;
      _forEach(origin.notes, (note) => {
        if (!_includes(_keys(note), "attachments")) return;
        if (_size(note.attachments) === 0) return;
        arr = _concat(arr, _cloneDeep(note.attachments));
      });
      return arr;
    };
    const buildDetailData = (data) => {
      let obj = { attachments: null, downloads: null };
      if (!_includes(_keys(data), "origin")) return obj;
      obj = _assign(obj, data.origin);
      _forEach(detailDataShowFields.value, (f) => {
        const value = getCFieldsData(f, "", "value");
        if (value === "") return;
        const filterArr = _filter(
          data.origin.custom_fields,
          (cf) => cf.field.name === value
        );
        if (_size(filterArr) !== 1) return;
        obj[f] = _head(filterArr).value;
      });
      obj.attachments = buildDetailAttachmentsData(data.origin);
      obj.downloads = buildDetailDownloadsData(data.origin);
      return obj;
    };

    const onTabClick = (tabKey) => {
      if (_trim(tabKey) === "") return;
      if (!_includes(_keys(tabClicked.value), tabKey)) return;
      if (tabKey === "review") {
        getMantisIssuesByUserId(account.value.userId);
        return;
      }
      if (tabClicked.value[tabKey]) return;
      tabClicked.value[tabKey] = !tabClicked.value[tabKey];
    };
    const onDownloadIssueFileClick = (download) => {
      getIssueFileByIssueIdAndFileId(detailData.value.id, download.id);
    };
    const onDetailBtnClick = (item) => {
      detailData.value = {};
      detailData.value = buildDetailData(item);
      showReportTable.value = false;
    };
    const onBackClick = () => {
      showReportTable.value = true;
    };

    const createNewIssueByAPI = (data) => {
      pwcMantisService
        .createIssueByData(data)
        .then(() => {
          $bvModals
            .msgBoxOk("回報成功，我們會盡快處理您的問題！即將回到首頁")
            .then((value) => {
              showSubmitBtn.value = false;
              navigateByNameAndParams("home", {});
            });
        })
        .catch(() => {
          submitCount.value += 1;
          if (submitCount.value === 5) {
            $bvModals
              .msgBoxOk(
                "抱歉，由於系統原因，回報失敗，請重新儲存一次或聯繫客服，我們會盡快處理您的問題！"
              )
              .then((value) => {
                showSubmitBtn.value = true;
              });
            return;
          }
          createNewIssueByAPI(data);
        })
        .finally(() => {
          showSubmitBtn.value = true;
          context.refs.verificationCode.refreshCode();
        });
    };
    const createNewIssue = () => {
      console.log($v);
      checkValidity().then((isOK: boolean) => {
        if (!isOK)
          $bvModals.msgBoxOk("欄位尚未填寫完畢，請於輸入完畢後再行送出！");
        else {
          submitCount.value = 0;
          const postData = getPostData();
          if (!postData.valid)
            $bvModals.msgBoxOk("資料錯誤，請檢查輸入資料的正確性！");
          else createNewIssueByAPI(postData.data);
        }
      });
    };
    const checkIssueFileType = (filesSize) => {
      filesSize -= 1;
      if (filesSize === -1) return;
      const filesData = new FormData();
      filesData.append("multipartFile", form.files[filesSize]);
      pwcMantisService
        .checkIssueFileTypeByData(filesData)
        .then((res) => {
          validFilesNum.value += 1;
          _size(form.files) === validFilesNum.value
            ? createNewIssue()
            : checkIssueFileType(filesSize);
        })
        .catch(notificationErrorHandler(notificationService));
    };
    const submit = () => {
      validFilesNum.value = 0;
      const filesSize = _size(form.files);
      filesSize !== 0 ? checkIssueFileType(filesSize) : createNewIssue();
    };

    watch(
      () => form.priority,
      (value) => {
        rules.mobileTel =
          value === "緊急"
            ? { required, mobileTel: mobileTel }
            : { mobileTel: mobileTel };
      },
      { immediate: false }
    );
    watch(
      () => form.files,
      (value) => {
        filesByFileReader.value = [];
        if (_size(form.files) !== 0)
          _forEach(value, (v) => {
            getBase64FileContent(v);
          });
      },
      { immediate: false }
    );

    getMantisAllProjects();
    getContactsData();
    getProjectUrl();
    buildCategoryOptions();

    onActivated(() => {
      reset();
      getProjectUrl();
      buildCategoryOptions();
      buildAccountData();
      if (!showSubmitBtn.value) showSubmitBtn.value = true;
    });

    return {
      isAuth,
      $v,
      $bvModals,
      formOptions,
      iFormGroupCheckClass,
      labelCols,
      contentCols,
      mLabelCols,
      mContentCols,
      detailContentCols,
      customFieldsDefaultData,
      form,
      table,
      showReportTable,
      detailData,
      deskTopDevice,
      showSubmitBtn,
      checkIssueStatus,
      reset,
      submit,
      validateState,
      getCFieldsData,
      onTabClick,
      onDetailBtnClick,
      onBackClick,
      onDownloadIssueFileClick,
      formatDate,
    };
  },
};
</script>
