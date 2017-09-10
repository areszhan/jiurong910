const  request  =  require（' request '）;
const  schedule  =  require（' node-schedule '）;

const  sendReminder  =（message，ifAt  =  true，ifAtAll  =  false）=> {
  request（{
    url ： ' https : //oapi.dingtalk.com/robot/send?access_token=bfc3085a381072cc6ee352738ad0293c22365a34bebbe3cdf62eea3cccc0c04e '，
    方法： “ POST ”，
    标题： {
      “ content-type ”： “ application / json ”，
    }，
    身体： JSON。stringify（{
      “信息类型”： “文本”，
      “ text ”： {
        “内容”：消息
      }，
      “ at ”： {
        “ atMobiles ”： [
          ifAt ？“ 15829679148 ”：null
        ]
        “ isAtAll ”： 虚假
      }
    }）
  }，function（error，response，body）{
    控制台。日志（正文）;
    如果（！错误&&  响应。的StatusCode  ===  200）{
    }
  }）;
}

/ **
 * * * * * *
 ┬┬┬┬┬┬
 │││││|
 │││││└星期几（0  -  7）（0或7是太阳）
 ││││└────月（1  -  12）
 │││└────────月（1  -  31）
 ││└────────────小时（0  -  23）
 │└────────────────分钟（0  -  59）
 └──────────────────────────────────────────────────────────────────
 * /

// sendReminder（'重启完成，我进入工作状态啦！'，false）;
// schedule.scheduleJob（'0 10 * * 1-5'，function（）{
//    sendReminder（'晨会30分钟准备\ n-统计内网+ RDC的昨日BUG，本月BUG \ n-浏览各个项目的进度\ n-昨日验收会BUG跟进\ n-对外Vone修改指派人\ n更新前一天版本，修改状态，设置新版本“）;
// }）;
// schedule.scheduleJob（'25 10 * * 1-5'，function（）{
//    sendReminder（'晨会5分钟准备\ n-打开云雀晨会纪要+ Aone项目域看板视图\ n-大电视就位'）;
// }）;
// schedule.scheduleJob（'29 10 * * 1-5'，function（）{
//    sendReminder（'晨会即将开始\ n-在群里通知大家参会\ n-结束后发布晨会纪要，并更新'）;
// }）;
时间表。scheduleJob（' 0 13 * * 5 '，function（）{
  sendReminder（'项目域周会4小时准备\ n - 统计本周线上BUG情况'）;
}）;
时间表。scheduleJob（' 30 16 * * 1-5 '，函数（）{
  sendReminder（'验收会30分钟准备\ n - 在群里提醒大家提前把变进拉进预发环境'）;
}）;
时间表。scheduleJob（' 59 16 * * 1-5 '，函数（）{
  sendReminder（'验收会即将开始\ n - 在群里通知相关人员参会\ n - 结束后发布验收结果'）;
}）;
