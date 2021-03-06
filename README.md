# PyCINRAD
CINRAD data reader.

A python class which can be used to read CINRAD SA/SB/CB files and plot graphs including PPI and RHI.

读取CINRAD雷达基数据的Python脚本，目前支持SA/SB/CB三种雷达数据格式（部分支持CC雷达），具体函数用法请看脚本注释。
该脚本目前还在继续开发中，欢迎提Issue/发PR^_^


### 用法
```
from CINRAD_radar import *
file = 'Z_RADR_I_Z9576_20180629043900_O_DOR_SA_CAP.bin'
radar = Radar(file)
```
由于SA/SB/CB雷达文件里并未记录站号，程序会尝试从文件名里提取站号然后寻找到对应的地理信息，形如 Z_RADR_I_Z9576_20180629043900_O_DOR_SA_CAP.bin 和 RADA_CHN_DOR_L2_O-Z9558-SA-CAP-20180725084700.bin 这两种形式的文件都是可以自动识别的。

如果程序没有读出站号，就会抛出警告:
```
Auto fill radar station info failed, use set_code and then _update_radarinfo manually instead.
```

这时候则需要手动设置站号，再更新雷达站的地理信息。
```
radar.set_code('Z9576')
radar._update_radar_info()
```

#### 绘制PPI
```
radar.draw_ppi(level, drange, datatype='r', smooth=True)
```
datatype目前支持 'r','v'和'et' 三种，对应反射率，速度和回波顶高。

当datatype='r'时，smooth参数可以对反射率进行平滑处理。


#### 绘制RHI
```
radar.draw_rhi(azimuth, drange)
```
传入方位角和距离即可绘制。

#### 绘制CINRAD/CC雷达反射率数据

由于本程序没有完全支持CC雷达，绘制CC雷达反射率的PPI的步骤稍有不同，需要先手动设置该仰角的度数再绘制。

```
radar = Radar('2018072615.12V', radartype='CC')
radar.set_elevation_angle(0.5)
radar.draw_ppi(0, 230, datatype='r')
```

PS:如在使用该脚本中有任何问题和建议，可以发邮件给我 274555447@qq.com
