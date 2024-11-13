<template>
  <UContainer
    class="fn-field-validation-container"
    @contextmenu.prevent="onContextMenu"
  >
    <UButton icon="i-heroicons-magnifying-glass" />
    <UAlert title="APT! APT!" />
    <UAvatar
      src="https://avatars.githubusercontent.com/u/739984?v=4"
      alt="Avatar"
    />
    <UBadge>Badge</UBadge>
    <UBreadcrumb divider="/" :links="links" />
    <UButton
      icon="i-heroicons-pencil-square"
      size="sm"
      color="primary"
      variant="solid"
      label="Button"
      :trailing="false"
    />
    <UCard>
      <template #header>
        <Placeholder class="h-8" />
      </template>

      <Placeholder class="h-32" />

      <template #footer>
        <Placeholder class="h-8" />
      </template>
    </UCard>
    <UCarousel
      v-slot="{ item }"
      :items="items"
      :ui="{ item: 'basis-full' }"
      class="rounded-lg overflow-hidden"
      arrows
    >
      <img :src="item" class="w-64 mx-auto" draggable="false" />
    </UCarousel>
    <UCheckbox label="Label" />
    <UChip>
      <UButton icon="i-heroicons-inbox" color="gray" />
    </UChip>
    <UCommandPalette
      v-model="selected"
      multiple
      nullable
      :autoselect="false"
      :groups="[{ key: 'people', commands: people }]"
      :fuse="{ resultLimit: 6, fuseOptions: { threshold: 0.1 } }"
    />
    <UContextMenu v-model="isOpen" :virtual-element="virtualElement">
      <div class="p-4">Menu</div>
    </UContextMenu>
    <UDropdown :items="dropdownItems" :popper="{ placement: 'bottom-start' }">
      <UButton
        color="white"
        label="Options"
        trailing-icon="i-heroicons-chevron-down-20-solid"
      />
    </UDropdown>
    <UHorizontalNavigation
      :links="NavigationLinks"
      class="border-b border-gray-200 dark:border-gray-800"
    />
    <UInputMenu v-model="selectedPeople" :options="InputMenuPeople" />
    <UButton label="Open" @click="isModalOpen = true" />
    <UModal v-model="isModalOpen" prevent-close>
      <UCard
        :ui="{
          ring: '',
          divide: 'divide-y divide-gray-100 dark:divide-gray-800',
        }"
      >
        <template #header>
          <div class="flex items-center justify-between">
            <h3
              class="text-base font-semibold leading-6 text-gray-900 dark:text-white"
            >
              Modal
            </h3>
            <UButton
              color="gray"
              variant="ghost"
              icon="i-heroicons-x-mark-20-solid"
              class="-my-1"
              @click="isModalOpen = false"
            />
          </div>
        </template>
        <Placeholder class="h-full" />
      </UCard>
    </UModal>
    <UButton
      label="Show toast"
      @click.stop="toast.add({ title: 'Hello world!' })"
    />
    <UPagination
      v-model="page"
      :page-count="5"
      :total="pageItems.length"
      :to="(page: number) => ({query: { page }, hash: '#links'})"
      show-last
      show-first
    />
    <URange :step="20" v-model="value" />
    <USelect v-model="country" :options="countries" option-attribute="name" />
    <div class="flex items-center space-x-4">
      <USkeleton class="h-12 w-12" :ui="{ rounded: 'rounded-full' }" />
      <div class="space-y-2">
        <USkeleton class="h-4 w-[250px]" />
        <USkeleton class="h-4 w-[200px]" />
      </div>
    </div>

    <UDivider
      label="Nuxt UI"
      :ui="{ label: 'text-primary-500 dark:text-primary-400' }"
    />
    <UCard>
      <div class="space-y-4">
        <UFormGroup label="Email" name="email">
          <UInput v-model="form.email" />
        </UFormGroup>
        <UFormGroup label="Password" name="password">
          <UInput v-model="form.password" type="password" />
        </UFormGroup>
        <UFormGroup label="file" name="file">
          <UInput type="file" size="sm" icon="i-heroicons-folder" />
        </UFormGroup>
        <UButton label="submit" color="gray" block @click.stop="submit" />
      </div>
    </UCard>
    <UNotifications />
  </UContainer>
</template>

