<template>
    <div class="app__box">
        <div class="app__content">
            <div class="app__title">
                <h1>Discord Time</h1>
                <p>Tools to create discord-formatted timestamp</p>
            </div>
            <div class="app__input">
                <h3 class="app__input__label">Date & Time</h3>
                <!-- prettier-ignore-attribute -->
                <Datepicker v-model="date" :dark=true></Datepicker>
                <h3 class="app__input__label" id="format__title">Format</h3>
                <select name="format" class="dp__input dp__theme_dark app__format" id="app__format">
                    <option value="short_date">Short Date</option>
                    <option value="long_date">Long Date</option>
                </select>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';

export default {
    name: 'App',
    components: { Datepicker },
    data() {
        return {
            date: new Date(),
            options: [
                { label: 'Short Time', value: 'short_date' },
                { label: 'Long Time', value: 'long_date' },
            ],
        };
    },
};
</script>

<style lang="scss">
@import './styles/mixin';
.app {
    &__box {
        position: absolute;
        width: 100vh;
        height: 50vh;
        left: 50%;
        top: 50%;
        background: #262f41;
        transform: translate(-50%, -50%);
        border-radius: 15px;
        @include on-mobile {
            height: auto;
            width: 100%;
        }
    }
    &__content {
        margin: 1rem;
    }
    &__title {
        margin-top: 2rem;
        margin-left: 5rem;
    }
    &__input {
        margin-top: 1.3rem;
        &__label {
            margin-bottom: 0.4rem;
            &#format__title {
                margin-top: 0.4rem;
            }
        }
        .dp__input {
            font-family: 'Lexend', sans-serif;
            &.app__format {
                appearance: none;
                cursor: pointer;
            }
        }
    }
}
</style>
