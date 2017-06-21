# UCloud UFile JavaScript SDK

JavaScript SDK for [UCloud UFile（对象存储服务 Object storage service）]()

## 目录 Contents
#### &sect; [说明 Description](#intro)
#### &sect; [安装 Installation](#install)
#### &sect; [示例 Examples](#examples)
#### &sect; [API 列表 API List](#api)
##### &raquo; [获取文件列表 Get File List（getFileList）](#getFileList)
##### &raquo; [查询文件信息 Get File Detail information（getFileDetail）](#getFileDetail)
##### &raquo; [下载文件 Download File（downloadFile）](#downloadFile)
##### &raquo; [删除文件 Delete File（deleteFile）](#deleteFile)
##### &raquo; [普通上传 Upload File（uploadFile）](#uploadFile)
##### &raquo; [表单上传 Form Upload（formUpload）](#formUpload)
##### &raquo; [分片上传 Slice Upload（sliceUpload）](#sliceUpload)
##### &raquo; [秒传文件 High Speed Upload（hitUpload）](#hitUpload)

## <a name="intro">&sect; 说明 Description</a>

> SDK需要和服务端结合使用。先配置好环境，安装web服务器和解析php的服务。  
> The SDK needs to be used  with the server. First configure the environment,
> then install the web server and parse php services.

> 部署SDK到服务器，配置好[安装](#install)中指定的4个参数，访问服务器地址，即可操作[示例](#examples)中的功能。
> Deploy the SDK to the server, configure the four parameters specified in [install] (# install),and access the server address to operate the functions in [example] (# examples).

## <a name="install">&sect; 安装 Installation</a>

> SDK需要浏览器支持HTML5。
> SDK requires browser support for HTML5

> 将src目录中的spark-md5-3.0.0.min.js和ufile.js引入到您的项目中，如下所示。
> Insert spark-md5-3.0.0.min.js and ufile.js in the src directory into your project, as shown below.

```
<script type="text/javascript" src="sdk/spark-md5-3.0.0.min.js"></script>
<script type="text/javascript" src="sdk/ufile.js"></script>
```

> 配置`bucketName`和`bucketUrl`。  
> configure 'bucketName' and 'bucketUrl'

> 既可以在实例化时传参设置，也可以在src目录的ufile.js中全局设置。  
> You can set the parameters when you instantiate, or you can set it globally in ufile.js in the src directory.

> 配置`UCLOUD_PUBLIC_KEY`和`UCLOUD_PRIVATE_KEY`。
> configure 'UCLOUD_PUBLIC_KEY' and 'UCLOUD_PRIVATE_KEY'

> 在token_server.php中设置。   
> configure at token_server.php

> 在[UCloud控制台](https://console.ucloud.cn/apikey)中可以查看您的API密钥的`public_key`和`private_key`。
> You can view the `public_key` and` private_key` of your API key in the [UCloud Console] (https://console.ucloud.cn/apikey).

## <a name="examples">&sect; 示例 Examples</a>

- 获取文件列表 Get File List
- 查询文件信息 Get File Detail information
- 下载文件 Download File
- 删除文件 Delete File
- 普通上传 Upload File
- 表单上传 Form Upload
- 分片上传 Slice Upload
- 秒传文件 High Speed Upload

参见SDK中examples目录中的示例。  
目录中的jQuery和Bootstrap不是必须引入，只是为了方便演示。  

See the example in the examples directory in the SDK.
The directory of jQuery and Bootstrap is not necessarily introduced, just for the convenience of presentation.

## <a name="api">&sect; API</a>

### <a name="getFileList">&raquo; 获取文件列表 Get File List（getFileList）</a>

#### 接口功能 Interface function

> 获取Bucket的文件列表
> Get a list of bucket files

#### 请求参数 Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|success |false |function |请求成功的回调函数  successful callback function |
|error |false |function |请求失败的回调函数  failed callback function |

#### 返回参数 Return parameter

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|BucketId |string |对象存储空间ID Object storage space ID |
|BucketName |string |对象存储空间名称 Object storage space name |
|DataSet |array |文件信息列表 File information list|
|NextMarker |string |下一个标志字符串  next flag string|

#### DataSet

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|BucketName |string |对象存储空间名称 Object storage space name|
|CreateTime |number |文件创建时间 file created time|
|FileName |string |文件名称 file name |
|Hash |string |文件ETag file hash tag |
|MimeType |string |文件类型 file MimeType|
|ModifyTime |number |文件修改时间 file modifed time|
|Size |number |文件大小 file storage size |

#### 调用示例 Examples

```
ufile.getFileList(successCallBack, errorCallBack);
```

### <a name="getFileDetail">&raquo; 查看文件信息 Get File Detail information（getFileDetail）</a>

#### 接口功能 Interface function

> 查询文件基本信息
> Query the file basic information

#### 请求参数 Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|fileName |true |string |请求查询的文件名称 The name of the file asking for the query|
|success |false |function |请求成功的回调函数 successful callback function|
|error |false |function |请求失败的回调函数 failed callback function|

#### 返回参数  Return parameter

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|contentType |string |文件类型 file type|
|eTag |string |文件eTag file eTag |
|status |string |返回的HTTP状态码。查询成功是200，失败是404 200 is success, 404 is failed |
|response |string |API返回的response  response by API|

#### 调用示例 Examples

```
ufile.getFileDetail(fileName, successCallBack, errorCallBack);
```

### <a name="downloadFile">&raquo; 下载文件（downloadFile）</a>

#### 接口功能 Interface function

> 下载文件 download file

#### 请求参数 Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|fileName |true |string |请求下载的文件名称 requested download file name |
|success |false |function |请求成功的回调函数  successful callback function|
|error |false |function |请求失败的回调函数 failed callback function|
|progress |false |function |请求下载进度的回调函数 request |

#### success返回

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|response |Blob。具体参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob) |API返回的response |

#### response

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|size |number |文件大小 file size |
|type |string |文件类型  file type |

#### progress Return

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|response |number |上传进度比例。已完成上传文件大小/总上传文件大小的值，位于0-1之间。Upload progress ratio. The value of the uploaded file size / total upload file size is between 0-1 |

#### 调用示例 Examples

```
ufile.downloadFile(fileName, successCallBack, errorCallBack, progressCallBack);
```

### <a name="deleteFile">&raquo; 删除文件 delete file（deleteFile）</a>

#### 接口功能 Interface function

> 删除文件
> delete file

#### 请求参数 Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|fileName |true |string |请求删除的文件名称 Deleted file name |
|success |false |function |请求成功的回调函数 successful callback function|
|error |false |function |请求失败的回调函数 failed callback function |

#### 调用示例 Examples

```
ufile.deleteFile(fileName, successCallBack, errorCallBack);
```

### <a name="uploadFile">&raquo; 普通上传（uploadFile）</a>

#### 接口功能 Interface function

> 普通上传文件
> Upload File

#### 请求参数 Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|data |true |object |请求上传的参数 Request to upload parameters |
|success |false |function |请求成功的回调函数 successful callback function |
|error |false |function |请求失败的回调函数 failed callback function |
|progress |false |function |请求下载进度的回调函数 Request to download-progress of the callback function |

#### data

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|file |true |File。具体参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/File) |请求上传的文件|
|fileRename |false |string |文件的重新命名 file's new name |

#### progress返回

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|response |number |上传进度比例。已完成上传文件大小/总上传文件大小的值，位于0-1之间。Upload progress ratio. The value of the uploaded file size / total upload file size is between 0-1. |

#### 调用示例 Examples

```
ufile.uploadFile(data, successCallBack, errorCallBack, progressCallBack);
```

### <a name="formUpload">&raquo; 表单上传（formUpload）</a>

#### 接口功能 Interface function

> 说明：适合使用浏览器的场景并且上传文件内容可以在一次HTTP请求完成，并且所有PUT上传支持的参数都可以在表单上传中指定。
> Description: Suitable for the use of the browser scene and upload the contents of the file can be completed in an HTTP request, and all PUT upload support parameters can be specified in the form upload.


#### 请求参数

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|data |true |object |请求上传的参数 Request to upload parameters |
|success |false |function |请求成功的回调函数 successful callback function|
|error |false |function |请求失败的回调函数 failed callback function |

#### data

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|file |true |File。具体参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/File) |请求上传的文件|
|fileRename |false |string |文件的重新命名 file's new name|

#### 调用示例 Examples

```
ufile.formUpload(data, successCallBack, errorCallBack);
```

### <a name="sliceUpload">&raquo; 分片上传（sliceUpload）</a>

#### 接口功能 Interface function

> 说明：适合大文件上传
> Description: suitable for large file upload

#### Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|data |true |object |请求上传的参数 Request to upload parameters|
|success |false |function |请求成功的回调函数 successful callback function|
|error |false |function |请求失败的回调函数 failed callback function|
|progress |false |function |请求下载进度的回调函数 Request to download the progress of the callback function|

#### data

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|file |true |File。具体参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/File) |请求上传的文件|
|fileRename |false |string |文件的重新命名 files new name |

