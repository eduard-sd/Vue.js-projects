<template>
    <div class="search-wrapper">
        <input
                type="text"
                :class="this.index"
                v-model="searchText"
                placeholder="Поиск"
                @blur="searchBlur"
        >
    </div>
</template>

<script>

export default {
    name: 'SearchFilter',
    props: {
        index: Number,
        lastSearchedText: String,
    },
    data() {
        return {
            searchText: '',
        };
    },

    watch: {
        searchText(text) {
            this.$emit('searchText', text);
        },
    },

    created() {
        this.$parent.$on('searchLast', (data) => {
            this.searchText = data.word;
        });
    },

    methods: {
        searchBlur(event) {
            if (this.searchText[this.index]) {
                this.$emit('searchBlur', event);
            }
        },
    },
};
</script>

<style scoped lang="sass">
    .search-wrapper
        display: flex
        flex-direction: column
</style>
