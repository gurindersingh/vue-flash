<template>
    <transition name="slide-left">
        <div class="notify p-fx t-0 r-0 bgc-green d-f ai-c mt-3 mr-3 py-4 px-5 bdr-10 z-fixed"
             :class="classes"
             v-if="show">
            <svg width="30" height="30" class="fill-white">
                <use :xlink:href="icon"></use>
            </svg>
            <p class="c-white mb-0 ml-3" v-html="message"></p>
        </div>
    </transition>
</template>

<script>
    export default {
        props: ['dataLevel', 'dataMessage', 'dataTimeout'],

        data() {
            return {
                message: null,
                level: null,
                show: false,
                timeout: this.dataTimeout ? this.dataTimeout : 3000,
                interval: null
            }
        },

        created() {
            if (this.dataMessage) {
                this.flash({message: this.dataMessage, level: this.dataLevel});
            }

            window.Event.listen('flash', data => {
                this.show = false;
                clearTimeout(this.interval);
                this.flash(data);
            });
        },

        methods: {
            flash(data) {

                if (data) {
                    this.message = data.message;
                    this.level = data.level;
                    this.timeout = data.timeout ? data.timeout : this.timeout;
                }

                this.$nextTick(() => {
                    this.show = true;
                    this.interval = setTimeout(() => this.show = false, this.timeout);
                });

            }
        },

        computed: {
            classes() {
                return {
                    'grad-error': this.level === 'error',
                    'grad-info': this.level === 'info',
                    'grad-success': this.level === 'success',
                }
            },

            icon() {

                switch (this.level) {

                    case 'error':
                        return '#icon-x-circle';
                        break;

                    case 'info':
                        return '#icon-info';
                        break;

                    default:
                        return '#icon-check';
                }

            }
        }
    };
</script>