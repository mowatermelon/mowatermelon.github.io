---
title: 框架学习之element表单验证
category: 框架学习
tags:
  - element
  - form
  - base
  - 框架学习
date: 2017-11-12 00:00:00
---

> 感觉element的表单组件验证还挺有意思的

# 第一步 添加el-form标签

`<el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm"></el-form>`

<!--more-->

- model 对应绑定的是下面input组的的顶级数据对象，是以自定义属性的形式进行添加
- status-icon这个是状态的icon，写了这个属性之后，input组做失焦验证的时候，input框最右侧出现成功或者失败的icon状态提示。
- rules对应的是下面input组做失焦验证的，主要规则数据，是以自定义属性的形式进行添加
- ref是绑定当前作用域中的ref对应的表单对象，举例

```javascript
     //可以在一个失焦验证中唤起另一个的失焦验证
    //重点在这一句  _this.$refs.ruleForm.validateField('userRPwd');
    const validatePass = (rule, value, callback) => {
      if (!value) {
        callback(new Error('请输入密码'));
      } else {
        if (_this.gores && _this.ruleForm.userRPwd !== '') {
          _this.$refs.ruleForm.validateField('userRPwd');
        }else if (!_this.gores){
          const UPassd = _this.$store.state.userPassword||_this.aesEncrypt('123', 'UPassd');
          if (value !== _this.aesDecrypt(UPassd, 'UPassd')) {
            callback(new Error('请输入正确的密码'));
          }
        }
        callback();
      }
    };

     //可以在清除按钮事件中写这样的逻辑
     goReg (formName) {
       this.$refs[formName].resetFields();
       this.gores = true;
     }

     //可以在按钮提交事件中写这样的事件验证
    checkReg (formName) {
      let _this = this;
      this.$refs[formName].validate((valid) => {
        if (valid) {
          _this.showSuc('登录成功');
          _this.$store.commit('setUName',_this.aesEncrypt(_this.ruleForm.userName, 'UName'));
          _this.$store.commit('setUPassd',_this.aesEncrypt(_this.ruleForm.userPwd, 'UPassd'));
          _this.$store.commit('checkLogin',false);
        } else {
          _this.showErr('请确认所有输入项都填写完成，或者两次密码输入是否匹配');
        }
      });
    }


```

---

# 第二步 写规则rule和数据model

```javascript
  data () {
    let _this = this;
    const validateName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入用户名'));
      } else {

        const UName = _this.$store.state.userName||_this.aesEncrypt('123', 'UName');

        if (!_this.gores && value !== _this.aesDecrypt(UName, 'UName')) {
          callback(new Error('请输入正确注册的用户名'));
        }
        callback();
      }
    };

    const validatePass = (rule, value, callback) => {
      if (!value) {
        callback(new Error('请输入密码'));
      } else {
        if (_this.gores && _this.ruleForm.userRPwd !== '') {
          _this.$refs.ruleForm.validateField('userRPwd');
        }else if (!_this.gores){
          const UPassd = _this.$store.state.userPassword||_this.aesEncrypt('123', 'UPassd');
          if (value !== _this.aesDecrypt(UPassd, 'UPassd')) {
            callback(new Error('请输入正确的密码'));
          }
        }
        callback();
      }
    };

    const validatePass2 = (rule, value, callback) => {
      if(_this.gores){
        if (!value) {
          callback(new Error('请输入确认输入密码'));
        } else if (value !== _this.ruleForm.userPwd) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      }else{
        callback();
      }

    };
    return {
      ruleForm:{
        userName: '',
        userPwd: '',
        userRPwd: ''
      },
      gores: false,
      rules: {
        userName: [
          { validator: validateName, trigger: 'blur' }
        ],
        userPwd: [
          { validator: validatePass, trigger: 'blur' }
        ],
        userRPwd: [
          { validator: validatePass2, trigger: 'blur' }
        ]
      }
    };
  },
```

---

# 第三步 与页面元素进行绑定

请注意每个`el-form-item`中的`prop`属性，这个是和检测规则进行紧密相连的，是对应`rules`的属性，请注意一定要一一对应呀。

