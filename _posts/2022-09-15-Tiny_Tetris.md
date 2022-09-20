---
title: tinyTetris源码解读
author: SHKChan
date: 2022-09-19
category: C++
layout: post
---
在GitHub上看到一个简单的俄罗斯方块开源项目,这里记录一下对其源码的解读.
Github地址:https://github.com/taylorconor/tinytetris

- main函数
```
/*******************
@func: main function
*******************/
// init curses and start runloop
int main() {
  srand(time(0));
  initscr();	// 初始化curses库
  start_color();	// 初始化curses库的颜色功能
  // colours indexed by their position in the block
  for (int i = 1; i < 8; i++) {
    init_pair(i, i, 0);	// 更改某个颜色对的定义,接受参数为(要更改的颜色对编号,前景色编号,背景色编号)
  }
  new_piece();	// 创建一个新方块(未绘制)
  resizeterm(22, 22);	// 将标准窗口和当前窗口的大小调整为指定的尺寸
  noecho();	// 关闭终端回显功能
  timeout(0);	// 为窗口非阻塞读取行为,当没有输入在等待时 getch() 将返回 -1.
  curs_set(0);	// 设置光标状态为可见
  box(stdscr, 0, 0);	// 在窗口边缘绘制边框
  runloop();	// 流程主循环
  endwin();	// 关闭curses库,终端恢复正常
}
```

- 