# python编程规范

python 封库编程规范

## 索引

* [文件结构与命名](#文件结构与命名)
* [类与注释](#类与注释)
* [常量命名](#常量命名)
* [变量命名](#变量命名)
* [函数命名与注释](#函数命名与注释)
* [高质量封库细节](#高质量封库细节)

## 文件结构与命名

库可以直接放在 Arduino 封库的根目录下，将 python 直接命名为python <br>
 <br>
文档结构应类似如下: <br>
<pre>

--python:
| --raspberrypi:
| | --DFRobot_Module.py
| | --Modele_demo_xxxx.py
| | ......
|
| --esp32:
| | --DFRobot_Module.py
| | --Modele_demo_xxxx.py
| | ......
| |
</pre>

例程文件头部注释写法：<br>

<pre>
""" file 文件名（不能使用中文）
  #
  # 如何做这个实验，描述实验步骤（只需要下载程序就能肉眼观测到的简单小实验例如blink，这步可以不写）（不能使用中文）
  # 实验现象是什么（不能使用中文）
  #
  # Copyright   [DFRobot](http://www.dfrobot.com), 2016
  # Copyright   GNU Lesser General Public License
  #
  # version  V1.0
  # date  2017-10-9
"""
</pre>

## 类与注释

类名应当以 DFRobot_ 作为开头, 模组型号作为结尾。<br>
在构造函数中说明参数:

```py
class DFRobot_Module:

  def __init__(i2cAddr):
    """ Class constructor

    :param i2cAddr:int Module's i2c address
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
  eModuleConfEnum2
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

受保护的变量（对应 cpp 里的 protected ）名前需要加 _, 私有的变量（对应 cpp 里的 private ）名前需要加 __ <br>
任何类型的变量和函数名都使用下划线命名规则 <br>

例：
```py
class DFRobot_Module:

  _protect_var = 1  # 受保护的变量
  _protect_list = [0, 1]  # 变量注释
  _protect_dict = {
    "a": 1
  }

  __private_var = 1  # 私有的变量
  __private_list = [0, 1]  # 变量注释
  __private_dict = {
    "a": 1
  }

  public_var = 1  # 公有变量
  public_list = [0, 1]
  public_dict = {
    "a": 1
  }

```

## 函数命名与注释

受保护的函数（对应 cpp 里的 protected ）名前需要加 _, 私有的函数（对应 cpp 里的 private ）名前需要加 __ <br>
函数名使用下划线命名规则 <br>

示例：
```py
class DFRobot_Module:

  def __init__(self, param1):
    """ Module init

    :param param1:int Set to ...
    """
    pass

  def _private_func(self, param1):
    """ func detail

    :param param1:int Set to ...
    """
    pass

  def public_func(self, param1):
    """ Check param1

    :param param1:int Parameter to check

    :return:bool Check result
      :retval True Check succeed
      :retval False Check falied
    """
    if param1:
      return True
    else:
      return False

  POWER_ON = 0x00
  POWER_OFF = 0x01

  def public_func2(self):
    """ Return power status

    :return Power status
    """
    return self._powerStatus

```

## 高质量封库细节

参考 Arduino 高质量封库细节，python 无法完成的项目不用理会 <br>

https://github.com/forKnowYou/program-standard-cpp
