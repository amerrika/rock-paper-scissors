<template>
    <div class="modal__backdrop" v-if="showModal">
        <div class="modal__content">
            <div>
                <h2>Rules</h2>
                <button @click="toggleModal" aria-label="Close modal">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" aria-hidden="true">
                        <path fill="#3B4262" fill-rule="evenodd"
                            d="M16.97 0l2.122 2.121-7.425 7.425 7.425 7.425-2.121 2.12-7.425-7.424-7.425 7.425L0 16.97l7.425-7.425L0 2.121 2.121 0l7.425 7.425L16.971 0z"
                            opacity=".45" />
                    </svg>
                </button>
            </div>
            <div class="mb-start-6">
                <img src="../assets/images/image-rules.svg" alt="Game rules" />
            </div>
        </div>
    </div>

    <Teleport to=".footer">
        <button @click="toggleModal" class="button" data-style="outline" aria-label="Open modal">Rules</button>
    </Teleport>
</template>

<script>
export default {
    data() {
        return {
            showModal: false,
        }
    },
    methods: {
        toggleModal() {
            this.showModal = !this.showModal
        }
    }
}
</script>
