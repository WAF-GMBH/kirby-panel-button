<template>
    <k-field class="k-button-field" :label="label" :help="help">

        <div class="k-button-field-button-wrapper">

            <button v-if="!isLoading" type="button" data-size="sm" data-has-icon="true" data-has-text="true" class="k-button-field-button k-button k-box" :data-theme="theme ? theme : 'neutral'" data-variant="filled" @click="onClick">
                <span class="k-button-icon"><k-icon :type="icon"/></span>
                <span class="k-button-text">{{ text }}</span>
            </button>
            
            <div v-if="isLoading && !hasError" type="button" data-size="sm" data-has-icon="true" data-has-text="true" class="k-button k-button-disabled k-box" data-variant="filled" data-disabled="true">
                <span class="k-button-icon"><k-icon :type="dots"/></span>
                <span class="k-button-text">Please wait</span>
            </div>
            
            <div v-if="hasError" type="button" data-size="sm" data-has-icon="true" data-has-text="true" class="k-button k-button-disabled k-box" data-disabled="true" data-variant="filled" data-theme="negative">
                <span class="k-button-icon"><k-icon :type="alert"/></span>
                <span class="k-button-text">Error</span>
            </div>

        </div>
            
    </k-field>
</template>

<script>

    import { openUrlInNewTab, triggerWebhook } from "./methods";

    export default {
        props: {
            label: String,
            text: String,
            url: String,
            theme: String,
            icon: String,
            open: Boolean,
            reload: Boolean,
            help: String,
            isLoading: true,
            hasError: false
        },
        methods: {
            async onClick(){
                if( this.open === true ){
                    openUrlInNewTab( this );
                } else {
                    triggerWebhook( this );
                }
            }
        }
    }
</script>

<style>

    p {
        margin-bottom: var(--spacing-2);
    }

    .k-button-field-button {
        display: flex;
        justify-content: flex-start;
        width: 100%;
    }

</style>