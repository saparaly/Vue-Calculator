<script>
export default {
    name: 'Calculator',
    props: {
        msg: String,
    },
    data(){
        return{
            output: '',
            prevVal: null,
            operationFire: false,
        }
    },
    methods: {
        clearField(){
            this.output = ''
        },
        setNegativeOrPositive(){
            this.output = this.output[0] === '-' ? this.output.slice(1) : `-${this.output}`
        },
        calculateMode(){
            this.output = parseFloat(this.output)/100
        },
        getNumber(n){
            if (this.operationFire){
                this.output = ''
                this.operationFire = false
            }
            this.output = `${this.output}${n}`
        },
        getDot(){
            if (this.output.indexOf('.') === -1){
                this.output = this.output+'.'
            }
        },
        processOutput(s){
            if (s == '+') {
                this.operation = (a, b) =>{
                    return  parseFloat(a) + parseFloat(b)
                }
            } else if (s == '/'){
                this.operation = (a, b) =>{
                    return  parseFloat(a) / parseFloat(b)
                }
            } else if (s == '-'){
                this.operation = (a, b) =>{
                    return  parseFloat(a) - parseFloat(b)
                }
            } else if (s == 'x'){
                this.operation = (a, b) =>{
                    return  parseFloat(a) * parseFloat(b)
                }
            }
            this.prevVal = this.output
            this.operationFire = true
        },
        updateOutput(){
            this.output = `${this.operation(this.prevVal, this.output)}`
            this.prevVal = null
        }
    }
}
</script>

<template>
    <div class="calculator">
        <h1>{{ msg }}</h1>

        <div class="table">
            <div class="row_result"> {{ output || 0 }}</div>
            <div class="row1">
                <div class="row" @click="clearField">C</div>
                <div class="row" @click="setNegativeOrPositive">+/-</div>
                <div class="row" @click="calculateMode">%</div>
                <div class="row" @click="processOutput('/')">/</div>
            </div>
            <div class="row1">
                <div class="row" @click="getNumber(7)">7</div>
                <div class="row" @click="getNumber(8)">8</div>
                <div class="row" @click="getNumber(9)">9</div>
                <div class="row" @click="processOutput('x')">x</div>
            </div>
            <div class="row1">
                <div class="row" @click="getNumber(4)">4</div>
                <div class="row" @click="getNumber(5)">5</div>
                <div class="row" @click="getNumber(6)">6</div>
                <div class="row" @click="processOutput('-')">-</div>
            </div>
            <div class="row1">
                <div class="row" @click="getNumber(1)">1</div>
                <div class="row" @click="getNumber(2)">2</div>
                <div class="row" @click="getNumber(3)">3</div>
                <div class="row" @click="processOutput('+')">+</div>
            </div>
            <div class="row1">
                <div class="row r22" @click="getNumber(0)">0</div>
                <div class="row r2"></div>
                <div class="row" @click="getDot">.</div>
                <div class="row" @click="updateOutput">=</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.table{
    width: fit-content;
    height: fit-content;
    border: 1px solid #333;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border-radius: 15px;
    overflow: hidden;
}

.row_result {
    width: 100%;
    height: 50px;
    background: #444;
    padding: 15px;
}
.row1 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.row {
    display: flex;
    align-items: center;
    justify-content: center;
    background: #333;
    width: 50px;
    height: 50px;
    border: 1px solid #444;
    cursor: pointer;
}
.row:last-child{
    background: orange;
}
.row.r2{
    border-left: none;
}
.row.r22{
    border-right: none;
}
</style>