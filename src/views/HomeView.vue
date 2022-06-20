<script setup>
import { ref, watchEffect } from "vue";
import { useRoute } from "vue-router";
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
import Modal from "../components/Modal.vue";

const showSidebar = ref(false);
const showMenu = ref(false);
const route = useRoute();

const showModal = () => {
  console.log("hello");
};

// watchEffect(() => route.params.modal, showModal());
const openModal = (cardID) => {
  for (const card of lists.value) {
    for (const task of card.list) {
      if (task.id === cardID) {
        task.showModal = true;
        document.body.classList.add("overflow-hidden");
      } else {
        card.showModal = false;
      }
    }
  }
};
const closeModal = (cardID) => {
  for (const card of lists.value) {
    for (const task of card.list) {
      if (task.id === cardID) {
        task.showModal = false;
        document.body.classList.add("overflow-hidden");
      } else {
        card.showModal = false;
      }
    }
  }
};

const addList = ref(false);

const toggleAddList = () => {
  addList.value = !addList.value;
};

const toggleCardForm = (cardID) => {
  for (const card of lists.value) {
    if (card.id === cardID) {
      card.formIsOpen = !card.formIsOpen;
    } else {
      card.formIsOpen = false;
    }
  }
};

const newList = ref("");

const addToList = () => {
  let name = newList.value;
  if (name) {
    lists.value.push({ name: name, list: [], formIsOpen: false, id: name });
    newList.value = "";
  }
};

const newTask = ref("");

const addTask = (cardID) => {
  let task = newTask.value;
  if (task) {
    for (const card of lists.value) {
      if (card.id === cardID) {
        card.list.push({
          title: task,
          id: task,
          showModal: false,
          addDescription: false,
        });
      }
      newTask.value = "";
    }
  }
};

