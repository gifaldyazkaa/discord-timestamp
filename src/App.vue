<template>
    <div class="app__box">
        <div class="app__content">
            <div class="app__title">
                <h1>🕑 Discord Timestamp</h1>
                <p>Tools to create discord-formatted timestamp</p>
            </div>
            <div class="app__input">
                <h3 class="app__input_label">📅 Date & Time</h3>
                <!-- prettier-ignore-attribute -->
                <Datepicker :modelValue="date" @update:modelValue="handleDate" :dark=true></Datepicker>
                <h3 class="app__input_label" id="format__title">📄 Format</h3>
                <select
                    v-model="format"
                    @load="handleSelect"
                    @input="handleSelect"
                    name="format"
                    class="dp__input dp__theme_dark app__format"
                    id="app__format"
                >
                    <option value="t">Short Time</option>
                    <option value="T">Long Time</option>
                    <option value="d">Short Date</option>
                    <option value="D">Long Date</option>
                    <option value="f">Short Date/Time</option>
                    <option value="F">Long Date/Time</option>
                    <option value="R">Relative Time</option>
                </select>
            </div>
            <div class="app__result">
                <div class="app__result_date">{{ out }}</div>
                <div class="app__result_formatted">{{ template }}</div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';
import m from 'moment';

export default {
    name: 'App',
    components: { Datepicker },
    data() {
        return {
            date: m().set('seconds', 0),
            format: 'f',
            template: null,
            out: null,
        };
    },
    methods: {
        handleDate(data) {
            const formatted = `<t:${this.date!.unix()}:f>`;
            this.date = m(data);
            this.template = formatted;
        },
        handleSelect(e) {
            const value = e.target.value;
            const formatted = `<t:${this.date!.unix()}:${value}>`;
            if (value === 't') {
                this.out = m(this.date).format('LT');
                this.template = formatted;
            }
            if (value === 'T') {
                this.out = m(this.date).format('LTS');
                this.template = formatted;
            }
            if (value === 'd') {
                this.out = m(this.date).format('L');
                this.template = formatted;
            }
            if (value === 'D') {
                this.out = m(this.date).format('LL');
                this.template = formatted;
            }
            if (value === 'f') {
                this.out = m(this.date).format('LLL');
                this.template = formatted;
            }
            if (value === 'F') {
                this.out = m(this.date).format('LLLL');
                this.template = formatted;
            }
            if (value === 'R') {
                this.out = m(this.date).fromNow();
                this.template = formatted;
            }
        },
    },
    mounted() {
        if (this.format === 'f') {
            const formatted = `<t:${this.date!.unix()}:f>`;
            this.out = m(this.date).format('D MMMM YYYY h:mm');
            this.template = formatted;
        }
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
        // margin-left: 5rem;
    }
    &__input {
        margin-top: 1.3rem;
        &_label {
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
    &__result {
        display: flex;
        justify-content: center;
        font-family: 'Lexend', sans-serif;
        &_date,
        &_formatted {
            display: inline-block;
            background: #212121;
            // width: 13rem;
            // height: 3.5rem;
            margin-top: 1.3rem;
            text-align: center;
            padding: 16px;
            border-radius: 10px;
        }
        &_formatted {
            margin-left: 8px;
        }
    }
}
</style>
