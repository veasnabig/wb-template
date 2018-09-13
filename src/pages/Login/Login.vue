<template>
<div class="bg">
    <div class="top-bar-wrapper">
        <div class="top-bar-head">
            <p class="date">
                <span class="label">ថ្ងៃ</span><span class="value">{{day}}</span> 
                <span class="label">ទី</span><span class="value">{{daysOfWeek}} </span>
                <span class="label">ខែ</span><span class="value">{{month}}</span>
                <span class="label">ឆ្នាំ</span><span class="value separator">{{year}}</span>
                <span class="label">ម៉ោង</span>
                <span class="value">{{hour}}ៈ</span>
                <span class="value">{{minutes}}ៈ</span>
                <span class="value">{{second}}</span>
                <span class="value">{{timeName}}</span>
            </p>
        </div>
    </div>
    <div class="left-curved"></div>
    <div class="right-curved"></div>
</div>
</template>

<script>
import dateformat from '../../lib/dateformat.js';
// var now = new Date();
// var date = dateformat(now, "ថ្ងៃ dddd ទី dd ខែ mmmm ឆ្នាំ yyyy, hh:MM TT");
export default {
    data: () => ({
        start: "",
        interval: "",
        hour: "",
        year:"",
        month: "",
        day: "",
        daysOfWeek: "",
        minutes: "",
        second: "",
        timeName: ""
    }),
    mounted() {
        this.interval = setInterval(() => {
            this.calcTime();
        }, 1000);
        this.date();
    },
    methods: {
        convertToUnicode(value) {
            let arr = value.toString().split("");
            let rs = "";
            for (let i = 0; i < arr.length; i++) {
                switch (+arr[i]) {
                    case 0:
                        rs += `\u17e0`
                        break;
                    case 1:
                        rs += `\u17e1`
                        break;
                    case 2:
                        rs += `\u17e2`
                        break;
                    case 3:
                        rs += `\u17e3`
                        break;
                    case 4:
                        rs += `\u17e4`
                        break;
                    case 5:
                        rs += `\u17e5`
                        break;
                    case 6:
                        rs += `\u17e6`
                        break;
                    case 7:
                        rs += `\u17e7`
                        break;
                    case 8:
                        rs += `\u17e8`
                        break;
                    case 9:
                        rs += `\u17e9`
                        break;
                }
            }
            return rs;

        },
        calcTime() {
            let now = new Date();
            this.hour = now.getHours();
            this.minutes = now.getMinutes();
            this.second = now.getSeconds();
            this.timeName = dateformat(now, "TT");
            if (this.second < 10) this.second = "0" + this.second;
            if (this.minutes < 10) this.minutes = "0" + this.minutes;
            if (this.hour < 10) this.hour = "0" + this.hour;
            this.second = this.convertToUnicode(this.second);
            this.minutes = this.convertToUnicode(this.minutes);
            this.hour = this.convertToUnicode(this.hour);
        },
        date() {
            let now = new Date();
            this.year = now.getFullYear();
            this.month = this.months(now.getMonth());
            this.daysOfWeek = this.daysOfWeekKh(now.getDay());
            this.day = now.getDate();
            if (this.day < 10) this.day = "0" + this.day;
            this.day = this.convertToUnicode(this.day);
            this.year= this.convertToUnicode(this.year);
        },
        months(month) {
            let rs = "";
            switch (month) {
                case 0:
                    rs = "មករា"
                    break;
                case 1:
                    rs = "កុម្ភៈ"
                    break;
                case 2:
                    rs = "មីនា"
                    break;
                case 3:
                    rs = "មេសា"
                    break;
                case 4:
                    rs = "ឧសភា"
                    break;
                case 5:
                    rs = "មិថុនា"
                    break;
                case 6:
                    rs = "កក្កដា"
                    break;
                case 7:
                    rs = "សីហា"
                    break;
                case 8:
                    rs = "កញ្ញា"
                    break;
                case 9:
                    rs = "តុលា"
                    break;
                case 10:
                    rs = "វិច្ឆកា"
                    break;
                case 11:
                    rs = "ធ្នូ"
                    break;
            }
            return rs;
        },
        daysOfWeekKh(day) {
            let rs = "";
            switch (day) {
                case 0:
                    rs = "អាទិត្យ"
                    break;
                case 1:
                    rs = "ច័ន្ទ"
                    break;
                case 2:
                    rs = "អង្គារ"
                    break;
                case 3:
                    rs = "ពុធ"
                    break;
                case 4:
                    rs = "ព្រហស្បតិ៍"
                    break;
                case 5:
                    rs = "សុក្រ"
                    break;
                case 6:
                    rs = "សៅរ៍"
                    break;
            }
            return rs;
        }
    }

};
</script>

