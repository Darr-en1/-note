## Serialization

### Serializer
序列化model中的对象

### ModelSerializer
通过model作映射，关联model中对象.
<br>

## view 
from Django class

### APIView 
from drf extends view<br>
提供REST framework的Request对象和Response对象。<br>
在进行dispatch()分发前，会对请求进行身份认证、权限检查、流量控制。<br>

### GenericAPIView
from drf extends APIView<br>
搭配一个或多个Mixin扩展类,增加了对于列表视图和详情视图可能用到的通用支持方法.

#### 五大扩展类

##### 1）ListModelMixin
列表视图扩展类，提供list(request, *args, **kwargs)方法快速实现列表视图，返回200状态码。

##### 2）CreateModelMixin
创建视图扩展类，提供create(request, *args, **kwargs)方法快速实现创建资源的视图，成功返回201状态码。
如果序列化器对前端发送的数据验证失败，返回400错误。

##### 3） RetrieveModelMixin
详情视图扩展类，提供retrieve(request, *args, **kwargs)方法，可以快速实现返回一个存在的数据对象。
如果存在，返回200， 否则返回404。

##### 4）UpdateModelMixin
更新视图扩展类，提供update(request, *args, **kwargs)方法，可以快速实现更新一个存在的数据对象。
同时也提供partial_update(request, *args, **kwargs)方法，可以实现局部更新。
成功返回200，序列化器校验数据失败时，返回400错误。

##### 5）DestroyModelMixin
删除视图扩展类，提供destroy(request, *args, **kwargs)方法，可以快速实现删除一个存在的数据对象。
成功返回204，不存在返回404

### viewSets  Router
viewsSets完成状态建模和API交互，把URL的创建过程依照通用的规范留给框架自动去完成。将视图集注册到Router

