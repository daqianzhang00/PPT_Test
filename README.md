# Quarto Slide模板
## 一、描述
本项目简要介绍如何用Quarto制作学术汇报Slide，并提供简单的模板。

## 二、渲染方法(仅展示Windows)
1. **在VS Code中安装Quarto。**
```
code --install-extension quarto.quarto
```
2. **编译自己的.qmd文件。** .qmd文件包括两个部分，第一部分是*YAML头部*，用于设置元数据和指定模板，第二部分是*正文内容*，语言格式与Markdown语言相同。
3. **用Quarto渲染。** 在VS Code终端框内输入渲染代码：
```Powershell
Quarto render 渲染文件名.qmd
```
4. **查看渲染文件。** 渲染后的文件名为*渲染文件名.html*，可在浏览器或VS Code中正常打开，则说明渲染成功。
5. **需要搭配_files文件使用。** 如果需要发给别人看，需要将*文件名.html* 文件和 *文件名_files* 文件夹一起发送，才能正常观看，否则就是无格式Slide模板。
## 三、主要参考
**2026年江财数经院陈志远老师暑期课程**  
- 参考陈志远老师Slide模板[`ruc-theme.scss`](./ruc-theme.scss) ，已放在文件夹中，如有需要可下载使用，来源是[陈志远老师主页](https://github.com/zhiyuanryanchen/zhiyuanryanchen.github.io)。
- 同时作者也做了微薄的修改，重新命名为[`JFDE-theme.scss`](./JFDE-theme.scss),已上传到GitHub。
- 该暑期课程陈志远老师也已上传到github账号上，感兴趣的同学可以去[陈志远老师主页](https://github.com/zhiyuanryanchen/zhiyuanryanchen.github.io)查看。
## 四、主要修改
1. **主题色修改**：[`原文件`](./ruc-theme.scss)主题色为Prussian Blue + Cyan，修改为JFDE Blue + JFDE Gold。
2. **字体修改**：添加了HarmonyOS Sans SC作为首选字体，该字体常用于商务汇报，免费可商用。
3. **字体颜色修改**：将大部分字体颜色设为黑色。
4. **强调框格式修改**：强化强调框格式对比度，增强阅读性。
5. **页码设置**：增加了Slide页码显示。

调整后Slide表现良好，测试Slide参见[AI_Investment.html](./ai_investment.html).
## 五、致谢
感谢陈志远老师精彩纷呈的教学，作者做此分享的目的一部分也是为了练习课上所学的git版本控制和github远程协作，同时也是对制作Slide有一定兴趣。如有同对制作Slide感兴趣、愿意指出模板不足并与我一同改进的同学，欢迎通过邮箱[qikaizhang2002@qq.com](mailto:qikaizhang2002@qq.com)与我联系，互相探讨。