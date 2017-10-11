# LogUtil
android手机端，车机端日志本地化，异常捕获上传工具，本地log文件在上传后或者三天以后将自动删除。

# Build
引入logutil.jar,Add as Library

# How to use
AndroidManifest.xml中添加

    <service android:name="com.neusoft.logutil.upload.UploadService" />

在Application的onCreate()方法中初始化

    //车机端
    LogManager.getInstance()
              .init(this, Environment.getExternalStorageDirectory().getPath() + "/LogUtil_Logs/", LogManager.LogType.TYPE_CAR)
              .setVehicleFactory("VehicleFactory")
              .setVehicleType("VehicleType")
              .setHost("Host")
              .setUuid("9999");

    //android App端
    LogManager.getInstance()
              .init(this, Environment.getExternalStorageDirectory().getPath() + "/LogUtil_Logs/", LogManager.LogType.TYPE_PHONE)
              .setVehicleFactory("VehicleFactory")
              .setVehicleType("VehicleType")
              .setHost("Host");

Log日志默认为关闭状态，打开或关闭LogCat输出（全局异常捕获始终开启）：

    LogUtil.getInstance().setIsOpen(context, true);

修改日志保存方式： PRINT_TYPE_LOGCAT（log打印） 或 PRINT_TYPE_FILE（本地保存）

    LogUtil.getInstance().setPrintType(context, PRINT_TYPE_FILE);

打印log日志，将自动本地化保存tag标签：

    LogUtil.e("test_log", "test");

获取所有保存的tag：

    LogUtil.getInstance().findAllTags();

修改单个tag开关状态，新保存的tag默认为开启状态：

    LogUtil.getInstance().changeTag("tag", true);

log日志压缩上传服务器，异常日志将自动上传，无需调用：

    LogManager.getInstance().upload();

# License

    Copyright 2017 zanjunrong
    
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
    http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
    
