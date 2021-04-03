<template>
    <img
        v-if="!Array.isArray(sources)"
        :src="sources"
        :class="classes"
        :alt="altText"
        :title="titleText"
    />
    <picture v-else>
        <template v-for="(source, key) in sources">
            <source
                :srcset="source"
                :type="'image/' + GetType(source)"
                :key="key"
            />
        </template>
        <img
            :src="GetPng(sources)"
            :class="classes"
            :alt="altText"
            :title="titleText"
        />
    </picture>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.component('MeImage', {
    props: {
        altText: {
            type: String,
            required: true
        },
        classes: {
            type: String,
            required: false
        },
        sources: {
            type: [String, Array],
            required: true
        },
        titleText: {
            type: String,
            required: false
        }
    },
    methods: {
        GetPng(sources: string[]): string {

            for (let source of sources) {
                if (source.split('.').pop() === 'png') {
                    return source;
                }
            }

            return '';
        },
        GetType(source: string): string {

            const extension: string = source.split('.').pop() ?? '';
            switch(extension) {
                case 'avif':
                case 'webp':
                case 'jpeg':
                case 'png':
                    return extension;
                case 'jpg':
                    return 'jpeg';
            }

            return '';
        }
    }
});
</script>
