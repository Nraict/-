<template>
  <div>
   <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
  <el-form-item label="活动名称" prop="name">
    <el-input v-model="ruleForm.name"></el-input>
  </el-form-item>
  <el-form-item label="活动区域" prop="region">
    <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>
<el-form-item label="手机" prop="moblie">
    <el-input v-model="ruleForm.moblie"></el-input>
  </el-form-item>
  <el-form-item label="邮箱" prop="email">
    <el-input v-model="ruleForm.email"></el-input>
  </el-form-item>
  <el-form-item label="英文" prop="English">
    <el-input v-model="ruleForm.English"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
    <el-button @click="resetForm('ruleForm')">重置</el-button>
  </el-form-item>
</el-form>
  </div>
</template>

<script>
export default {
    data() {
        return {
            ruleForm: {
                name: '',
                moblie: '',
                region: '',
                email: '',
                English: '',
            },
            rules: {
                // 姓名验证
                name: [
                    { required: true, message: '请输入活动名称', trigger: 'blur' },
                    { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
                ],
                // 手机验证
                moblie: [
                    { required: true, message: '请输入手机', trigger: 'blur' },
                    {
                        validator: function(rule, value, callback) {
                            var MobileRegex = /^1[0-9]{10}$/;
                            if (!MobileRegex.test(value)) {
                                callback(new Error('手机号码格式不正确！'))
                            } else {
                                callback();
                            }
                        },
                        trigger: 'blur'
                    }
                ],
                // 邮箱
                email: [
                    { required: true, message: '请输入邮箱', trigger: 'blur' },
                    {
                        validator: function(rule, value, callback) {
                            var emailRegex = /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/;
                            if (!emailRegex.test(value)) {
                                callback(new Error('邮箱格式不正确！'))
                            } else {
                                callback();
                            }
                        },
                        trigger: 'blur'
                    }
                ],
                region: [
                    { required: true, message: '请选择活动区域', trigger: 'change' }
                ],
                // 英文
                English: [
                    { required: true, message: '请输入', trigger: 'blur' },
                    {
                        validator: function(rule, value, callback) {
                            var emailRegex = /^[a-z\#]*$/;
                            if (!emailRegex.test(value)) {
                                callback(new Error('只支持小写英文和拼音'))
                            } else {
                                callback();
                            }
                        },
                        trigger: 'blur'
                    }
                ]

            }
        };
    },
    methods: {
        submitForm(formName) {
            this.$refs[formName].validate((valid) => {
                if (valid) {
                    alert('submit!');
                } else {
                    console.log('error submit!!');
                    return false;
                }
            });
        },
        resetForm(formName) {
            this.$refs[formName].resetFields();
        }
    }
}
</script>