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
                :srcset="GetSourcSet(source)"
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
            required: false,
            default: ''
        },
        sizes: {
            type: Array,
            required: false,
            default: []
        },
        sources: {
            type: [String, Array],
            required: true
        },
        titleText: {
            type: String,
            required: false,
            default: ''
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
        GetSourcSet(source: string): string {

            if (this.sizes.length) {

                let splitted: string[] = source.split('.');
                let indexBeforeType: number = splitted.length - 2;
                let sourceset: string = '';
                this.sizes.forEach(size => {
                    let copySplitted = [...splitted];
                    copySplitted[indexBeforeType] += `-${size}`;
                    sourceset += copySplitted.join('.') + ` ${size}w,`;
                });

                let lastSize: number = [...this.sizes].pop() as number;
                sourceset += source + ' ' + (lastSize / 2 + lastSize) + 'w';

                return sourceset;
            }

            return source;
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
