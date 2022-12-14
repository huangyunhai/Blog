---
layout: post
category: Unity
tags: Unity
---
Unity 在移动端中文本输入，如果抛开与平台相关更加紧密的安卓Java代码与iOS Objective-C代码，那么应该重点关注的是InputField类和TouchScreenKeyboard类。
InputField类是UGUI的输入组件。TouchScreenKeyboard类顾名思义就是移动端的半屏输入工具类。查看InputField的API文档，可以发现InputField中有个TouchScreenKeyboard的属性，其实就是输入框在移动端输入是唤醒的半屏输入法。
下面介绍下安卓端和iOS端的一些异同点。
1. 不同点，Android下的半屏输入法是会有个全屏遮罩，点击键盘以外的地方收起键盘，不会触发游戏中界面的点击事件。iOS则没有这个遮罩。并且在点击其他区域收起键盘时，在InputField的OnEditEnd事件中获取到的TouchScreenKeyboard的状态时LostFocus。在iOS中则为Canceled
```c#
// Android
inputField.touchScreenKeyboard.status == TouchScreenKeyboard.Status.LostFcous
// iOS
inputField.touchScreenKeyboard.status == TouchScreenKeyboard.Status.Canceled
```
2. 相同点，在Android或iOS设备上弹出来的半屏输入框中，点击确定按钮或回车键，在OnEditEnd事件中获取到的TouchScreenKeyboard的status都是Done.
```c#
// 点击确定按钮
if(inputField.touchScreenKeyboard.status == TouchScreenKeyboard.Status.Done)
{
	// TODO: do something when input finish
}
```
3. 相同点，在Android和iOS上，如果InputField的ContentType是Standard，弹出来的半屏输入框，允许输入emoji表情，但是在InputField和游戏内的Text都是无法显示的。