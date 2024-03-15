<template>
    <div class="progress-ring-container">
        <svg viewBox="0 0 100 100" class="progress-ring">
            <circle
                    class="static-ring-circle"
                    :stroke="staticColor"
                    :stroke-width="strokeWidth"
                    fill="transparent"
                    cx="50"
                    cy="50"
                    :r="radius"
            />
            <circle
                    class="progress-ring-circle"
                    :stroke-dasharray="circumference"
                    :stroke-dashoffset="circumference * (1 - checkInputValue)"
                    stroke-linecap="round"
                    :stroke="color"
                    :stroke-width="strokeWidth"
                    fill="transparent"
                    cx="50"
                    cy="50"
                    :r="radius"
                    filter="drop-shadow(0 0 3px rgb(235 228 36))"
            />
        </svg>
        <div class="progress-value">{{ progressValue }}%</div>
    </div>
</template>

<script>
    export default {
        name: "ProgressBar",
        props: {
            value: {
                type: Number,
                default: 0.5,
            },
            radius: {
                type: Number,
                default: 40,
            },
            strokeWidth: {
                type: Number,
                default: 10,
            },
            color: {
                type: String,
                default: 'rgb(235 228 36)',
            },
            staticColor: {
                type: String,
                default: 'rgb(79 68 102)',
            },
        },
        data() {
            return {};
        },
        computed: {
            circumference() {
                return 2 * Math.PI * this.radius;
            },
            progressValue() {
                return Math.round(this.checkInputValue * 100);
            },
            checkInputValue() {
                if (this.value > 1 || this.value < 0) {
                    return 0
                }
                return this.value
            }
        },
    };
</script>

<style scoped>
    .progress-ring-container {
        width: 200px;
        position: relative;
    }

    .progress-ring {
        width: 200px;
        height: 200px;
        background-color: rgb(36 21 64);
    }

    .static-ring-circle,
    .progress-ring-circle {
        transition: stroke-dashoffset 0.35s;
        transform: rotate(-90deg);
        transform-origin: 50% 50%;
    }

    .progress-value {
        font-size: 30px;
        color: rgb(235 228 36);
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>
