# LINE botのやつで作ったWebAPI



https://script.google.com/home/projects/1R_Md0jJtHqIyIcIFY37paBb9rH8HpvvLCufv9WY2vACa9SrK5yYcqX5Q/edit



```gas
//HTTP GETをハンドリングする
function doGet(e) {
  //リクエストパラメータ名"text"の値を取得する
  const searchDate = new Date(e.parameter.date);

  // console.log(searchDate);

  const events = getCalendarEvents(searchDate);
  
  let result = {
    message: events
  }

  let out = ContentService.createTextOutput();
  //Mime TypeをJSONに設定
  out.setMimeType(ContentService.MimeType.JSON);
  //JSONテキストをセットする
  out.setContent(JSON.stringify(result));
  return out;
}

const CALENDAR_ID = 'bv7ufj9tt81i9v57c80hhh7nnhamek8d@import.calendar.google.com'; //カレンダーID
function getCalendarEvents(searchDate) {
  const calendar = CalendarApp.getCalendarById(CALENDAR_ID);
   
  const events = calendar.getEventsForDay(searchDate);
 
  let res = [];
  for(const event of events){
    // title: event.getTitle(),
    const startTime = Utilities.formatDate(event.getStartTime(), "JST", "yyyy-MM-dd'T'HH:mm:ss'Z'");
    const endTime = Utilities.formatDate(event.getEndTime(), "JST", "yyyy-MM-dd'T'HH:mm:ss'Z'");

    const record = {
      title: event.getTitle(),
      startTime: startTime.substring(11,19),
      endTime: endTime.substring(11,19),
    }
    
    res.push(record);
  }
  return res;
}
```



doGet(e):=e.parameter.dateに`yyyy/mm/dd`の形式で来る予定なのでその日付のカレンダーの情報を返す

getCalendarEvents(date):=事前に準備したカレンダーIDからカレンダーのdate日の情報を引っ張ってくる

公式ドキュメント↓

https://developers.google.com/apps-script/reference/utilities/utilities#formatDate(Date,String,String)





やってることとしてはすごく簡単

ABCのBレベル

