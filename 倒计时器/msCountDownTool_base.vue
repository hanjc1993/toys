<template>
    <div id="draw">
        <div class="items">
            <div class="item">{{a}}</div>
            <div class="item">{{b}}</div>
            <div class="item">:</div>
            <div class="item">{{c}}</div>
            <div class="item">{{d}}</div>
        </div>
        <button @click="start">开始倒计时</button>
    </div>

</template>
<script>
    export default {
        data() {
            return {
                a: 3,
                b: 0,
                c: 0,
                d: 0,
                canStart: true
            }
        },
        methods: {
            start() {
                if (this.canStart) {
                    this.canStart = false;
                    // 核心，仅仅支持10s的整数倍起步
                    setTimeout(() => {
                        let count = this.a * 10 * 10 * 5 - 1;
                        // 4位定时器
                        let ms20 = setInterval(() => { // 20毫秒，本来是10ms，反正也看不清
                                if (count === 0) return clearInterval(ms20);
                                this.d = this.d === 0 ? 8 : this.d - 2;
                                count--;
                            }, 20),
                            ms100 = setInterval(() => { // 100毫秒
                                if (count === 0) return clearInterval(ms100);
                                this.c = this.c === 0 ? 9 : this.c - 1;
                            }, 100),
                            s1 = setInterval(() => { // 1秒
                                if (count === 0) return clearInterval(s1);
                                this.b = this.b === 0 ? 9 : this.b - 1;
                            }, 1000),
                            s10 = setInterval(() => { // 10秒
                                if (count !== 0) return this.a--;
                                clearInterval(s10);
                                this.canStart = true;
                            }, 10000);
                        // 第一次手动赋值
                        this.a--;
                        this.b = this.c = 9;
                        this.d = 8;
                    }, 18); // 20ms延迟，给2ms执行，首次偏差几ms无所谓
                }
            }
        }
    }
</script>

<style scoped lang="scss">
    #draw {
        font-size: 50px;
    }
    .item {
        width: 50px;
        text-align: center;
        float: left;
    }
</style>
