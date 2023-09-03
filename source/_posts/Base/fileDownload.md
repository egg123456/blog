---
title: fileDownload
date: 2018/5/2
categories:
- base
---
> 文件下载可分为两种方式，一、文件链接方式，像平常的 a 标签，window.open 都可以下载。二、文件流方式(二进制流)，一般使用场景为后端导出的报表。

### 链接方式
1. a 链接
```html
  <a href="http://xxxx" target="_blank" download="fileName">download</a>
```
+ 优点：
  可以直接下载txt、png、pdf、exe、xlsx等类型文件
+ 缺点：
  a标签只能做get请求，所以url有长度限制
  无法获取下载进度
  跨域限制
  无法在header中携带token做鉴权操作
  无法判断接口是否成功
  IE兼容问题
2. window.open
+ 优点：
  简单方便
+ 缺点：
  会出现URL长度限制问题
  需要注意url编码问题
  无法获取下载进度
  无法在header中携带token做鉴权操作
  无法判断接口是否成功
  无法直接下载浏览器可直接预览的文件类型（txt、png、pdf会直接预览）
3. window.location.href
+ 优点
  简单方便直接
  可以下载大文件(G以上)
+ 缺点
  会出现URL长度限制问题
  需要注意url编码问题
  无法获取下载进度
  无法在header中携带token做鉴权操作
  无法直接下载浏览器可直接预览的文件类型（txt、png、pdf会直接预览）
  无法判断接口是否返回成功



### 文件流下载
```js
/**
 * 下载二进制文件
 * @param {string} url 请求地址
 * @param {object} params 请求参数
 */
export function downLoadFile(url, params) {
  return axios
    .request({
      url,
      method: 'get',
      params,
      responseType: 'blob',
    })
    .then((res) => {
      const { data, headers } = res;
      // 在 JavaScript 中 Blob 类型的对象表示一个不可变、原始数据的类文件对象。 它的数据可以按文本或二进制的格式进行读取，也可以转换成 ReadableStream 用于数据操作。
      const blob = new Blob([data], { type: headers['content-type'] });
      const fileName = decodeURI(
        headers['content-disposition'].replace(/\w+; filename="(.*)"/, '$1')
      );
      if ('download' in document.createElement('a')) {
        // 非IE下载
        const elink = document.createElement('a');
        elink.download = fileName;
        elink.style.display = 'none';
        // 创建blob url（生成的 URL 存储了一个 URL → Blob 映射）
        elink.href = URL.createObjectURL(blob);
        document.body.appendChild(elink);
        elink.click();
        URL.revokeObjectURL(elink.href); // 释放URL 对象
        document.body.removeChild(elink);
      } else {
        // IE10+下载
        navigator.msSaveBlob(blob, fileName);
      }
    })
    .catch(async (err) => {
      const text = (await err.response?.data?.text()) || '{}';
      message.error(JSON.parse(text)?.message);
    });
}
```
+ 优点：
  可以下载txt、png、pdf等类型文件
  可以在header中携带token做鉴权操作
  可以获取文件下载进度
  可以判断接口是否返回成功
+ 缺点：
  兼容性问题，IE10以下不可用，注意Safari浏览器,官网给出 Safari has a serious issue with blobs that are of the type application/octet-stream 将后端返回的文件流全部获取后才会下载

[quote](https://blog.csdn.net/kaiup/article/details/124771466)