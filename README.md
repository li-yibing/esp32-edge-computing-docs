# 文档说明

文档地址：https://github.com/li-yibing/esp32-edge-computing-docs。
 
本仓库为[esp32-edge-computing](https://github.com/li-yibing/esp32-edge-computing)项目的说明文档。

## 文档构建说明
1. 你可以编辑任何在[docs](docs)文件夹中的`*.md`文件。
2. 然后创建PR请求合并到`main`分支(或者直接在`main`分支编辑).
3. 当发生合并时, [Github Actions](https://github.com/li-yibing/esp32-edge-computing-docs/actions)会重新生成文档并放置在`gh-pages`分支。 这个分支的内容会自动展示在[文档站点](https://li-yibing.github.io/esp32-edge-computing-docs/)。

## 编辑页面
每个页面的右上角都有`Edit on GitHub`，点击可以进入GitHub进行编辑。

## 添加新页面
1. 在[docs](docs)文件夹添加`*.md`文件。
2. 在[docs/nav.yml](docs/nav.yml)添加**文件名**，并且注意控制层级关系。

## 解析文档
在主项目中[configfile](https://github.com/li-yibing/esp32-edge-computing/rolling/sd-card/config/config.ini)的每一个参数都进行了列举。
他们的相关描述都在`param-docs/parameter-pages`(通过config模块进行配置)。
当文档发生变化时，在`param-docs`文件夹下的`concat-parameter-pages.py`脚本需要被执行一次。
这在Github action自动执行。
它会将所有的文档添加到`../docs/Parameters.md`，这个文档被`mkdocs`所需要。

### 模板生成
当任何新参数添加到配置文件中，`generate-template-param-doc-pages.py`脚本都需要重新执行。
然后检查是否每一个配置都有了对应的页面。
 - 如果没有页面则生成一个模板页面。
 - 如果页面已经存在，则不做任何变更。

如果参数出现在`expert-params.txt`列表中, 会提示**Expert warning**。

如果参数出现在`hidden-in-ui.txt`列表中, 会提示**Note**。

## 格式化
### 文本块
可以使用 **!!!**扩展来创建一个文本块。
```
!!! Note
    I am a note
```
记得增加4个空格!
可选的类型有: `attention, caution, danger, error, hint, important, note, tip, warning`
详见 https://python-markdown.github.io/extensions/admonition/。

## 本地测试
在本地测试:
1. 克隆仓库
2. 安装文档创建工具(详见[.github/workflows/build-docs.yaml](.github/workflows/build-docs.yaml)):
    ```
    pip install --upgrade pip
    pip install mkdocs mkdocs-gen-files mkdocs-awesome-pages-plugin mkdocs-material pymdown-extensions mkdocs-enumerate-headings-plugin
    ```
3. 在仓库文件夹, 调用`mkdocs serve`(保证其运行)，会自动产生文档。
  你可以在 http://127.0.0.1:8000/AI-on-the-edge-device-docs/查看。
    
  任何文件的变更都是自动发布更新的。
