---
title: 原生半屏内容发布器
header: develop
nav: api
sidebar: open_replyeditor
---

## swan.openReplyEditor

> 基础库 3.100.4 版本开始支持，以下版本请使用小程序发布器组件。

**解释**： 调起原生半屏内容发布器，并支持开发者配置发布器展示模块。
**方法参数**：Object object

|参数名 |类型  |必填 | 默认值 |说明|
|---- | ---- | ---- | ----|----|
|sendBackgroundColor   | String  |  否  | #3388ff |发布按钮填充颜色，支持#333 和#333333 两种写法|
|sendTextColor  |  String  | 否 | #FFFFFF |发表按钮颜色，支持#333 和#333333 两种写法|
|sendText  |  Object  | 否 | 发表 | 发表的显示文案|
|contentPlaceholder  |  String  | 否 | 请输入内容|内容提示占位文案|
|moduleList  |  Array  | 否 | -|显示模块list|
|emojiPath  |  String  | 否 | -|设置自定义表情配置路径|
|success  |  Function  | 否 | -|发布内容的回调函数|
|fail  |  Function  | 否 | -|调起失败的回调函数|
|complete  |  Function  | 否 | -|接口调用结束的回调函数（调用成功、失败都会执行）|



**success返回参数说明**：

|参数名 |类型 | 说明|
|---- | ---- | ---- |
| status  | String |当前发布器状态  reply: 点击发表按钮；draft: 草稿状态，发布器当前为隐藏状态。|
| tempFile  | ` Array.<object> ` |图片的本地文件列表，每一项是一个 File 对象。|
| content | String | 正文 |


**moduleList 列表**：
若moduleList传空数组或不传，则默认展示正文、图片模块、表情模块。若传值，则只展示所传 list 中配置的模块。 
如：`moduleList: ['image']` 则只展示图片模块。

|moduleList| 类型 |描述|
|---|---|---|
|image|String|图片模块|
|emoji|String|表情模块|


**emojiPath 参数说明**：

开发者在配置 emoji 模块后，可以选择是否使用自定义表情表。若使用自定义表情功能，则将自定义表情的资源文件夹路径传入 emojiPath 字段。若不传 emojiPath 字段则使用默认表情包。

自定义表情资源文件夹格式：
文件夹中包括：`emoji.json` 和所有表情图片资源。外层文件夹名字可以由开发者自由定义，路径配置在 emojiPath 中即可，`emoji.json` 为固定文件名，请开发者按格式创建。表情没有数量和大小限制，但是表情资源会占用包体大小。

![图片](../../../img/api/community_editor/emoji_path.jpg)
`emoji.json` 格式：
![图片](../../../img/api/community_editor/emoji_json.jpg)



**示例**：

<a href="swanide://fragment/a013aec8b73e24ed9f6bbf11f4f1cd431566889380983" title="在开发者工具中预览效果" target="_self">在开发者工具中预览效果</a>

```js
swan.openReplyEditor({
    sendBackgroundColor: '#3388ff',
    sendTextColor: '#FFFFFF',
    sendText: '发送',
    contentPlaceholder: '请输入评论内容',
    moduleList: ['emoji'],
    emojiPath: '../../emojidata',
    success: function (res) {
      console.log('openReplyEditor success', res);
      // 点击了发表按钮
      if (res.status === 'reply') {
		    // 开发者处理返回内容。
        // 主动关闭评论发布器
        swan.closeReplyEditor({
          success: function (res) {
            console.log('closeReplyEditor success', res);
          }
        });
      }
      // 点击发布器外隐藏发布器，编辑的内容将存为草稿
      else if (res.status === 'draft') {
          // 处理草稿内容，如ui处理
      }

    },
    fail: function (res) {
      console.log('openReplyEditor fail', res);
    },
    complete: function (res) {
      console.log('openReplyEditor complete', res);
    }
})
```

## swan.closeReplyEditor

> 基础库 3.100.4 版本开始支持，以下版本请使用小程序发布器组件。

**解释**： 关闭原生半屏内容发布器

**方法参数**：Object object

**emojiPath 参数说明**：

|参数名 |类型  |必填 | 默认值 |说明|
|---- | ---- | ---- | ----|----|
|success  |  Function  | 否 | -|发布内容的回调函数|
|fail  |  Function  | 否 | -|调起失败的回调函数|
|complete  |  Function  | 否 | -|接口调用结束的回调函数（调用成功、失败都会执行）|

**示例**：

<a href="swanide://fragment/60bcc47865b41b72a8e375455c11857b1566889666184" title="在开发者工具中预览效果" target="_self">在开发者工具中预览效果</a>

```js
swan.openReplyEditor({
    sendBackgroundColor: '#3388ff',
    sendTextColor: '#FFFFFF',
    sendText: '发送',
    contentPlaceholder: '请输入评论内容',
    moduleList: ['emoji'],
    emojiPath: '../../emojidata',
    success: function (res) {
      console.log('openReplyEditor success', res);
      // 点击了发表按钮
      if (res.status === 'reply') {
	      	// 开发者处理返回内容。
          // 主动关闭评论发布器
          swan.closeReplyEditor({
            success: function (res) {
              console.log('closeReplyEditor success', res);
            }
          });
	    }
      // 点击发布器外隐藏发布器，编辑的内容将存为草稿
      else if (res.status === 'draft') {
        // 处理草稿内容，如ui处理
      }
    },
    fail: function (res) {
      console.log('openReplyEditor fail', res);
    },
    complete: function (res) {
      console.log('openReplyEditor complete', res);
    }
})
```