const lists = ref([
  {
    name: "Guidelines",
    list: [
      {
        title: "From guidelines",
        id: "1",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 1,
  },
  {
    name: "Ideas",
    list: [
      { title: "From ideas", id: "2", showModal: false, addDescription: false },
    ],
    formIsOpen: false,
    id: 2,
  },
  {
    name: "Research",
    list: [
      {
        title: "From Research",
        id: "3",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 3,
  },
  {
    name: "Writing",
    list: [
      {
        title: "From Writing",
        id: "4",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    showModal: false,
    id: 4,
  },
  {
    name: "Draft Received",
    list: [
      {
        title: "From draft received",
        id: "5",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 5,
  },
  {
    name: "Editing",
    list: [
      {
        title: "From editing",
        id: "6",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 6,
  },
  {
    name: "Good to go",
    list: [
      {
        title: "From good to go",
        id: "7",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 7,
  },
  {
    name: "Ready to Publish",
    list: [
      {
        title: "From ready to publish",
        id: "8",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 8,
  },
  {
    name: "Published",
    list: [
      {
        title: "From published",
        id: "9",
        showModal: false,
        addDescription: false,
      },
    ],
    formIsOpen: false,
    id: 9,
  },
  {
    name: "Paid",
    list: [
      { title: "From paid", id: "10", showModal: false, addDescription: false },
    ],
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
            class="cursor-pointer mr-2 text-transparent/[0.5] hover:text-transparent/[0.3]"
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
          class="grow px-5 py-2 pb-12 text-[15px] flex overflow-y-hidden overflow-x-scroll space-x-2"
        >
          <draggable
            v-model="lists"
            item-key="id"
            animation="300"
            class="flex space-x-2 min-w-fit text-[15px]"
          >
            <template #item="{ element: list }">
              <div class="overflow-y-hidden">
                <div
                  class="bg-[#EBECF0] flex flex-col justify-between max-h-[97%] min-w-[300px] max-w-[300px] rounded p-2 space-y-2 overflow-hidden"
                >
                  <div
                    class="flex items-center font-semibold text-gray-700 pl-3"
                  >
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
                  <div class="space-y-2 h-fit overflow-y-scroll scrollbar-hide">
                    <!-- draggable list here -->
                    <div>
                      <draggable
                        v-model="list.list"
                        item-key="id"
                        group="card"
                        animation="300"
                        class="space-y-2"
                        fallbackTolerance="7"
                      >
                        <template #item="{ element }">
                          <div>
                            <div
                              @click="openModal(element.id)"
                              class="bg-white break-all group relative flex space-x-1 items-center drop-shadow hover:bg-gray-50 cursor-pointer text-gray-600 px-2 py-1 rounded"
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
                            <Modal
                              v-if="element.showModal == true"
                              @closeModal="closeModal(element.id)"
                            >
                              <div
                                class="relative space-y-12 pt-4 px-2 text-gray-600"
                              >
                                <div class="flex justify-between">
                                  <div
                                    class="flex grow space-x-3 md:ml-4 font-semibold"
                                  >
                                    <IconCard class="text-2xl" />
                                    <span
                                      contenteditable="true"
                                      class="w-full text-xl overflow-wrap break-all outline-blue-600 p-1"
                                      >{{ element.title }}</span
                                    >
                                  </div>
                                  <IconClose
                                    @click="closeModal(element.id)"
                                    class="text-2xl cursor-pointer p-1 mr-3 rounded-full w-8 h-8 hover:bg-gray-300"
                                  />
                                </div>

                                <div
                                  class="md:px-4 flex flex-col md:flex-row md:space-x-4 space-y-8 md:space-y-0"
                                >
                                  <!-- description and activity -->
                                  <div
                                    class="flex flex-col space-y-1 grow space-x-3 font-semibold"
                                  >
                                    <!-- description -->
                                    <div class="flex space-x-2 mb-7">
                                      <IconCard class="text-2xl" />
                                      <div
                                        class="flex flex-col w-full space-y-3"
                                      >
                                        <span class="text-lg">Description</span>
                                        <div
                                          v-if="!element.addDescription"
                                          @click="element.addDescription = true"
                                          class="w-full h-[60px] font-normal rounded bg-gray-200 cursor-pointer hover:bg-gray-300 transition-bg md:px-4 p-2"
                                        >
                                          Add a more detailed description...
                                        </div>
                                        <form
                                          v-else
                                          @submit.prevent=""
                                          class="w-full font-normal text-gray-600 space-y-2"
                                        >
                                          <textarea
                                            v-model="newTask.title"
                                            spellcheck="false"
                                            placeholder="Add a more detailed description..."
                                            class="w-full placeholder:text-gray-500 focus:outline-blue-600 placeholder:font-normal placeholder:text-base scrollbar-hide break-word resize-none overflow-wrap bg-white rounded-sm outline-none pb-6 p-2 h-[120px] px-4"
                                          ></textarea>
                                          <div class="flex items-center">
                                            <div
                                              class="flex items-center grow space-x-2"
                                            >
                                              <button
                                                class="outline-none rounded py-2 px-3 bg-[#0079BF] hover:brightness-90 text-white"
                                              >
                                                Save
                                              </button>
                                              <div
                                                @click="
                                                  element.addDescription = false
                                                "
                                                class="cursor-pointer rounded py-2 px-3 hover:bg-gray-300"
                                              >
                                                Cancel
                                              </div>
                                            </div>
                                            <div
                                              class="cursor-pointer rounded py-2 px-3 bg-gray-200 hover:bg-gray-300"
                                            >
                                              Formatting help
                                            </div>
                                          </div>
                                        </form>
                                      </div>
                                    </div>
                                    <!-- activity -->
                                    <div class="flex space-x-3">
                                      <IconCard class="text-2xl" />
                                      <div
                                        class="flex flex-col w-full space-y-3"
                                      >
                                        <div
                                          class="flex justify-between items-center"
                                        >
                                          <span class="text-lg">Activity</span>
                                          <div
                                            class="cursor-pointer font-normal rounded py-2 px-3 bg-gray-200 hover:bg-gray-300"
                                          >
                                            Show details
                                          </div>
                                        </div>
                                      </div>
                                    </div>

                                    <div class="flex space-x-2 pt-2">
                                      <div
                                        class="rounded-full bg-blue-500 p-1 w-8 h-8 flex items-center justify-center text-white"
                                      >
                                        JS
                                      </div>
                                      <form
                                        @submit.prevent=""
                                        class="w-full font-normal space-y-2 bg-white flex flex-col rounded drop-shadow"
                                      >
                                        <input
                                          class="peer w-full p-1 outline-none rounded px-4 placeholder:font-normal placeholder:text-gray-600"
                                          placeholder="Write a comment..."
                                        />
                                        <div
                                          class="hidden items-center justify-between peer-focus:flex px-4 py-1"
                                        >
                                          <button
                                            class="outline-none rounded py-1 px-3 bg-gray-200 hover:bg-gray-300"
                                          >
                                            Save
                                          </button>
                                        </div>
                                      </form>
                                    </div>
                                  </div>

                                  <!-- add to card and actions -->
                                  <div
                                    class="flex space-y-8 flex-col h-auto md:space-y-14"
                                  >
                                    <div class="space-y-2 w-full">
                                      <h3
                                        class="font-semibold text-sm text-gray-500"
                                      >
                                        Add to card
                                      </h3>
                                      <div
                                        class="md:space-y-2 grid grid-cols-2 w-full gap-2 gap-y-4 md:inline-block"
                                      >
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Members</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Labels</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Checklist</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Dates</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Attackments</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer t text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Cover</span>
                                        </div>
                                      </div>
                                    </div>
                                    <div class="space-y-2 w-full">
                                      <h3
                                        class="font-semibold text-sm text-gray-500"
                                      >
                                        Actions
                                      </h3>
                                      <div
                                        class="md:space-y-2 grid grid-cols-2 w-full gap-2 gap-y-4 md:inline-block"
                                      >
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Move</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Copy</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Watch</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Make template</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />*
                                          <span>Delete</span>
                                        </div>
                                        <div
                                          class="bg-gray-200 space-x-3 cursor-pointer t text-gray-600 rounded flex px-3 p-1 items-center hover:bg-gray-300 md:w-[180px]"
                                        >
                                          <IconBoard class="" />
                                          <span>Share</span>
                                        </div>
                                      </div>
                                    </div>
                                  </div>
                                </div>
                              </div>
                            </Modal>
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
                      v-model="newTask"
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
              </div>
            </template>
          </draggable>
          <div
            v-if="!addList"
            @click="toggleAddList"
            class="flex bg-[#6FCC89] hover:brightness-105 transition-[brightness] min-w-[300px] max-w-[300px] items-center space-x-2 px-4 py-1 rounded cursor-pointer h-[50px]"
          >
            <IconPlus class="text-lg" />
            <span>Add another list</span>
          </div>
          <form
            @submit.prevent="addToList()"
            v-else
            class="min-w-[300px] max-w-[300px] text-gray-500 space-y-2 p-2 rounded bg-[#EBECF0] h-fit"
          >
            <input
              v-model="newList"
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
                  @click="toggleAddList"
                  class="text-2xl cursor-pointer hover:text-gray-700"
                />
              </div>
            </div>
          </form>
        </div>
      </div>
      <!-- content ends here -->
      <!-- add a new list form -->
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
  background: rgb(209 213 219);
  height: fit-content;
  opacity: 0.3;
}

.sortable-drag {
  height: fit-content;
}
</style>
