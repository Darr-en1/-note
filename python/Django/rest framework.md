## Serialization

### Serializer
序列化model中的对象

### ModelSerializer
通过model作映射，关联model中对象.
<br>

### Serializer的嵌套，包含
#### example
request post请求json数据格式
```python
{
    'device_label': "device01",
    'cabinet': 10,
    "description": "description01",
    "temperatures":[
        {
            "record_datetime": "2018_08_10_19_25_40",
            "temperature": 31.56
        },
        {
            "record_datetime": "2018_08_10_19_25_51",
            "temperature": 24.23
        }
    ]
}
```
model.py
```python
class DeviceTemperature(models.Model):
    class Meta:
        permissions = (
            ("view_devicetemperature", "Can view device temperature"),
        )

    device = models.ForeignKey(Device, on_delete=models.CASCADE)
    cabinet = models.ForeignKey(Cabinet, on_delete=models.CASCADE)
    description = models.CharField(max_length=50)
    record_datetime = models.DateTimeField(default=timezone.now)
    temperature = models.DecimalField(max_digits=5, decimal_places=2)
```
serializer.py
```python
class DeviceTemperatureSerializer(serializers.ModelSerializer):
    record_datetime = serializers.DateTimeField(
        input_formats=['%Y_%m_%d_%H_%M_%S']
    )
    class Meta:
        model = DeviceTemperature
        fields = (
            'record_datetime',
            'temperature'
        )
        
class CreateDeviceTempSerializer(serializers.Serializer):
    device_label = serializers.SlugRelatedField(
        queryset=Device.objects.all(),
        slug_field='device_label'
    )
    cabinet = serializers.PrimaryKeyRelatedField(
        queryset=Cabinet.objects.all()
    )
    description = serializers.CharField(max_length=50)
    temperatures = DeviceTemperatureSerializer(many=True)
```



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
