<template>
<div class="twoDiv">
    <el-card>
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
            <el-row :gutter="10">
                <el-col :span="8">
                    <el-form-item>
                        <el-date-picker v-model="value2" type="daterange" :shortcuts="shortcuts" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期" align="right">
                        </el-date-picker>
                    </el-form-item>
                </el-col>
                <el-col :span="4" :pull="1">
                    <el-form-item>
                        <el-select v-model="value" placeholder="请选择">
                            <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                </el-col>
                <el-col :span="2" :pull="2">
                    <el-form-item>
                        <el-button type="primary">Search</el-button>
                    </el-form-item>
                </el-col>
            </el-row>
        </el-form>

        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
            <el-row>
                <el-col span="6">
                    <el-form-item>
                        <el-input class="txtTwo" />
                    </el-form-item>
                </el-col>
                <el-col span="2" :pull="1">
                    <el-form-item>
                        <el-button type="success">Search</el-button>
                    </el-form-item>
                </el-col>
            </el-row>
        </el-form>

        <el-table :data="tableData" style="width: 100%">
            <el-table-column label="编号" width="90">
                <template #default="scope">
                    <i class="el-icon-time"></i>
                    <span style="margin-left: 10px">{{ scope.row.no }}</span>
                </template>
            </el-table-column>
            <el-table-column prop="name" label="客户" width="100"></el-table-column>
            <el-table-column prop="number" label="合约号" width="100"></el-table-column>
            <el-table-column prop="departure" label="启运港" width="100">
            </el-table-column>
            <el-table-column prop="port" label="目的港" width="130">
            </el-table-column>
            <el-table-column prop="datatime" label="储运日期" width="100">
            </el-table-column>
            <el-table-column prop="wigth" label="箱型箱量" width="100">
            </el-table-column>
            <el-table-column prop="shop" label="供应商" width="100">
            </el-table-column>
            <el-table-column label="操作">
                <template #default="scope">
                    <el-button type="primary" @click="editForm">view</el-button>
                    <el-button type="danger" @click="changeUserInfo(scope.row.no)">delete</el-button>
                </template>
            </el-table-column>
        </el-table>

    </el-card>
</div>
</template>

<script>
export default {
    data() {
        return {
            ruleForm: {
                name: '',
                region: '',
                date1: '',
                date2: '',
                delivery: false,
                type: [],
                resource: '',
                desc: ''
            },
            rules: {
                name: [{
                        required: true,
                        message: '请输入活动名称',
                        trigger: 'blur'
                    },
                    {
                        min: 2,
                        max: 5,
                        message: '长度在 3 到 5 个字符',
                        trigger: 'blur'
                    }
                ],
                region: [{
                    required: true,
                    message: '请选择活动区域',
                    trigger: 'change'
                }],
                date1: [{
                    type: 'date',
                    required: true,
                    message: '请选择日期',
                    trigger: 'change'
                }],
                date2: [{
                    type: 'date',
                    required: true,
                    message: '请选择时间',
                    trigger: 'change'
                }],
                type: [{
                    type: 'array',
                    required: true,
                    message: '请至少选择一个活动性质',
                    trigger: 'change'
                }],
                resource: [{
                    required: true,
                    message: '请选择活动资源',
                    trigger: 'change'
                }],
                desc: [{
                    required: true,
                    message: '请填写活动形式',
                    trigger: 'blur'
                }]
            },
            shortcuts: [{
                text: '最近一周',
                value: (() => {
                    const end = new Date();
                    const start = new Date();
                    start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
                    return [start, end]
                })()
            }, {
                text: '最近一个月',
                value: (() => {
                    const end = new Date();
                    const start = new Date();
                    start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
                    return [start, end]
                })()
            }, {
                text: '最近三个月',
                value: (() => {
                    const end = new Date();
                    const start = new Date();
                    start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
                    return [start, end]
                })()
            }],
            value2: '',
            value1: '',
            tableData: [{
                    no: "1",
                    name: "友梦",
                    number: "12345",
                    departure: "SHANGHAI",
                    port: "HONG KONG",
                    datatime: "2020-10-30",
                    wigth: "10X20'GP",
                    shop: "COSCO",
                    shopETM: "CY-CY",
                    myETM: "CY-DOOR",
                },
                {
                    no: "2",
                    name: "YoomSoft",
                    number: "66666",
                    departure: "SHENZHEN",
                    port: "HONG KONG",
                    datatime: "2021-1-15",
                    wigth: "10X20'GP",
                    shop: "COSCO",
                    shopETM: "CY-CY",
                    myETM: "CY-DOOR",
                },
                {
                    no: "3",
                    name: "Yoom",
                    number: "888888",
                    departure: "QINGDAO",
                    port: "HONG KONG",
                    datatime: "2020-11-08",
                    wigth: "10X20'GP",
                    shop: "COSCO",
                    shopETM: "CY-CY",
                    myETM: "CY-DOOR",
                },
            ],
            input: "",
            value2: "",
            options: [{
                    value: "选项1",
                    label: "SHANGHAI",
                },
                {
                    value: "选项2",
                    label: "SHENZHEN",
                },
                {
                    value: "选项3",
                    label: "QINGDAO",
                },
            ],
            value: "",
        };
    },
    methods: {
        editForm() {
            this.$router.replace("/home/editbooking");
        },
        changeUserInfo(no){
            console.log(no);
        }
    },
};
</script>

<style>
.twoDiv .txtTwo {
    width: 400px;
}

#table {
    margin-left: -21px;
    margin-right: -839px;
    margin-top: 30px;
}

#button1 {
    margin-top: -41px;
    margin-left: 993px;
}

#button {
    margin-top: -31px;
    margin-left: 890px;
}

#input {
    margin-top: -58px;
    margin-left: 594px;
    margin-right: -370px;
}

#sel {
    margin-top: -70px;
    margin-left: 363px;
    margin-right: -135;
}

.twoDiv .el-form-item {
    height: 50px;
}

.twoDiv .gray {
    color: gray;
}

.twoDiv .sel {
    margin-top: 8px;
    margin-left: 0px;
    height: 38px;
}

.twoDiv .el-select {
    margin-top: -20px;
    height: 38px;
}
</style>
