// 回到首页
home();
sleep(2000);

// 打开抖音
app.launchApp("抖音");
sleep(5000);

// 获取屏幕分辨率
let screenHeight = device.height;
let screenWidth = device.width;

while (true) {
  // 点赞
  sleep(1000);

  // 关注
  let gzId = id("com.ss.android.ugc.aweme:id/f03");
  if (gzId) {
    let gzView = gzId.findOnce();
    if (gzView) {
      let position = gzView.bounds();
      click(position.centerX(), position.centerY());
      sleep(1000);
    }
  }
  sleep(5000);

  // 短视频的滑动
  swipe(
    screenWidth / 2,
    (screenHeight / 3) * 2,
    screenWidth / 2,
    screenHeight / 4,
    500
  );
  sleep(2000);
}