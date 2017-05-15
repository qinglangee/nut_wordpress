# chrome DevTools 使用小提示

## 文件切换
`Ctrl + P`
## 在所有文件中查找
`Ctrl + Shift + F`   
## 跳到xx行
`Ctrl + G for Windows and Linux, (or Cmd + L for Mac)`
## 在控制台选择元素

    $() – Short for document.querySelector(). Returns the first element, matching a CSS selector ( e.g. $(‘div’) will return the first div element in the page).
    $$() – Short for document.querySelectorAll(). Returns an array of elements that match the given CSS selector.
    $0 – $4 – A history of the five most recent DOM elements that you’ve selected in the elements panel, $0 being the latest.
## 选中多个光标位置
按着 Ctrl 选就行了
## 保存 log
这个功能打勾就行
## 颜色选择器（吸管）
在css面板点击一个颜色，会有一个颜色选择器， 可以在网页中任意设置这个颜色
## 强制设置状态
如 :hover and :focus ， 见 tips 11

## 12. Visualize the shadow DOM

Web browsers construct things like textboxes, buttons and inputs out of other basic elements which are normally hidden from view. However, you can go to Settings -> General and toggle Show user agent shadow DOM, which will display them in the elements tab. You can even style them individually, which gives you a great deal of control.


## 13. Select next occurrence

If you press Ctrl + D (Cmd + D) while editing files in the Sources Tab, the next occurrence of the current word will be selected as well, helping you edit them simultaneously.

## 14. Change color format

Use Shift + Click on the color preview to alter between rgba, hsl and hexadecimal formatting.

## 15. Editing local files through workspaces

Workspaces are a powerful Chrome DevTools feature, which turns it into a real IDE. Workspaces match the files in the Sources tab to your local project files, so now you can edit and save directly, without having to copy/paste your changes into an external text editor.

To configure Workspaces, go to the Sources tab and right click anywhere in the left panel (where the sources are) and choose Add Folder To Worskpace, or just drag and drop your whole project folder into Developer Tools. Now, the chosen folder, its sub directories and all the files in them will be available for editing no matter what page you are on. To make it even more useful, you can then map files in your folder to those used by the page, allowing for live editing and easy saving.

You can learn more about Workspaces [here][2].
Further reading

[Chrome Keyboard Shortcuts][3]

[A long list of tips and tricks in the Google Chrome docs][4]



refs: 
[15 Must-Know Chrome DevTools Tips and Tricks][1]


[1]: http://tutorialzine.com/2015/03/15-must-know-chrome-devtools-tips-tricks/
[2]: https://developer.chrome.com/devtools/docs/workspaces
[3]: https://developer.chrome.com/devtools/docs/shortcuts
[4]: https://developer.chrome.com/devtools/docs/tips-and-tricks