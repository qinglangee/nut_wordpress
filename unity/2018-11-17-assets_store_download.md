# 手动下载 unity assets store 中的 asset

是不可能的， 只能在unity中下载。 
unity中开始下载后，后放在临时目录中。
生成一个临时文件 `C:\\Users\(your-user-name)\\AppData\\Roaming\\Unity\\Asset Store\(asset-developer-name)\(asset-category)\(asset-name).json`.
json文件中有下载链接。这个链接可以在浏览器中下载文件，但是加密的。可以把下载的文件改成unity的临时文件名，放到对应目录下，重启unity让它来完成解压。

*On a mac it's located under "~/Library/Unity/Asset\ Store".*