<script lang="ts">
import { useMouse, useWindowScroll } from "@vueuse/core";
export default {
  name: "fn-field-validation",
  components: {},
  setup() {
    const people = [
      { id: 1, label: "Wade Cooper" },
      { id: 2, label: "Arlene Mccoy" },
      { id: 3, label: "Devon Webb" },
      { id: 4, label: "Tom Cook" },
      { id: 5, label: "Tanya Fox" },
      { id: 6, label: "Hellen Schmidt" },
      { id: 7, label: "Caroline Schultz" },
      { id: 8, label: "Mason Heaney" },
      { id: 9, label: "Claudie Smitham" },
      { id: 10, label: "Emil Schaefer" },
    ];
    const selected = ref([people[3]]);
    const links = [
      { label: "Home", icon: "i-heroicons-home", to: "/" },
      { label: "Navigation", icon: "i-heroicons-square-3-stack-3d" },
      { label: "Breadcrumb", icon: "i-heroicons-link" },
    ];
    const items = [
      "https://picsum.photos/600/800?random=1",
      "https://picsum.photos/600/800?random=2",
      "https://picsum.photos/600/800?random=3",
      "https://picsum.photos/600/800?random=4",
      "https://picsum.photos/600/800?random=5",
      "https://picsum.photos/600/800?random=6",
    ];
    const { x, y } = useMouse();
    const { y: windowY } = useWindowScroll();
    const isOpen = ref(false);
    const virtualElement = ref({ getBoundingClientRect: () => ({}) });

    const onContextMenu = () => {
      const top = unref(y) - unref(windowY);
      const left = unref(x);
      virtualElement.value.getBoundingClientRect = () => ({
        width: 0,
        height: 0,
        top,
        left,
      });
      isOpen.value = true;
    };
    const form = reactive({ email: "mail@example.com", password: "password" });
    const dropdownItems = [
      [
        {
          label: "Profile",
          avatar: {
            src: "https://avatars.githubusercontent.com/u/739984?v=4",
          },
        },
      ],
      [
        {
          label: "Edit",
          icon: "i-heroicons-pencil-square-20-solid",
          shortcuts: ["E"],
          click: () => {
            console.log("Edit");
          },
        },
        {
          label: "Duplicate",
          icon: "i-heroicons-document-duplicate-20-solid",
          shortcuts: ["D"],
          disabled: true,
        },
      ],
      [
        {
          label: "Archive",
          icon: "i-heroicons-archive-box-20-solid",
        },
        {
          label: "Move",
          icon: "i-heroicons-arrow-right-circle-20-solid",
        },
      ],
      [
        {
          label: "Delete",
          icon: "i-heroicons-trash-20-solid",
          shortcuts: ["⌘", "D"],
        },
      ],
    ];
    const NavigationLinks = [
      {
        label: "Profile",
        avatar: {
          src: "https://avatars.githubusercontent.com/u/739984?v=4",
        },
        badge: 100,
      },
      {
        label: "Installation",
        icon: "i-heroicons-home",
        to: "/getting-started/installation",
      },
      {
        label: "Horizontal Navigation",
        icon: "i-heroicons-chart-bar",
        to: "/components/horizontal-navigation",
      },
      {
        label: "Command Palette",
        icon: "i-heroicons-command-line",
        to: "/components/command-palette",
      },
    ];
    const InputMenuPeople = [
      "Wade Cooper",
      "Arlene Mccoy",
      "Devon Webb",
      "Tom Cook",
      "Tanya Fox",
      "Hellen Schmidt",
      "Caroline Schultz",
      "Mason Heaney",
      "Claudie Smitham",
      "Emil Schaefer",
    ];
    const selectedPeople = ref(InputMenuPeople[0]);
    const isModalOpen = ref(false);
    const toast = useToast();
    const page = ref(1);
    const pageItems = ref(Array(50));
    const value = ref(50);
    const country = ref("CA");
    const countries = [
      { name: "United States", value: "US" },
      { name: "Canada", value: "CA", disabled: true },
      { name: "Mexico", value: "MX" },
    ];

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

    const submit = () => {
      console.log("submit");
    };

    return {
      submit,
      form,
      selected,
      selectedPeople,
      people,
      InputMenuPeople,
      links,
      NavigationLinks,
      items,
      dropdownItems,
      isOpen,
      isModalOpen,
      virtualElement,
      onContextMenu,
      toast,
      page,
      pageItems,
      value,
      country,
      countries,
    };
  },
};
</script>
