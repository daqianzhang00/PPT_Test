# Quarto Slide模板
## 一、描述
本项目简要介绍如何用Quarto制作学术汇报Slide，并提供简单的模板。
## 二、主要参考
**2026年江财数经院陈志远老师暑期课程**  
参考陈志远老师Slide模板[`ruc-theme.scss`](./ruc-theme.scss) ，做了微薄的修改，重新命名为[`JFDE-theme.scss`](./JFDE-theme.scss),该暑期课程陈志远老师也已上传到github账号上，感兴趣的同学可以去[陈志远老师主页](https://github.com/zhiyuanryanchen/zhiyuanryanchen.github.io)查看。
## 三、主要修改
1. **主题色修改**：原文件主题色对比度较低，[`原文件`](./ruc-theme.scss)主题色为Prussian Blue + Cyan，修改为JFDE Blue + JFDE Gold。
2. **字体修改**：原文件字体较细，因此添加了HarmonyOS Sans SC作为字体，该字体区分度高，免费可商用。
3. **字体颜色修改**：将大部分字体颜色设为黑色，增强学术汇报严肃性。
4. **强调框格式修改**：原文件强调框颜色和文字颜色对比度较差，修改稿强化了对比度，增强阅读性。
5. **页码设置**：增加了Slide页码。

调整后Slide表现良好，测试Slide参见[AI_Investment.html](./AI_Investment.html).
## 四、渲染方法(仅展示Windows)
1. **在VS Code中安装Quarto。**
```
code --install-extension quarto.quarto
```
2. **编译自己的.qmd文件。**.qmd文件包括两个部分，第一部分是*YAML头部*，用于设置元数据和指定模板，第二部分是*正文内容*，语言格式与Markdown语言相同。
3. **用Quarto渲染。**在VS Code终端框内输入渲染代码：
```Powershell
Quarto render 渲染文件名.qmd
```
4. **查看渲染文件。**渲染后的文件名为*渲染文件名.html*，可在浏览器或VS Code中正常打开，则说明渲染成功。
## 五、致谢
感谢陈志远老师精彩纷呈的教学，作者做此分享的目的一部分也是为了练习课上所学的git版本控制和github远程协作，同时也是对制作Slide有一定兴趣，欢迎同对制作Slide感兴趣的同学通过邮箱[qikaizhang2002@qq.com](mailto:qikaizhang2002@qq.com)与我联系。