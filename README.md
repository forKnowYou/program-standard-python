# python编程规范

python 封库编程规范

## 索引

* [文件结构与命名](#文件结构与命名)
* [类与注释](#类与注释)
* [常量命名](#常量命名)
* [变量命名](#变量命名)
* [函数命名与注释](#函数命名与注释)

## 文件结构与命名

库可以直接放在 Arduino 封库的根目录下，将 python 库的文档结构命名为 raspberry | micropython <br>
 <br>
文档结构应类似如下: <br>
<pre>

--raspberry:
|   lib.py
|   xx.py
|   ...
|   --examples:
|   |   module_func.py
|   |   ...
</pre>

## 类与注释

类名应当以 DFRobot_ 作为开头, 模组型号作为结尾。<br>
在构造函数中说明参数:

```py
class DFRobot_Module:

  def __init__(i2cAddr):
    """ Class constructor

    :param i2cAddr Module's i2c address
    """
    pass

```

## 常量命名

C 库中的宏，包括枚举变量在 python 中需要写在类的全局变量中，并所有字母大写

C 库中的定义：
```cpp
#define MODULE_CONF   0x00

typedef enum {
  eModuleConfEnum1,
  eModuleCOnfEnum2
} eModuleConf_t;
```

对应 python 中的定义：
```py
class DFRobot_Module:

  CONF = 0x00

  CONF_ENUM1 = 0x00
  CONF_ENUM2 = 0x01

```

## 变量命名

私有变量名前需要加 _ <br>
变量遵循驼峰命名法 <br>
列表变量需要在变量名前加 l，后面的字母首字母大写并遵循驼峰命名法 <br>
元祖变量全部用列表变量表示 <br>
字典变量需要在变量名前加 d，后面的字母首字母大写并遵循驼峰命名法 <br>

例：
```py
class DFRobot_Module:

  _privateVar = 1  # 私有变量
  _lPrivateList = [0, 1]
  _dPrivateDict = {
    "a": 1
  }

  publicVar = 1  # 公有变量
  lPublicList = [0, 1]
  dPublicDict = {
    "a": 1
  }

```

## 函数命名与注释

私有函数名前需要加 _ <br>
函数名遵循驼峰命名法 <br>

示例：
```py
class DFRobot_Module:

  def __init__(self, param1):
    """ Module init

    :param param1 Set to ...
    """
    pass

  def _privateFunc(self, param1):
    pass

  def publickFunc(self, param1):
    """ Check param1

    :param param1 Parameter to check

    :return Check result
      :retval True Check succeed
      :retval False Check falied
    """
    if param1:
      return True
    else:
      return False

  POWER_ON = 0x00
  POWER_OFF = 0x01

  def publicFunc2(self):
    """ Return power status

    :return Power status
    """
    return self._powerStatus

```