```html
      <el-row type="flex" justify="center">
        <el-col :xs="24" :sm="8" class="loginBox">

          <div class="text-center">
            <i class="el-icon-menu loginIcon" alt="用户登录" v-if="!gores"></i>
            <i class="el-icon-date loginIcon" alt="用户注册" v-if="gores"></i>
          </div>
          <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm">

            <el-col :span="24" class="n-p-l-r">
              <el-form-item class="h1" prop="userName">
                <el-input placeholder="请输入用户名" v-model="ruleForm.userName">
                  <template slot="prepend"><i class="el-icon-edit"></i></template>
                </el-input>
              </el-form-item>
            </el-col>

            <el-col :span="24" class="n-p-l-r">
              <el-form-item class="h1" prop="userPwd">
                <el-input placeholder="请输入密码" v-model="ruleForm.userPwd" type="password">
                  <template slot="prepend"><i class="el-icon-edit-outline"></i></template>
                </el-input>
              </el-form-item>
            </el-col>

            <el-col :span="24" class="n-p-l-r" v-show="gores">
              <el-form-item class="h1" prop="userRPwd">
                <el-input placeholder="请再次确认输入密码" v-model="ruleForm.userRPwd" type="password">
                  <template slot="prepend"><i class="el-icon-edit-outline"></i></template>
                </el-input>
              </el-form-item>
            </el-col>

            <el-col :span="24" v-if="!gores" class="n-p-l-r">
              <el-form-item>
                <el-button type="primary" plain @click="checkLogin('ruleForm')" class="long">登陆账户</el-button>
              </el-form-item>
            </el-col>

            <el-col :xs="24" :sm="10" :offset="14" v-if="!gores" class="n-p-l-r">
              <el-form-item>
                <el-button plain @click="goReg('ruleForm')" class="long">用户注册</el-button>
              </el-form-item>
            </el-col>

            <el-col :span="24" v-if="gores" class="n-p-l-r">
              <el-form-item>
                <el-button type="primary" plain @click="checkReg('ruleForm')" class="long">注册账户</el-button>
              </el-form-item>
            </el-col>

            <el-col :xs="24" :sm="10" :offset="14" v-if="gores" class="n-p-l-r">
              <el-form-item  v-if="gores">
                <el-button plain @click="goLogin('ruleForm')" class="long">已有帐号去登陆</el-button>
              </el-form-item>
            </el-col>

          </el-form>
        </el-col>

      </el-row>
```

---

# 第四步 效果预览

## 登录效果预览

