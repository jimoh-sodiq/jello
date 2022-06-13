<script setup>
import { ref } from "vue";
import draggable from "vuedraggable";
import TheButton from "../components/TheButton.vue";
import IconHamburger from "../components/icons/IconHamburger.vue";
import IconDropdown from "../components/icons/IconDropdown.vue";
import IconBoard from "../components/icons/IconBoard.vue";
import IconStar from "../components/icons/IconStar.vue";
import IconUsers from "../components/icons/IconUsers.vue";
import IconFilter from "../components/icons/IconFilter.vue";
import IconThunderbolt from "../components/icons/IconThunderbolt.vue";
import IconMenu from "../components/icons/IconMenu.vue";
import IconCard from "../components/icons/IconCard.vue";
import IconPlus from "../components/icons/IconPlus.vue";
import IconPen from "../components/icons/IconPen.vue";
import IconClose from "../components/icons/IconClose.vue";

const showSidebar = ref(false);
const showMenu = ref(false);

const toggleCardForm = (cardID) => {
  for (const card of lists.value) {
    if (card.id === cardID) {
      card.formIsOpen = !card.formIsOpen;
    } else {
      card.formIsOpen = false;
    }
  }
};

const addTask = (cardID) => {
  if (newTask.value) {
    for (const card of lists.value) {
      if (card.id === cardID) {
        card.list = [...card.list, newTask.value];
      }
      newTask.value = {
        title: "",
        id: ((Math.random() / 5) * 8) / 6 / 3 / 6 + "random",
      };
    }
  }
};

const newTask = ref({
  title: "",
  id: ((Math.random() / 5) * 8) / 6 / 3 / 6 + "random",
});

const lists = ref([
  {
    name: "Guidelines",
    list: [{ title: "From guidelines", id: "listonecard" }],
    formIsOpen: false,
    id: 1,
  },
  {
    name: "Ideas",
    list: [{ title: "From ideas", id: "listtwocard" }],
    formIsOpen: false,
    id: 2,
  },
  {
    name: "Research",
    list: [{ title: "From Research", id: "listtwocard" }],
    formIsOpen: false,
    id:3,
  },
  {
    name: "Writing",
    list: [{ title: "From Writing", id: "listtwocard" }],
    formIsOpen: false,
    id: 4,
  },
  {
    name: "Draft Received",
    list: [{ title: "From draft received", id: "listtwocard" }],
    formIsOpen: false,
    id: 5,
  },
  {
    name: "Editing",
    list: [{ title: "From editing", id: "listtwocard" }],
    formIsOpen: false,
    id: 6,
  },
  {
    name: "Good to go",
    list: [{ title: "From good to go", id: "listtwocard" }],
    formIsOpen: false,
    id: 7,
  },
  {
    name: "Ready to Publish",
    list: [{ title: "From ready to publish", id: "listtwocard" }],
    formIsOpen: false,
    id: 8,
  },
  {
    name: "Published",
    list: [{ title: "From published", id: "listtwocard" }],
    formIsOpen: false,
    id: 9,
  },
  {
    name: "Paid",
    list: [{ title: "From paid", id: "listtwocard" }],
    formIsOpen: false,
    id: 10,
  },
]);
</script>

