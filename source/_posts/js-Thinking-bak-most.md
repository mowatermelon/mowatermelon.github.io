---
title: 西瓜有话说之js学习整理常用篇
category: js_thinking
tags:
- bak
- watermelon
- js_thinking
date: 2017-10-24 00:00:00
---
# 1 array

数组常用验证

<!-- more -->

```javascript

//给数组去重
Array.prototype.unique = function () {
  this.sort(); //先排序
  var res = [this[0]];
  for (var i = 1; i < this.length; i++) {
    if (this[i] !== res[res.length - 1]) {
      res.push(this[i]);
    }
  }
  return res;
}

//计算数组之和
function sum(list) {
  return eval(list.join("+"));
}
//验证数组中是否包含重复数据
function checkArrayUnique(arr) {
    var isUnique = false;
    var initArrL = arr.length;
    if (arr.length > 1) {
        arr = arr.unique();
        if (arr.length != initArrL) {
            isUnique = true;
        }
    }

    return isUnique;
}


```

# 2 form

表单常用验证

```javascript
//验证数组中数据是否为空
function checkArrayNull(str) {
    var isNull= false;
    var emptyReg = /^\s*$/g; //验证是否为空
    isNull = emptyReg.test(str) || str == key_bjwb;
    return isNull;
}

//验证数组中数据是否为正整数
function checkArrayInteger(str) {
    var intReg = /[1-9]\d*/g;
    return intReg.test(str);
}

//验证数组中数据是否为0到100的两位小数
function checkArrayFloat(str) {
    //var floatReg = /(?!^0\.0?0$)^[0-9][0-9]?(\.[0-9]{1,2})?$/;
    var floatReg =/^([1-9]\d{0,1}(\.\d{1,2})?|100)$/;
    return floatReg.test(str);
}

//-------------------------------------------------身份证验证-------start
  function CheckCardId(strCard) {
    var IsCheck = true;
    //校验长度，类型
    if (isCardNo(strCard) === false) {
      IsCheck= false;
    }

    //校验生日
    if (checkBirthday(strCard) === false) {
      IsCheck= false;
    }
    //检验位的检测
    if (checkParity(strCard) === false) {
      IsCheck= false;
    }
    return IsCheck;
  }

  //检查号码是否符合规范，包括长度，类型
  function isCardNo(card) {
    //身份证号码为15位或者18位，15位时全为数字，18位前17位为数字，最后一位是校验位，可能为数字或字符X
    var reg = /(^\d{15}$)|(^\d{17}(\d|X)$)/;
    if (reg.test(card) === false) {
      return false;
    }

    return true;
  };

  //检查生日是否正确
  function checkBirthday(card, birthID) {
    var len = card.length;
    //身份证15位时，次序为省（3位）市（3位）年（2位）月（2位）日（2位）校验位（3位），皆为数字
    if (len == '15') {
      var re_fifteen = /^(\d{6})(\d{2})(\d{2})(\d{2})(\d{3})$/;
      var arr_data = card.match(re_fifteen);
      var year = arr_data[2];
      var month = arr_data[3];
      var day = arr_data[4];
      var birthday = new Date('19' + year + '/' + month + '/' + day);
      if (Format(birthID) != "") {
        $("#" + birthID).val('19' + year + '/' + month + '/' + day);
      } else {
        return verifyBirthday('19' + year, month, day, birthday);
      }
    }
    //身份证18位时，次序为省（3位）市（3位）年（4位）月（2位）日（2位）校验位（4位），校验位末尾可能为X
    if (len == '18') {
      var re_eighteen = /^(\d{6})(\d{4})(\d{2})(\d{2})(\d{3})([0-9]|X)$/;
      var arr_data = card.match(re_eighteen);
      var year = arr_data[2];
      var month = arr_data[3];
      var day = arr_data[4];
      var birthday = new Date(year + '-' + month + '-' + day);
      if (Format(birthID) != "") {
        $("#" + birthID).val(year + '-' + month + '-' + day);
      } else {
        return verifyBirthday(year, month, day, birthday);
      }
    }
  return false;
  };

  //检查生日是否合理
  function verifyBirthday(year, month, day, birthday) {
    var now = new Date();
    var now_year = now.getFullYear();
    //年月日是否合理
    if (birthday.getFullYear() == year && (birthday.getMonth() + 1) == month && birthday.getDate() == day) {
      //判断年份的范围（3岁到100岁之间)
      var time = now_year - year;
        if (time >= 3 && time <= 100) {
          return true;
        }
        return false;
      }
    return false;
  }

  //校验位的检测
  function checkParity(card) {
  //15位转18位
  card = changeFivteenToEighteen(card);
    var len = card.length;
    if (len == '18') {
      var arrInt = new Array(7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2);
      var arrCh = new Array('1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2');
      var cardTemp = 0, i, valnum;
      for (i = 0; i < 17; i++) {
        cardTemp += card.substr(i, 1) * arrInt[i];
      }
      valnum = arrCh[cardTemp % 11];
      if (valnum == card.substr(17, 1)) {
        return true;
      }
      return false;
    }
    return false;
  };

  //15位转18位身份证号
  function changeFivteenToEighteen(card) {
    if (card.length == '15') {
      var arrInt = new Array(7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2);
      var arrCh = new Array('1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2');
      var cardTemp = 0, i;
      card = card.substr(0, 6) + '19' + card.substr(6, card.length - 6);
      for (i = 0; i < 17; i++) {
        cardTemp += card.substr(i, 1) * arrInt[i];
      }
      card += arrCh[cardTemp % 11];
      return card;
    }
    return card;
  };

  //取身份证前两位,校验省份
  function checkProvince(card,txtProvince) {
      var province = card.substr(0, 2);
      if (vcity[province] == undefined) {
        return false;
      } else {
      if (Format(txtProvince) != "") {
        $("#" + txtProvince).val(vcity[province]);
      }
    }
    return true;
  };

  //是否为日期格式
  function checkDate(RQ) {
    var date = RQ;
    var result = date.match(/^(\d{1,4})(-|\/)(\d{1,2})\2(\d{1,2})$/);

    if (result == null){
      return false;
    }
    var d = new Date(result[1], result[3] - 1, result[4]);
    d =(d.getFullYear() == result[1] && (d.getMonth() + 1) == result[3] && d.getDate() == result[4]);
    return d;
  }
  //备份
  function CheckCardIdBF(e) {
    var bDone = true;
    var Wi = new Array(7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2);
    var arrVerifyCode = new Array('1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2');
    var Checker = new Array('1', '9', '8', '7', '6', '5', '4', '3', '2', '1', '1');
    if (e.length < 15 || e.length == 16 || e.length == 17 || e.length > 18) {
      bDone = false;
      return false;
    }
    var Ai = "";
    if (e.length = 18) {
      Ai = e.substr(1, 17)
    } else if (e.length = 15) {
      Ai = e;
      Ai = e.substr(0, 6) + '19' + e.substr(6, e.length - 6);
    }
    if (isNaN(parseInt(Ai))) {
      bDone = false;
      return false;
    }

    var strYear, strMonth, strDay
    strYear = parseInt(Ai.substr(5, 4));
    strMonth = parseInt(Ai.substr(9, 2))
    strDay = parseInt(Ai.substr(11, 2))
    BirthDay = $.trim(strYear) + "-" + $.trim(strMonth) + "-" + $.trim(strDay);
    if (checkDate(BirthDay)) {
      // if (DateDiff("y", new Date(), BirthDay) < -140 || DateDiff("y", BirthDay, new Date()) < 0) {
      // bDone = false;
      // return false;
      // }
        if (strMonth > 12 || strDay > 31) {
        bDone = false;
        return false;
      }
    } else {
      bDone = false;
      return false;
    }

    var TotalmulAiWi = 0;
    for (var i = 0; i < 17; i++) {
      var ss = Wi[i];
      var dd = parseInt(Ai.substr(i, 1));
      TotalmulAiWi += parseInt(Ai.substr(i, 1)) * Wi[i];
    }
    var modValue
    modValue = TotalmulAiWi % 11
    var strVerifyCode
    strVerifyCode = arrVerifyCode[modValue]

    if (e.length = 18) {
      if (e.substr(18, 1) == "X") {
        e = e.substr(0, 17) + "x";
      }
      var dxssd = e.substr(17, 1);
      if (strVerifyCode != e.substr(17, 1)) {
        bDone = false;
        return false;
      }
    }
  }
//-------------------------------------------------身份证验证-------end

//防止sql注入
function Format(val) {
  if (val == null || typeof (val) == "undefined" || (val + "") == "null") {
    return "";
  } else {
    return val + "";
  }
}
```