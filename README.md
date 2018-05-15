# dt在线自动答题

本JS代码仅供交流学习，请勿用作非法用途。

**使用说明：**

>推荐使用手动版本（以防检测机制突然更新）

>题目出现后，在你要答题的页面点击F12（不是本页面），点击Console或者控制台，复制输入下面的代码，点击回车或者运行。
>由于答题系统可能更新，请每次答题前访问本页面获取最新的代码，确保答案无误。

>>手动版本

```
let answers = [];
let answerIndex = 0;
$.ajax({
    type: 'POST',
    url: 'http://xxjs.dtdjzx.gov.cn/quiz-api/game_info/lookBackSubject',
    data: {
        roundOnlyId: JSON.parse(localStorage.w_allHuiKan2).data.roundOnlyId
    },
    dataType: "json",
    success: function(res) {
        let data = res.data.dateList;
        var str = '';
        if (res.code == 200 && data.length > 0) {
            for (var i = 0; i < data.length; i++) {
                answers.push(data[i].answer);
            }
            oneti();
        } else {
            console.log(`roundOnlyId错误！`);
        }
    }
})
$(".W_fl").append("<span id='divMsg' style='position:  absolute;margin-left: 180px;display: none;' >");
let msgDiv = $("#divMsg");
msgDiv.text("手动版本：带有绿色边框为正确选项！");
msgDiv.css({
    "border": "3px solid blue"
});
msgDiv.css({
    "color": "#0ef"
});
msgDiv.fadeIn();
let index = 0;
let elemLi = $(".w_charu li");
let length = elemLi.length;

function oneti() {
    if (index < length) {
        var e = elemLi[index];
        index++;
        getAns(e);
    }
}

function getAns(e) {
    let thisAnswer = answers[answerIndex++];
    let ans = thisAnswer.split(',');
    ans.forEach(a => {
        $(e).find("input[value=" + a + "]").parent().css("border", "2px solid green");
    });
    oneti();
}
```
