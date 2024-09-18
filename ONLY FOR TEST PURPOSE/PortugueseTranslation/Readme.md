# 太吾英文社区翻译mod使用文档

## 目录
- [太吾英文社区翻译mod使用文档](#太吾英文社区翻译mod使用文档)
	- [目录](#目录)
		- [安装](#安装)
		- [Mod目录结构](#mod目录结构)
		- [界面语言包维护](#界面语言包维护)
		- [配置表语言包维护](#配置表语言包维护)
		- [各类名字语言包维护](#各类名字语言包维护)
		- [官方事件语言包维护](#官方事件语言包维护)
		- [Label调整风格维护](#label调整风格维护)
  
### 安装
	1. 创意工坊安装
		如果本mod已上传至创意工坊，直接订阅即可
	2. 社区安装包安装
		获取到本mod后，在游戏安装目录根目录创建Mod文件夹，将CommunityTranslation文件夹放入此文件夹即可。

### Mod目录结构
	从本mod根目录开始，要求必须存在 Languages/en 文件夹，在其内部放入各类语言包，各类名字相关的语言包请保持位于NameTranslations目录
	Plugins文件夹，Config.lua，Settins.lua文件为mod必须文件
	CustomLabelStyle为自定义调整指定界面的Label风格的配置文件，如果有新增文本调整需求，参考[Label调整风格维护](#label调整风格维护)可以在内部增加对应配置

### 界面语言包维护
	游戏更新发布后，把最新的ui_language.json放入Languages/en

### 配置表语言包维护
	游戏更新发布后，把最新的各配置表语言包放入Languages/en

### 各类名字语言包维护
	此类语言包一般改动很少，如发生变动，会有mod提示发现未翻译的名字，未翻译的名字也会自动写入 Languages/en/NameTranslations 目录下对应类型名字的MissingXXX.txt内，对应找到未翻译的内容，翻译后加入相应名字文件即可

### 官方事件语言包维护
	如果发现Languages/en目录不存在events.json文件，或者解析events.json文件后发现该文件并未全部翻译对应事件，按下左Ctrl+F12，将生成全部事件的events_cn.json文件，生成后的文件位于mod根目录，使用翻译工具翻译此文件的各个value到英文，把结果覆盖Languages/en/events.json即可。
	事件还存在一个选项可用条件文本语言包，文件名EventOptionTips_CN.txt，mod对这个文件名进行了修改:Languages/en/EventOptionTips.txt

### Label调整风格维护
	打开mod根目录下的CustomLabelStyle.json,要修改的Label所属的UI名字作为key，每个界面的修改需求对应一个Json数组。每个数组元素是一个修改需求，修改目标可以根据需要采用如下两种方式定位：
      	1. 根据绝对路径指定  
      		此修改方式要求数组元素的修改需求中存在Path为Key的一个路径，路径从本页面的第一级子节点开始指定
      	2. 指定一个根节点，修改其下全部的(包括未激活的)Label
      		此修改方式要求数组元素的修改需求中存在Root为Key的一个路径，路径从本页面的第一级子节点开始指定
	可选指定：
		1. 指定一个Key为ExcludeNames，Value为Json数组的键值对，数组的每个值都是一个字符串。定位修改目标时，如果label的名字存在于该数组，则这个label将不会被修改
		2. 指定一个Key为Width，Value为浮点数的键值对，可以修改目标Label的宽度
		3. 指定一个Key为Height，Value为浮点数的键值对，可以修改目标Label的高度
		4. 指定一个Key为IncludeParent，Value为布尔值的键值对，可以选择在修改目标Label的时候是否同步修改其父节点
		5. 指定一个Key为RepositionParent，Value为布尔值的键值对，可以选择在修改目标Label的时候是否重设其父节点的位置
    源码见mod文件TextMeshProCustomStyleHandler.cs
