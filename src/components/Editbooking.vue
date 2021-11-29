<template>
<div class="threeDiv">
    <el-card>
        <el-form label-position="top" label-width="100px" :model="ruleForm" :rules="rules" ref="ruleForm">
            <el-row :gutter="30">
                <el-col :span="6">
                    <el-form-item label="启动港">
                        <el-select v-model="value" clearable placeholder="请选择">
                            <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                </el-col>
                <el-col :span="6">
                    <el-form-item label="卸货港">
                        <el-select v-model="value" clearable placeholder="请选择">
                            <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                </el-col>

                <el-col :span="6">
                    <el-form-item label="出运日期">
                        <el-date-picker v-model="value1" type="date" placeholder="选择日期">
                        </el-date-picker>
                    </el-form-item>
                </el-col>

                <el-col :span="6">
                    <el-form-item label="供货商条款">
                        <el-select v-model="value" clearable placeholder="请选择">
                            <el-option v-for="item in options1" :key="item.value" :label="item.label" :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                </el-col>
            </el-row>

            <el-row :gutter="30">
                <el-col :span="6">
                    <el-form-item label="船名">
                        <el-input placeholder="请输入内容" clearable v-model="input"></el-input>
                    </el-form-item>
                </el-col>
                <el-col :span="6">
                    <el-form-item label="航次">
                        <el-input placeholder="请输入内容" clearable></el-input>
                    </el-form-item>
                </el-col>
                <el-col :span="6">
                    <el-form-item label="合约号">
                        <el-input placeholder="请输入内容" clearable style="width: 278px"></el-input>
                    </el-form-item>
                </el-col>
                <el-col :span="6">
                    <el-form-item label="我司条款">
                        <el-select v-model="value" clearable placeholder="请选择">
                            <el-option v-for="item in options2" :key="item.value" :label="item.label" :value="item.value"></el-option>
                        </el-select>
                    </el-form-item>
                </el-col>
            </el-row>
            <el-row>
                <el-col :span="6">
                    <el-form-item label="供应商">
                          <el-select v-model="value" clearable placeholder="请选择">
                                      <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
                             </el-select>
                    </el-form-item>
                </el-col>
            </el-row>

            <fieldset class="fds" :model="dynamicValidateForm" ref="dynamicValidateForm">
                <legend align="left">集装箱</legend>

                <el-row class="rr">
                    <el-col :span="4">
                        <el-form-item label="箱型">
                            <el-input-number v-model="num_0" @change="handleChange" :min="1"></el-input-number>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4" :pull="1">
                        <el-form-item class="selMe">
                            <el-select class="me" clearable placeholder="请选择" v-model="gp0">
                                          <el-option v-for="item in gps" :key="item.value" :label="item.label" :value="item.value"></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col class="inKg" :span="4" :pull="1">
                        <el-form-item label="重量KG(仅货物)">
                            <el-input placeholder="请输入内容" clearable v-model="w1"></el-input>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4">
                        <el-form-item label="操作">
                            <el-button type="primary" @click="add()">新增</el-button>
                            <el-button type="danger" @click.prevent="removeDomain()">删除</el-button>
                        </el-form-item>
                    </el-col>
                </el-row>
                <el-row v-if="showNum>=2" class="rr">
                    <el-col :span="4">
                        <el-form-item label="箱型">
                            <el-input-number v-model="num_1" @change="handleChange" :min="1"></el-input-number>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4" :pull="1">
                        <el-form-item class="selMe">
                            <el-select class="me" clearable placeholder="请选择" v-model="gp1">
                                          <el-option v-for="item in gps" :key="item.value" :label="item.label" :value="item.value"></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col class="inKg" :span="4" :pull="1">
                        <el-form-item label="重量KG(仅货物)">
                            <el-input placeholder="请输入内容" clearable v-model="w2"></el-input>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4">
                        <el-form-item label="操作">
                            <el-button type="primary" @click="add()">新增</el-button>
                            <el-button type="danger" @click.prevent="removeDomain()">删除</el-button>
                        </el-form-item>
                    </el-col>
                </el-row>
                <el-row v-if="showNum>=3" class="rr">
                    <el-col :span="4">
                        <el-form-item label="箱型">
                            <el-input-number v-model="num_2" @change="handleChange" :min="1"></el-input-number>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4" :pull="1">
                        <el-form-item class="selMe" :pull="1">
                            <el-select clearable placeholder="请选择" v-model="gp2">
                                          <el-option v-for="item in gps" :key="item.value" :label="item.label" :value="item.value"></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col class="inKg" :span="4" :pull="1">
                        <el-form-item label="重量KG(仅货物)">
                            <el-input placeholder="请输入内容" clearable v-model="w3"></el-input>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4">
                        <el-form-item label="操作">
                            <div class="btn">
                                <el-button type="primary" @click="add()">新增</el-button>
                                <el-button type="danger" @click.prevent="removeDomain()">删除</el-button>
                            </div>
                        </el-form-item>
                    </el-col>
                </el-row>

            </fieldset>

            <el-row :gutter="30">
                <el-col :span="8">
                    <el-form-item label="收货人">
                        <el-input type="textarea" :rows="4" placeholder="请输入内容" v-model="textarea">
                        </el-input>
                    </el-form-item>
                </el-col>
                <el-col :span="8">
                    <el-form-item label="发货人">
                        <el-input type="textarea" :rows="4" placeholder="请输入内容" v-model="textarea">
                        </el-input>
                    </el-form-item>
                </el-col>
                <el-col :span="8">
                    <el-form-item label="通知人">
                        <el-input type="textarea" :rows="4" placeholder="请输入内容" v-model="textarea">
                        </el-input>
                    </el-form-item>
                </el-col>
            </el-row>
        </el-form>
    </el-card>
