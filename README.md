## 原理

本demo是在浏览器运行的人脸口罩检测网页demo，介绍如何将深度学习的人脸口罩检测模型部署到浏览器里面。

深度学习模型，可以借助TensorFlow.js库，运行在浏览器里。首先，需要使用`tensorflowjs_converter`将tensorflow的`graph model`或者keras的`layer model`转换为TensorFlow.js支持的模型。
该工具可以通过`pip install tensorflowjs`安装。

如果使用Keras模型转的操作如下：
```
tensorflowjs_convert --input_format keras --output_format tfjs_layers_model   /path/to/keras/hdf5/model  /path/to/output/folder
```
模型会生成`model.json`文件和一个或者多个`bin`文件，其中前者保存模型的拓扑，后者保存模型的权重。
使用JavaScript，需要在html中先引入`tfjs.min.js`库，然后加载模型
```
<script src="js/tfjs.min.js"></script> 

```
在`detection.js`中，加载模型
```
model = await tf.loadLayersModel('./tfjs-models/model.json');
```
置于anchor生成、输出解码、nms与使用python版本并无太大差异，大家可以查看`detection.js`中三个相关的函数，一目了然。

## 运行方法
在当前目录下打开终端，只需要建立一个最小web server即可。
对于使用python的用户
```
// python3用户
python -m http.server
// python2用户
python -m SimpleHTTPServer

```
如果你使用Node.js
```
npm install serve -g //安装serve
serve // this will open a mini web serve
// 您也可以使用http-serve
npm install http-server -g
http-server
```