# 项目名称
ThinkPHP5+微信小程序商城

# 项目预览
![gif](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/preview.gif)
#### 商城首页
![img](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/1.PNG)
![img](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/2.PNG)
![img](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/3.PNG)
#### 商城分类页
![img](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/4.PNG)
#### 商品详情页
![img](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/5.PNG)
#### 商品购物车页
![img](https://raw.githubusercontent.com/Vanvansama/TP5_MiniPrograms/master/PreviewImage/6.PNG)

# 特性
1.  api采用RESTFul API风格
（RESTFul API风格可参考GitHub 开发者文档）
返回码、URL语义、HTTP动词、错误码、异常返回
使用Token令牌来构建用户授权体系
API版本控制（v1、v2）

2.  TP5三大核心：路由、控制器、模型
以ORM的方式查询数据库
使用TP5验证器Validate构建整个验证层
开发环境和生产环境下不同的全局异常处理机制
TP5缓存的使用
在TP5中使用数据库事务

3.  微信小程序登录状态维护
微信支付接入
微信模板消息
Class和Module面向对象的思维构建前端代码
前端如何管理用户令牌
体验优化

# 项目接口
~~~
//Banner
Route::get('api/:version/banner/:id', 'api/:version.Banner/getBanner');

//Theme
Route::group('api/:version/theme',function(){
    Route::get('', 'api/:version.Theme/getSimpleList');
    Route::get('/:id', 'api/:version.Theme/getComplexOne');
    Route::post(':t_id/product/:p_id', 'api/:version.Theme/addThemeProduct');
    Route::delete(':t_id/product/:p_id', 'api/:version.Theme/deleteThemeProduct');
});

//Product
Route::post('api/:version/product', 'api/:version.Product/createOne');
Route::delete('api/:version/product/:id', 'api/:version.Product/deleteOne');
Route::get('api/:version/product/by_category/paginate', 'api/:version.Product/getByCategory');
Route::get('api/:version/product/by_category', 'api/:version.Product/getAllInCategory');
Route::get('api/:version/product/:id', 'api/:version.Product/getOne',[],['id'=>'\d+']);
Route::get('api/:version/product/recent', 'api/:version.Product/getRecent');

//Category
Route::get('api/:version/category', 'api/:version.Category/getCategories'); 
Route::get('api/:version/category/all', 'api/:version.Category/getAllCategories');

//Token
Route::post('api/:version/token/user', 'api/:version.Token/getToken');

Route::post('api/:version/token/app', 'api/:version.Token/getAppToken');
Route::post('api/:version/token/verify', 'api/:version.Token/verifyToken');

//Address
Route::post('api/:version/address', 'api/:version.Address/createOrUpdateAddress');
Route::get('api/:version/address', 'api/:version.Address/getUserAddress');

//Order
Route::post('api/:version/order', 'api/:version.Order/placeOrder');
Route::get('api/:version/order/:id', 'api/:version.Order/getDetail',[], ['id'=>'\d+']);
Route::put('api/:version/order/delivery', 'api/:version.Order/delivery');

//不想把所有查询都写在一起，所以增加by_user，很好的REST与RESTFul的区别
Route::get('api/:version/order/by_user', 'api/:version.Order/getSummaryByUser');
Route::get('api/:version/order/paginate', 'api/:version.Order/getSummary');

//Pay
Route::post('api/:version/pay/pre_order', 'api/:version.Pay/getPreOrder');
Route::post('api/:version/pay/notify', 'api/:version.Pay/receiveNotify');
Route::post('api/:version/pay/re_notify', 'api/:version.Pay/redirectNotify');
Route::post('api/:version/pay/concurrency', 'api/:version.Pay/notifyConcurrency');

//Message
Route::post('api/:version/message/delivery', 'api/:version.Message/sendDeliveryMsg');
~~~

# 目录结构
~~~
+---api
|   |   common.php
|   |   config.php
|   |   
|   +---controller
|   |   |   BaseController.php
|   |   |   
|   |   \---v1
|   |           Address.php
|   |           Banner.php
|   |           Category.php
|   |           Miss.php
|   |           Order.php
|   |           Pay.php
|   |           Product.php
|   |           Sample.php
|   |           Theme.php
|   |           Token.php
|   |           
|   +---model
|   |       Auth.php
|   |       Banner.php
|   |       BannerItem.php
|   |       BaseModel.php
|   |       Category.php
|   |       Image.php
|   |       Order.php
|   |       OrderProduct.php
|   |       Product.php
|   |       ProductImage.php
|   |       ProductProperty.php
|   |       Sample.php
|   |       Theme.php
|   |       ThirdApp.php
|   |       User.php
|   |       UserAddress.php
|   |       
|   +---service
|   |       AccessToken.php
|   |       AppToken.php
|   |       Banner.php
|   |       DeliveryMessage.php
|   |       Image.php
|   |       Order.php
|   |       Pay.php
|   |       Sample.php
|   |       Token.php
|   |       UserToken.php
|   |       WxMessage.php
|   |       WxNotify.php
|   |       
|   \---validate
|           AddressNew.php
|           AppTokenGet.php
|           BaseValidate.php
|           Count.php
|           IDCollection.php
|           IDMustBePositiveInt.php
|           IsValidUserToken.php
|           OrderPlace.php
|           PagingParameter.php
|           PreOrder.php
|           SampleGet.php
|           ThemeProduct.php
|           TokenGet.php
|           
+---extra
|       queue.php
|       secure.php
|       setting.php
|       wx.php
|               
+---lib
|   +---enum
|   |       OrderStatusEnum.php
|   |       ScopeEnum.php
|   |       
|   \---exception
|           BaseException.php
|           CategoryException.php
|           ExceptionHandler.php
|           ForbiddenException.php
|           MissException.php
|           OrderException.php
|           ParameterException.php
|           ProductException.php
|           SuccessMessage.php
|           ThemeException.php
|           TokenException.php
|           UserException.php
|           WeChatException.php       
~~~