</div>
</template>

<script>
export default {
    data() {
        return {
            showNum: 1,
            dynamicValidateForm: {
                domains: [{
                    value: ''
                }],
                // num:'1',
                // gp:'20GP',
                // input:'',
            },
            input: '',
            w1: "",
            w2: "",
            w3: "",
            gp0: "20GP",
            gp1: "30GP",
            gp2: "40GP",
            num_0: 1,
            num_1: 1,
            num_2: 1,
            ruleForm: {},
            textarea: "",
            addDialogVisible: false,
            input: "",
            value1: "",
            value: new Date(),
            gps: [{
                    value: "20",
                    label: "20GP",
                },
                {
                    value: "30",
                    label: "30GP",
                },
                {
                    value: "40",
                    label: "40GP",
                },
            ],
            options2: [{
                    value: "选项1",
                    label: "CY-DOOR",
                },
                {
                    value: "选项2",
                    label: "CY",
                },
            ],
            options1: [{
                    value: "选项1",
                    label: "CY-CY",
                },
                {
                    value: "选项2",
                    label: "CY",
                },
            ],
            options: [{
                    value: "选项1",
                    label: "SHANGHAI",
                },
                {
                    value: "选项2",
                    label: "QINGDAO",
                },
                {
                    value: "选项3",
                    label: "SHENZHEN",
                },
            ],
            value: "",

            rules: {
                name: [{
                    required: true,
                    message: "请输入...",
                    trigger: "blur",
                }, ],
                gp: [{
                    required: true,
                    message: "请输入...",
                    trigger: "blur",
                }, ],
            },

        };
    },
    methods: {
        handleChange(value) {
            // console.log(value);
        },
        removeDomain() {
            if (this.showNum >= 3) {
                this.showNum = 3
            }
            if (this.showNum <= 1) {
                this.showNum = 1
            }
            this.showNum--
        },
        add() {
            if (this.showNum < 1) {
                this.showNum = 1
            }
            this.showNum++
        }
    },
};
</script>

<style>
.fds .selMe {
    padding-top: 50px;
}

.fds .inKg {
    margin-right: 30px;
}

.threeDiv {
    font-weight: bold;
}

.threeDiv .el-row {
    height: 100px;
}

.threeDiv .el-card {
    padding-bottom: 50px;
}

.threeDiv .fds {
    border: 1px solid rgb(206, 200, 200);
}
.threeDiv .btn{
    width: 185px;
}
</style>