<style lang="scss" scoped>
.bg {
    height: 100vh;
    width: 100%;
    background: linear-gradient(0deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.3)), url("../../assets/bg-blur.jpg") no-repeat;
    background-size: cover;
    background-position: 50%;
    position: absolute;
    animation: login-bg .5s;
}

.top-bar-wrapper {
    height: 20px;
    width: 100%;
    background: rgba(0, 0, 0, .2);
    position: absolute;
    top: 0;
    .top-bar-head {
        height: 20px;
        width: 40%;
        background: rgba(0, 0, 0, .2);
        position: absolute;
        top: 20px;
        left: 50%;
        transform: translate(-50%);
        border-bottom-left-radius: 50px;
        border-bottom-right-radius: 50px;
    }
}

.left-curved {
    height: 100%;
    width: 35px;
    float: left;
    z-index: 10;
    position: absolute;
    left: 0;
    /* Permalink - use to edit and share this gradient: http://colorzilla.com/gradient-editor/#000000+0,ffffff+100&0.6+0,0+60 */
    background: -moz-linear-gradient( left, rgba(255, 255, 255, 0.3) 0%, rgba(153, 153, 153, 0) 60%, rgba(255, 255, 255, 0) 100%);
    /* FF3.6-15 */
    background: -webkit-linear-gradient( left, rgba(255, 255, 255, 0.3) 0%, rgba(153, 153, 153, 0) 60%, rgba(255, 255, 255, 0) 100%);
    /* Chrome10-25,Safari5.1-6 */
    background: linear-gradient( to right, rgba(255, 255, 255, 0.3) 0%, rgba(153, 153, 153, 0) 60%, rgba(255, 255, 255, 0) 100%);
    /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#99000000', endColorstr='#00ffffff', GradientType=1);
    /* IE6-9 */
}

.right-curved {
    height: 100%;
    width: 35px;
    float: right;
    z-index: 999px;
    position: absolute;
    right: 0;
    /* Permalink - use to edit and share this gradient: http://colorzilla.com/gradient-editor/#ffffff+2,000000+100&0+40,0.6+100 */
    background: -moz-linear-gradient( left, rgba(255, 255, 255, 0) 2%, rgba(65, 65, 65, 0) 40%, rgba(255, 255, 255, 0.3) 100%);
    /* FF3.6-15 */
    background: -webkit-linear-gradient( left, rgba(255, 255, 255, 0) 2%, rgba(156, 156, 156, 0) 40%, rgba(255, 255, 255, 0.3) 100%);
    /* Chrome10-25,Safari5.1-6 */
    background: linear-gradient( to right, rgba(255, 255, 255, 0) 2%, rgba(44, 44, 44, 0) 40%, rgba(255, 255, 255, 0.3) 100%);
    /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#00ffffff', endColorstr='#99000000', GradientType=1);
    /* IE6-9 */
}

.date {
    color: white;
    position: absolute;
    width: 100%;
    top: -15px;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: 'NiDATaprom',Arial, Helvetica, sans-serif;
    // font-size: 18px;
    .label{
        color: rgba(255, 255, 255,.3);
        font-size: 14px;
        margin-right: 2px;
    }
    .value{
        color:white;
        font-size: 18px;
    }
    .separator{
        padding-right:5px;
        margin-right:5px;
        border-right:white 2px solid;
    }
}

// keyframe
@keyframes login-bg {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
</style>
