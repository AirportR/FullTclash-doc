---
description: 绘图相关配置
---

# image

### title

绘图标题，默认值为 'FullTclash'。

> 示例：
>
> ```yaml
> image:
>  title: "FullTclash"
> ```

### color

绘图的相关颜色配置，以下示例均为默认值。

> 示例：
>
> ```yaml
> image:
>  title: 'FullTclash' # 绘图时的标题
>  #以下是颜色配置，其中speed是速度相关,name为颜色名字，value为颜色值，目前仅支持十六进制，label是颜色对应的速度区间（单位MB）,不用动，只需改value值，其他项是为了做区分。
>  color:
>   speed: # 刚刚好有七个颜色，多一个少一个可能会有奇怪的效果。注意缩进。如果不想有太多颜色，可以两个颜色取同样的颜色值。
>    - { label: 0, name: '云水', value: '#B4C3D0', alpha: 255 }
>    - { label: 1, name: '晴山', value: '#91AEC4', alpha: 255 }
>    - { label: 5, name: '秋波', value: '#8BB8CB', alpha: 255 }
>    - { label: 10, name: '天韵', value: '#5796B3', alpha: 255 }
>    - { label: 20, name: '鸢尾', value: '#1988AE', alpha: 255 }
>    - { label: 60, name: '甸子', value: '#238BBC', alpha: 255 }
>    - { label: 100, name: '景泰', value: '#2A73AC', alpha: 255 }
>   delay: #延迟单位: ms
>    - { label: 1, name: '云水', value: '#B4C3D0', alpha: 255 }
>    - { label: 100, name: '晴山', value: '#91AEC4', alpha: 255 }
>    - { label: 200, name: '秋波', value: '#8BB8CB', alpha: 255 }
>    - { label: 300, name: '天韵', value: '#5796B3', alpha: 255 }
>    - { label: 500, name: '鸢尾', value: '#1988AE', alpha: 255 }
>    - { label: 1000, name: '甸子', value: '#238BBC', alpha: 255 }
>    - { label: 2000, name: '景泰', value: '#2A73AC', alpha: 255 }
>    - { label: 99999, name: '景泰', value: '#8d8b8e', alpha: 255 }  #第八个为超时，label无用
>   "yes": '#bee47e' #解锁色块的颜色，注意不要去掉双引号
>   "yesalpha": 255 #解锁颜色块透明度
>   "no": '#ee6b73' #失败色块的颜色，注意不要去掉双引号
>   "noalpha": 255 #失败颜色块透明度
>   na: '#8d8b8e' #N/A色块的颜色
>   naalpha: 255  #N/A颜色块透明度
>   wait: '#dcc7e1' #待解锁色块的颜色
>   waitalpha: 255  #待解锁色块的颜色
>   iprisk: #IP风险色块颜色,名称后面加alpha为颜色块透明度属性
>    low: '#ffffff'
>    lowalpha: 255
>    medium: '#ffffff'
>    mediumalpha: 255
>    high: '#ffffff'
>    highalpha: 255
>    veryhigh: '#ffffff'
>    veryhighalpha: 255
>   warn: '#fcc43c' #警告色块，一般为黄色或橙色
>   warnalpha: 255  #警告颜色块透明度
> ```

#### watermark

水印设置

> 示例：
>
> ```yaml
> image:
>  watermark:
>   enable: true #是否启用
>   text: '只是一个水印' #水印文本
>   color: '#000000' #颜色值
>   alpha: 16 # 透明度, 可用范围(0-255)
>   font_size: 64 #字体大小
>   angle: -16.0 #旋转角度
>   row_spacing: 0 #行距
>   start_y: 0 #纵坐标起始位置
> ```

#### background

绘图的背景颜色配置

> 示例：
>
> ```yaml
> image:
>  background:
>   backgrounds: '#ffffff' #联通性测试内容背景色
>   ins: '#ffffff' #拓扑测试入口内容背景色
>   outs: '#ffffff' #拓扑测试出口内容背景色
>   speedtest: '#ffffff' #速度测试内容背景色
>   speedtitle: '#EAEAEA' #速度测试标题栏颜色
>   testtitle: '#EAEAEA' #联通性测试标题栏颜色
>   topotitle: '#EAEAEA' #拓扑测试标题栏颜色
> ```