#### success返回

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|Bucket |string |对象存储空间名称 Object storage space name|
|Key |string |文件名称 file name|
|FileSize |string |文件大小 file size|

#### progress返回

|名称 name |类型 type |说明 description |
|:----- |:------|:----------------------------- |
|status |string |上传状态。init表示初始化分片；uploading表示分片上传中；uploaded表示完成分片。 |
|value |number |上传进度比例。已完成上传文件大小/总上传文件大小的值，位于0-1之间。 |

#### 调用示例 examples

```
ufile.sliceUpload(data, successCallBack, errorCallBack, progressCallBack);
```

### <a name="hitUpload">&raquo; 秒传文件（hitUpload）</a>

#### 接口功能 Interface function

> 说明：先判断待上传文件的hash值，如果UFile中可以查到此文件，则不必再传文件本身。
> Note: first determine the hash value of the file to be uploaded, if UFile can be found in this file, you do not have to repeat the file itself.

#### 请求参数 Request parameter

|名称 name |必选 required|类型 type|说明 description|
|:----- |:-------|:-----|----- |
|file |true |File。具体参见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/File) |请求上传的文件。 |
|success |false |function |请求成功的回调函数 successful callback function |
|error |false |function |请求失败的回调函数 failed callback function|

#### 调用示例 examples

```
ufile.hitUpload(file, successCallBack, errorCallBack);
```