![图片](https://dn-coding-net-production-pp.qbox.me/f9d6b0a2-5fb8-49a3-afc8-2c7a4864b60e.png)

## 注册效果预览

![图片](https://dn-coding-net-production-pp.qbox.me/887e3585-a811-4efa-b7b9-a13590761157.png)

# 放上完整项目代码

```html
<template>
  <transition name="fade">
    <div>
      <el-row type="flex" justify="center">
        <el-col :xs="24" :sm="8" class="loginBox">

          <div class="text-center">
            <i class="el-icon-menu loginIcon" alt="用户登录" v-if="!gores"></i>
            <i class="el-icon-date loginIcon" alt="用户注册" v-if="gores"></i>
          </div>
          <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm">

            <el-col :span="24" class="n-p-l-r">
              <el-form-item class="h1" prop="userName">
                <el-input placeholder="请输入用户名" v-model="ruleForm.userName">
                  <template slot="prepend"><i class="el-icon-edit"></i></template>
                </el-input>
              </el-form-item>
            </el-col>

            <el-col :span="24" class="n-p-l-r">
              <el-form-item class="h1" prop="userPwd">
                <el-input placeholder="请输入密码" v-model="ruleForm.userPwd" type="password">
                  <template slot="prepend"><i class="el-icon-edit-outline"></i></template>
                </el-input>
              </el-form-item>
            </el-col>

            <el-col :span="24" class="n-p-l-r" v-show="gores">
              <el-form-item class="h1" prop="userRPwd">
                <el-input placeholder="请再次确认输入密码" v-model="ruleForm.userRPwd" type="password">
                  <template slot="prepend"><i class="el-icon-edit-outline"></i></template>
                </el-input>
              </el-form-item>
            </el-col>

            <el-col :span="24" v-if="!gores" class="n-p-l-r">
              <el-form-item>
                <el-button type="primary" plain @click="checkLogin('ruleForm')" class="long">登陆账户</el-button>
              </el-form-item>
            </el-col>

            <el-col :xs="24" :sm="10" :offset="14" v-if="!gores" class="n-p-l-r">
              <el-form-item>
                <el-button plain @click="goReg('ruleForm')" class="long">用户注册</el-button>
              </el-form-item>
            </el-col>

            <el-col :span="24" v-if="gores" class="n-p-l-r">
              <el-form-item>
                <el-button type="primary" plain @click="checkReg('ruleForm')" class="long">注册账户</el-button>
              </el-form-item>
            </el-col>

            <el-col :xs="24" :sm="10" :offset="14" v-if="gores" class="n-p-l-r">
              <el-form-item  v-if="gores">
                <el-button plain @click="goLogin('ruleForm')" class="long">已有帐号去登陆</el-button>
              </el-form-item>
            </el-col>

          </el-form>
        </el-col>

      </el-row>
    </div>

  </transition>
</template>

<script>
import crypto from 'crypto';

export default {
  name: 'Login',
  data () {
    let _this = this;
    const validateName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入用户名'));
      } else {

        const UName = _this.$store.state.userName||_this.aesEncrypt('123', 'UName');

        if (!_this.gores && value !== _this.aesDecrypt(UName, 'UName')) {
          callback(new Error('请输入正确注册的用户名'));
        }
        callback();
      }
    };

    const validatePass = (rule, value, callback) => {
      if (!value) {
        callback(new Error('请输入密码'));
      } else {
        if (_this.gores && _this.ruleForm.userRPwd !== '') {
          _this.$refs.ruleForm.validateField('userRPwd');
        }else if (!_this.gores){
          const UPassd = _this.$store.state.userPassword||_this.aesEncrypt('123', 'UPassd');
          if (value !== _this.aesDecrypt(UPassd, 'UPassd')) {
            callback(new Error('请输入正确的密码'));
          }
        }
        callback();
      }
    };

    const validatePass2 = (rule, value, callback) => {
      if(_this.gores){
        if (!value) {
          callback(new Error('请输入确认输入密码'));
        } else if (value !== _this.ruleForm.userPwd) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      }else{
        callback();
      }

    };
    return {
      ruleForm:{
        userName: '',
        userPwd: '',
        userRPwd: ''
      },
      gores: false,
      rules: {
        userName: [
          { validator: validateName, trigger: 'blur' }
        ],
        userPwd: [
          { validator: validatePass, trigger: 'blur' }
        ],
        userRPwd: [
          { validator: validatePass2, trigger: 'blur' }
        ]
      }
    };
  },
  methods: {
    checkLogin (formName) {
      let _this = this;
      this.$refs[formName].validate((valid) => {
        if (valid) {
          _this.showSuc('登录成功');
          _this.$store.commit('setUName',_this.aesEncrypt(_this.ruleForm.userName, 'UName'));
          _this.$store.commit('setUPassd',_this.aesEncrypt(_this.ruleForm.userPwd, 'UPassd'));
          _this.$store.commit('checkLogin',false);
        } else {
          _this.showErr('用户名或者帐号输入错误请确认');
        }
      });

    },
    checkReg (formName) {
      let _this = this;
      this.$refs[formName].validate((valid) => {
        if (valid) {
          _this.showSuc('登录成功');
          _this.$store.commit('setUName',_this.aesEncrypt(_this.ruleForm.userName, 'UName'));
          _this.$store.commit('setUPassd',_this.aesEncrypt(_this.ruleForm.userPwd, 'UPassd'));
          _this.$store.commit('checkLogin',false);
        } else {
          _this.showErr('请确认所有输入项都填写完成，或者两次密码输入是否匹配');
        }
      });

    },
    goReg (formName) {
       this.$refs[formName].resetFields();
       this.gores = true;
    },
    goLogin (formName) {
      this.$refs[formName].resetFields();
      this.gores = false;
    },
    aesEncrypt(data, key) {
        const cipher = crypto.createCipher('aes192', key);
        var crypted = cipher.update(data, 'utf8', 'hex');
        crypted += cipher.final('hex');
        return crypted;
    },
    aesDecrypt(encrypted, key) {
        const decipher = crypto.createDecipher('aes192', key);
        var decrypted = decipher.update(encrypted, 'hex', 'utf8');
        decrypted += decipher.final('utf8');
        return decrypted;
    },
    showSuc(msg){
      this.$message({
        showClose: true,
        message: msg,
        type: 'success',
        duration:500
      });
    },
    showErr(msg){
      this.$message({
        showClose: true,
        message: msg,
        type: 'error'
      });
    }

  }
};
</script>

<style lang="scss" scoped>
$normal_shadom:#ddd;//页面默认阴影颜色
$normal_active:#5bc0de;//页面默认主色调
$normal_color:#fff; //页面默认未激活色


.loginBox{
  box-shadow: 0 0 21px 2px $normal_shadom;
  margin-top:8%;
  padding: 3%;
  .loginIcon{
    background: $normal_active;
    color:$normal_color;
    border-radius: 100%;
    padding: 25px;
    font-size: 40px;
    margin-bottom: 30px;
  }
}

@media (max-width:768px){
  .loginBox{
    box-shadow: 0 0 21px 2px $normal_color;
  }
}
</style>

```

---
