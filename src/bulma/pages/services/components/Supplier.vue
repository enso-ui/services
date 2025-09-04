<template>
    <div class="columns supplier-wrapper">
        <div class="column is-3">
            <div class="field">
                <label class="label">
                    {{ i18n('Supplier') }}
                </label>
                <div class="control">
                    <input class="input"
                        :value="supplier.name"
                        readonly>
                </div>
            </div>
        </div>
        <div class="column">
            <div class="field">
                <label class="label">
                    {{ i18n('Acquisition Price') }}
                </label>
                <div class="control">
                    <input class="input"
                        :value="supplier.cost.acquisitionPrice"
                        v-select-on-focus
                        @input="$emit('acquisition-price-updated', $event.target.value);
                            clearError('acquisitionPrice');">
                </div>
                <p class="help is-danger"
                    v-if="hasError('acquisitionPrice')">
                    {{ getError('acquisitionPrice') }}
                </p>
            </div>
        </div>
        <div class="column is-narrow">
            <div class="field">
                <label class="label">
                    {{ i18n('Mapped At') }}
                </label>
                <div class="control">
                    <input class="input timestamp"
                        :value="supplier.cost.createdAt"
                        readonly>
                </div>
            </div>
        </div>
        <div class="column is-narrow">
            <div class="field">
                <label class="label">
                    {{ i18n('Updated At') }}
                </label>
                <div class="control">
                    <input class="input timestamp"
                        :value="supplier.cost.updatedAt"
                        readonly>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { focus, selectOnFocus } from '@enso-ui/directives';
import Errors from '@enso-ui/laravel-validation';

export default {
    name: 'Supplier',

    directives: { focus, selectOnFocus },

    inject: ['i18n'],

    props: {
        errors: {
            type: Errors,
            required: true,
        },
        index: {
            type: Number,
            required: true,
        },
        supplier: {
            type: Object,
            required: true,
        },
    },

    emits: ['acquisition-price-updated', 'part-number-updated'],

    methods: {
        clearError(field) {
            this.errors.clear(field);
        },
        errorKey(field) {
            return `suppliers.${this.index}.cost.${field}`;
        },
        getError(field) {
            const key = this.errorKey(field);

            return this.errors.get(key)
                .replace(key, 'field')
                .replace('field field', 'field');
        },
        hasError(field) {
            return this.errors.has(this.errorKey(field));
        },
    },
};
</script>

<style lang="scss">
.supplier-wrapper .timestamp {
    width: 7em;
}
</style>
