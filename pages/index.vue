<template>
    <article>
        <h1>Marian Schwandt</h1>
        <p>{{ $t('titleNote') }}</p>
        <MeDivider />
        <p>
            {{ $t('name', ['Marian Schwandt']) }}
            {{ $t('place', ['Magdeburg']) }}
        </p>
        <p>
            {{ $t('devStarting') }}
        </p>
        <p>
            {{ $t('privateDev') }}
        </p>
        <p>
            <i18n path="githubLink" tag="label" for="githubProfileText">
                <MeLink :displayName="$t('githubProfileText')" :url="githubUrl" />
            </i18n>
        </p>
        <MeDivider />
        <p>
            <MeLink
                class="github-link"
                displayName="GitHub"
                icon="github"
                :url="githubUrl"
            />
        </p>
    </article>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
    data: function() {
        return {
            githubUrl: 'https://github.com/mschwandt98'
        }
    }
});
</script>

<style lang="scss">
@import '~assets/icons.css';

.github-link {
    align-items: center;
    display: flex;
    font-size: 1.5em !important;
    gap: .25em;
    width: fit-content;

    i {
        color: #24292e;
    }

    &:hover span {
        color: #24292e;
    }

    span {
        color: #b5b5b5;
        transition: color .2s ease-in;

        &::after {
            background-color: #24292e !important;
        }
    }
}
</style>
