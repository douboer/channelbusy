
## awk version of wifi network channel busy analysis for H3C hardware
-- Chengan douboer@gmail.com

## 信道利用率解析工具使用方法

#### 工具作用：
1.	自动生成采集脚本，避免手工编辑脚本出错问题。
2.	自动解析从AC采集到的AP的信道繁忙率的原始log，并把繁忙率数据与热点及AP匹配。

#### 使用该工具用户需要做什么：
1.	采集AC下的热点及AP的信息表（一个AC一张表）；可以从网管导出设备表，对需要采集的AP进行筛选得到。该表放置在AClist文件夹下，文件名中需包含AC的IP地址（不包含AC IP地址的将被忽略）。
2.	登陆到AC，执行createscript工具自动生成的脚本，执行结果保存log文件；log文件名需包含AC的IP地址（不包含AC IP地址的将被忽略）；文件可以放置在任何文件夹下。

#### 使用步骤：
1.	整理采集AC信息表，放到AClist目录下，格式见下文
2.	运行createscript.bat，在scripts目录下生成脚本文件
3.	telnet到相应AC，把脚本贴进去运行；运行输出保存为log文件，放到文件夹内
4.	运行channelbusyabstract.bat，结果生成在outputs目录。

#### 说明：
1.	AC采集下来的文件放在多个文件夹下，请修改channelbusyabstract.bat，红字部分修改为文件夹名字
@awk -f channelbusyabstract.awk 5月25号（衢州-样例）
2.	AC信息表为CSV格式（逗号分隔的文本），格式如下：
#城市名称	区县	分局	热点名称	厂家	型号	AP编号	设备名称	IP地址
衢州	衢州市区	柯城分局	衢州学院4#宿舍楼	H3C	WA1208E-GP-H20-T	qz_xyss4h_1fap1	4号宿舍楼1FAP1	10.20.152.194
3.	标识为样例的文件，使用时可删除


#### 附：
1.	目录结构
├-信道利用率（主目录，任意文件名）
│  │  abstractchannelbusy.bat
│  │  AC-10.20.145.55_channelbusy12点-23点.txt
│  │  awk.exe
│  │  channelbusyabstract.awk
│  │  channelbusyabstract.infn.awk
│  │  createscript.awk
│  │  createscript.bat
│  │  channelbusyabstract.bat
│  │  debug
│  │  logfn.txt
│  │  信道利用率读取方法.docx
│  │  工具使用方法.docx
│  │  
│  ├-5月25号衢州（样例）
│  │      AC-10.20.145.55_channelbusy12点-23点（样例）.txt
│  │      …………
│  ├-AClist（放置需要采集信道利用率的AC信息，文件格式见说明）
│  │      AC-10.20.145.55（样例）.CSV
│  │      …………
│  ├-outputs（放置输出文件，文件通过channelbusyabstract自动生成）
│  │      5月25号（衢州-样例）_channelbusy.csv
│  │      …………
│  └-scripts（放置AC脚本，脚本通过createscript自动生成）
│          script_AC-10.20.145.55（样例）.txt

2.	信道利用率脚本说明

