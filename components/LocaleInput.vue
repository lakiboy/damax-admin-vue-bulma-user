<template>
    <b-select @input="value => $emit('input', value ? value : '')"
              :loading="loading"
              :value="current"
              :disabled="disabled"
              :expanded="expanded"
              :id="id"
              :placeholder="$t('user.label.choose_locale')">
        <option v-for="item in options" :value="item.code">{{ item.name }}</option>
    </b-select>
</template>

<script>
import { intl as api } from '../api'

export default {
    model: { prop: 'selected' },

    props: {
        id: String,
        selected: String,
        disabled: { type: Boolean, default: false },
        expanded: { type: Boolean, default: true }
    },

    data () {
        return { options: null }
    },

    computed: {
        loading () {
            return this.options === null
        },

        current () {
            return this.loading ? null : this.selected
        }
    },

    async created () {
        this.options = await api.localesList()
    }
}
</script>