<template>
  <main class="w-screen h-screen overflow-hidden text-white">
    <nav class="h-12 bg-[#3FA05A] w-screen">nav here</nav>
    <section class="h-full w-full flex overflow-hidden">
      <!-- sidebar here -->
      <div
        class="h-[100%] bg-[#3FA05A] transition-[width] duration-[.35s]"
        :class="showSidebar ? 'w-[44rem]' : 'w-0'"
      >
        sidebar here
      </div>
      <!-- sidebar ends here -->

      <!-- content here -->
      <div
        class="h-full grow bg-[#4BBF6B] relative space-y-4 flex flex-col overflow-hidden"
      >
        <!-- content navbar here -->
        <div
          class="w-full space-y-2 grid md:flex grid-col-4 md:flex-row flex-wrap items-center px-4"
        >
          <div
            @click="showSidebar = !showSidebar"
            title="Expand sidebar"
            class="cursor-pointer mr-2 text-green-800 flex"
          >
            <IconHamburger />
          </div>
          <div class="flex flex-wrap space-x-2 md:space-x-4 items-center mt-2">
            <TheButton>
              <template #leftIcon><IconBoard class="mr-2" /></template>
              <template #default>Board</template>
              <template #rightIcon><IconDropdown /></template>
            </TheButton>
            <div
              class="flex flex-wrap items-center whitespace-nowrap rounded px-2 transition-[background-color] capitalize cursor-pointer font-bold text-xl hover:bg-[#6FCC89] hover:brigtness-105 h-[35px]"
            >
              <span>Kanban Template</span>
            </div>
            <TheButton class="group hover:brightness-100"
              ><IconStar
                class="text-xl group-hover:scale-110 group-hover:text-yellow-300"
            /></TheButton>
          </div>
          <span class="mx-2 font-thin text-gray-300 hidden md:inline-block"
            >|</span
          >
          <div class="flex flex-wrap items-center">
            <TheButton>
              <template #default>Jello Workspace</template>
            </TheButton>
            <span class="font-thin mx-2 text-gray-300 hidden md:inline-block"
              >|</span
            >
            <TheButton>
              <template #leftIcon><IconUsers class="mr-2 text-xl" /></template>
              <template #default>Workspace visible</template>
            </TheButton>
          </div>
          <span class="font-thin mx-2 text-gray-300 hidden md:inline-block"
            >|</span
          >
          <div class="grow">js invite</div>
          <div class="flex justify-end items-center space-x-2 grow">
            <TheButton>
              <template #leftIcon
                ><IconThunderbolt class="mr-2 text-lg"
              /></template>
              <template #default>Automation</template>
            </TheButton>
            <TheButton>
              <template #leftIcon><IconFilter class="mr-2 text-lg" /></template>
              <template #default>Filter</template>
            </TheButton>
            <TheButton @click="showMenu = !showMenu">
              <template #leftIcon><IconMenu class="mr-2 text-2xl" /></template>
              <template #default>Show menu</template>
            </TheButton>
          </div>
        </div>
        <!-- content navbar ends here -->

        <div
          class="grow px-5 py-2 space-x-2 pb-12 overflow-x-scroll flex text-[15px] overflow-y-hidden"
        >
          <div
            v-for="list in lists"
            :key="list.id"
            class="bg-[#EBECF0] h-fit flex flex-col justify-between max-h-[97%] min-w-[300px] max-w-[300px] rounded p-2 space-y-2 overflow-hidden"
          >
            <div class="flex items-center font-semibold text-gray-700 pl-3">
              <div
                class="w-full overflow-wrap text-[15px] p-1 flex items-center break-all cursor-pointer outline-blue-600"
                contentEditable="true"
                spellcheck="false"
                @keyup.enter="(e) => e.target.blur()"
              >
                {{ list.name }}
              </div>
              <div
                class="hover:bg-gray-300 h-9 w-9 transition self-start duration-[0.2s] rounded flex items-center justify-center cursor-pointer"
              >
                <IconMenu class="h-full text-2xl text-gray-500" />
              </div>
            </div>
            <!-- task list here-->
            <div class="space-y-2 overflow-y-scroll scrollbar-hide">
              <!-- draggable list here -->
              <div class="overflow-y-scroll scrollbar-hide">
                <draggable
                  v-model="list.list"
                  item-key="id"
                  group="card"
                  animation="300"
                  class="space-y-2"
                >
                  <template #item="{ element }">
                    <div
                      class="bg-white break-all group relative flex space-x-1 items-center  drop-shadow hover:bg-gray-50 cursor-pointer text-gray-600 px-2 py-1 rounded"
                    >
                      <p class="grow break-word">
                        {{ element.title }}
                      </p>

                      <div
                        class="flex self-start group-hover:visible invisible items-center justify-center bg-gray-50 hover:bg-gray-300 rounded p-2"
                      >
                        <IconPen class="text-base text-gray-800" />
                      </div>
                    </div>
                  </template>
                </draggable>
              </div>
              <!-- draggable list ends here -->

              <!-- add a card here -->
            </div>
            <!-- New card form here -->
            <div
              v-if="list.formIsOpen == false"
              class="flex w-full items-center cursor-pointer text-gray-500 py-1"
            >
              <div
                @click="toggleCardForm(list.id)"
                class="flex grow items-center space-x-2 px-4 py-1 rounded hover:bg-gray-300"
              >
                <IconPlus class="text-lg" />
                <span>Add a card</span>
              </div>
              <div
                class="flex items-center justify-center hover:bg-gray-300 rounded p-1"
              >
                <IconCard class="text-lg" />
              </div>
            </div>
            <form
              @submit.prevent="addTask(list.id)"
              class="w-full text-gray-600 space-y-1"
              v-else
            >
              <textarea
                v-model="newTask.title"
                spellcheck="false"
                placeholder="Enter a title for this card..."
                class="w-full scrollbar-hide break-word resize-none overflow-wrap bg-white drop-shadow rounded outline-none pb-6 p-2 h-auto"
              ></textarea>
              <div class="flex items-center">
                <div class="flex items-center grow space-x-2">
                  <button
                    class="outline-none rounded py-2 px-3 bg-[#0079BF] hover:brightness-90 text-white font-semibold"
                  >
                    Add card
                  </button>
                  <IconClose
                    @click="toggleCardForm(list.id)"
                    class="text-2xl cursor-pointer hover:text-gray-700"
                  />
                </div>
                <div
                  class="hover:bg-gray-300 h-9 w-9 transition duration-[0.2s] rounded flex items-center justify-center cursor-pointer"
                >
                  <IconMenu class="h-full text-2xl text-gray-500" />
                </div>
              </div>
            </form>
          </div>
          <!-- add a new list form -->
          <form
            class="min-w-[300px] max-w-[300px] text-gray-500 space-y-2 p-2 rounded bg-[#EBECF0] h-fit"
          >
            <input
              spellcheck="false"
              placeholder="Enter a title for this list..."
              class="w-full break-all border-[2px] scrollbar-hide border-[#0079BF] overflow-wrap bg-white drop-shadow rounded outline-none p-2 h-auto"
            />
            <div class="flex items-center">
              <div class="flex items-center grow space-x-2">
                <button
                  class="outline-none rounded py-2 px-3 bg-[#0079BF] hover:brightness-90 text-white font-semibold"
                >
                  Add list
                </button>
                <IconClose
                  class="text-2xl cursor-pointer hover:text-gray-700"
                />
              </div>
            </div>
          </form>
          <!-- add a new list form ends here -->
        </div>
      </div>
      <!-- content ends here -->

      <!-- menu sectio start here -->
      <div
        class="h-[100%] bg-[#3FA05A] transition-[width] duration-[.35s]"
        :class="showMenu ? 'w-[44rem]' : 'w-0'"
      >
        Menu here
      </div>
      <!-- menu section ends here -->
    </section>
  </main>
</template>

<style scoped>
.sortable-ghost {
  background-color: rgb(209 213 219);
}
.sortable-drag {
}
</style>
