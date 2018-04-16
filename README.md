# 灯塔在线自动答题

本JS代码仅供交流学习，请勿用作非法用途。

**使用说明：**

>题目出现后，在你要答题的页面点击F12（不是本页面），点击Console或者控制台，复制输入下面的代码，点击回车或者运行，“自动答题”。

```
let answers=[];let answerIndex=0;$.ajax({type:'POST',url:'http://xxjs.dtdjzx.gov.cn/quiz-api/game_info/lookBackSubject',data:{roundOnlyId:JSON.parse(localStorage.w_allHuiKan2).data.roundOnlyId},dataType:"json",success:function(res){let data=res.data.dateList;var str='';if(res.code==200&&data.length>0){for(var i=0;i<data.length;i++){answers.push(data[i].answer)}oneti()}else{console.log(`roundOnlyId错误！`)}}})$(".W_fl").append("<span id='divMsg' style='position:  absolute;margin-left: 180px;display: none;' >");let msgDiv=$("#divMsg");msgDiv.text("请控制交卷时间在30s之后，否则会被系统检测！");msgDiv.css({"border":"3px solid blue"});msgDiv.css({"color":"#0ef"});msgDiv.fadeIn();let index=0;let elemLi=$(".w_charu li");let length=elemLi.length;function oneti(){if(index<length){var e=elemLi[index];index++;getAns(e)}}let w_btn_tab_down=$(".w_btn_tab_down");function getAns(e){let thisAnswer=answers[answerIndex++];let ans=thisAnswer.split(',');ans.forEach(a=>{$(e).find("input[value="+a+"]").click()});gzzrClick()}function gzzrClick(){clientXArr.push(gzzrRdm(540,620));clientXArrY.push(gzzrRdm(530,550));w_btn_tab_down.click();oneti()}function gzzrRdm(min,max){return Math.floor((Math.random()*(max-min+1)+min))}function countX(){var obj={},arr=clientXArr,maxArr=[];for(var i=0,len=arr.length;i<len;i++){if(obj[arr[i]]){obj[arr[i]]++;maxArr.push(obj[arr[i]])}else{obj[arr[i]]=1}}maxArr=maxArr.sort(function(x,y){return x-y});repeatX=maxArr.length>0?maxArr[maxArr.length-1]:0}
```
