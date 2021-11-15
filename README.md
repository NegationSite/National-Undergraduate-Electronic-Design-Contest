# 三端口DC-DC变换器

本仓库为本人对于2021年全国电子设计大赛参赛的经历以及我们组对于[(C题)三端口DC-DC变换器](2021年C题.docx)（2021年电赛全部试题请点击文末的链接）设计的方案。水平有限，仅限参考！文末附有本文提到的某些相关资料的链接。

## 第一部分：参赛经历

这个部分只是我的一些七七八八八的主观感受和一些流水账，凌乱而又杂碎。

### 写在最前面的话

本人只是来自湖南的一个2019级普普通通的电子信息工程专业的在读生，所处的学校不是985也不是211，它很普通。我这个专业也不是学校的强势专业，学院的经费也很有限。但幸运的是，我的两个队友都很强，我是被带飞的那个人，我个人的水平只是同届参赛队伍所有队员中处于中下游水平。如果是我的两个队友来做这个仓库，他们一定能够做的更好。只不过是恰好因为我比较菜，所以有空余时间做一下这点微不足道的事情。

### 正式比赛之前

实打实算，我大概今年7月才算正确的跨入电赛的大门。之前确实学校组织过校赛或者其他之类的，但是都只能够算是小打小闹。我们小组是在7月初才成立的。之后便一直以小组的形式参加学校的集训。当时参加校赛选拔时，我们仨分别属于三个不同的队伍，在当时看来，我们只是为了获得一个参赛资格而配凑在一起。但是我们的羁绊越来越深，他们两个对我很包容，我很感激他们俩！在参加今年的比赛之前，我们参赛实属艰辛。本来以为比赛会在8月4日如期举办。但是7月底8月初，湖南疫情突然有点点失控，有传言是电赛延迟一周举办。但是当时长沙的几个学校立马就疏散留校的学生，紧急让他们回家，我们学校的负责人则是在等有关的通知，关于疏散留校学生的通知、电赛如期举行或者是电赛延期举行的通知。我也不知道他在等哪个，但是他就是在等通知。等到有具体的通知（电赛延期，延期时间确定在9月14日往后）时，已经是8月2号。在当时看来，湖南的疫情是比较严重的，学校已经无法让所有留校的同学离校了，会存在安全隐患。一鼓作气，再而衰，三而竭。我8月份的训练是基本没有进步。9月开学，学院搬迁到了新校区，实验室也只能是搬家。搬家，带来了新的环境，外加上缺乏状态，确确实实影响挺大。在正式比赛之前的两三天，实验室几乎处于没有人的状态（参赛人员中有许多的2018级的同学，他们还要同时准备考研）。

### 关于学校暑期的集训

我现在感觉我们的运气还是可以的，在暑假的时候，我们组只训练的几个题目，但是基本都包括完了今年C题所需要的所有模块。最初，我们小组做了一个简单的单相逆变电路进行练手，其具体的相关参数已经找不到了。在制作的过程中，解决了交直流电路电压电流检测、辅助电源、BUCK、BOOST、IR2104和光耦结合的MOS管驱动电路……等等相关问题。之后我们就开始制作单相APF([2013年电子设计大赛](2013全国电子设计大赛题目.pdf)中的A题)，但是做了半个月，尝试过纯硬件方法（芯片UCC28019）的方法，也尝试过其他方法，但是最终没有达到设计要求。然后就开始做了一部分[2015年电赛试题](2015全国电子设计大赛题目.pdf)中的A题，但是只做了一点点，然后2021年电赛试题的材料清单就出来了。

## 2021年电子设计大赛C题的相关分析

### 关于2021年电赛的[材料清单](2021电赛器材清单.pdf)

首先一个可以肯定的是，最终的题目与最初的题目是存在差异的。大概是因为疫情耽误了很长的一段时间，所以导致最终的题应该是出现了修改题目的现象（可以从材料清单中出现了亚克力球但是最终却是没有和亚克力球相关的题目来推断）。这个部分的相关推测是针对为改变之前。
材料清单中这些元器件大概率是与电力电子方向题目有关的：

1. 自带管理功能2000～3000mAh 18650型锂离子电池四节及相应电池盒
2. 大功率电阻（10Ω/200W,50Ω/30W）
3. 小容量三相自耦调压器三相隔离变压器（300VA，1:1）

关于这三个元器件分析如下：

1. 一节锂电池正常电压约为4伏左右，四节锂电池则是16伏。18650型号电池的最大电流约为4A.同时可以推测的是，出现了锂电池意味着题目中会存在电池的充放电模块。
2. 200W的10欧电阻，大约可承受电压为44.7伏，可承受电流为4.5A；30W的50欧电阻大约可承受电压为38V，可承受电流为0.77A.

所以最终的题目可能与[2017年电子设计大赛](2017年大学生子电子设计竞赛题目(A-P题全)附元器件清单.pdf)A题类似，出一个模拟微电网的相关题目，同时在结合如今出题的趋势（新能源），所以猜测题目可能为一个风力发电模拟并网系统的装置，总的拓扑大概为AC-DC-AC，其中DC还要再加上和电池充放电结构（风力发电出来的电为三相电，对其进行整流，期间就可以加入10欧的电阻，然后再进行三相逆变并入电网，电网接入三相负载——三个50欧姆的电阻，Y连接。其中，当线电压比较小时（模拟风力发电电压比较小时）则弃风——即此时只采用电池进行供电；当线电压处于某一个范围时，电池和三相电源同时给最后的负载供电；线电压再升高，采用三相电源供电，电池处于充电状态）。

### 审题[（2021年电子设计大赛C题）](2021年C题.docx)

如果只看基本要求部分，其实是无法根据$U_S$确定$U_I$的。这样的话就会有很多种拓扑结构的选择。但是如果看完发挥部分的要求，那么就能发现，如果发挥部分能够完成的话，那么就一定存在
$$ \mathbf{U}_S=\frac{\mathbf{U}_I}{2} $$
同时，在这个等式成立的情况下，那么也就完成了最大功率点跟踪。所以对于此时 $U_I$的取值为12.5V~27.5V之间。如果仅想要实现基本部分的话，那么就可以采用比较简单的拓扑结构，同时也会降低控制难度。

### 主要拓扑结构

我们小组直接在模拟光伏电池之后接[BOOST变换器](http://www.elecfans.com/analog/20171102574041.html)，并配合STM32F4将其后端输出电压恒定在30V。对于电池充放电，我们采用了[双向DC-DC充放电电路](http://www.elecfans.com/yuanqijian/dianrongqi/20171202591513_3.html)。同时，为了更好的满足基本要求中的效率指标，我们将双向DC-DC充放电电路选择放在了BOOST电路的前端，即直接与$U_I$相连接。[BOOOST](BOOST变换器.png)和[DC-DC变换器](双向DC-DC变换器.png)连接方式仅供参考。

### 辅助电源

对于辅助电源，我们采用了金升阳电源砖中URB2405YMD-10WR3和URB2412YMD-10WR3两个版本。其连接方式可以参考[用户手册](金升阳电源砖.PDF)。相较于由其他的装置制成的辅源，电源砖无疑更加省心一些。

### [电压电流检测](电压电流检测.png)

对于实现自动控制，那么就需要进行电压电流检测。与常规而言，电流检测一般在低端，但是我们在实际的电路当中，由于接地的问题，使得对于$U_I$的检测采用低端电流进行检测总是不准确，所以对于$U_I$的检测我们最后放在了高端。  
我们电压电流检测均采用差分放大电路，电流通过一个采样电阻样转化为电压后输入运放进行放大，电压直接则是直接输入运放进行缩小。

### [MOS管驱动电路](MOS管驱动.png)

对于MOS管的驱动，我们采用IR2104，其输入一路PWM信号可以转化为两路互补PWM信号从而对两MOS管同时控制使其能交替导通。但是在使用过程中发现，如果使用IR2104直接连接单片机的话，常常因为MOS管烧坏引起IR2104烧坏，从而导致烧坏单片机。所以我们在IR2104与单片机之间通过一个TLP250光耦进行隔离可以有效的对单片机进行保护。同样的，诸如缓冲器74HC245等也能起到保护作用。

### 最大功率点跟踪的实现

目前，最大功率点跟踪（Maximum Power Point Tracking，简称 MPPT）的方法有很多，如恒定电压控制法，扰动观测法，导纳增量法，模糊控制法……但不同的方法在实际的使用中存在不同的优缺点.

1. 恒定电压控制法（CVT）。当整个电路系统确定的情况下，模拟光伏电池的最大功率电压为一个恒定的值。因此控制模拟光伏电池输出电压检Ui控制在Us/2处，此时模拟光伏电池在整个工作过程中将近似工作在最大功率点处。
2. 扰动观测法( P&O) 。通过扰动模拟光伏电池的输出电压，判断扰动前后系统输出功率的变化情况，并按照使输出功率增加的原则来对系统进行控制。
3. 导纳增量法(IncCond) 。根据电路知识可知，在最大功率点处有$\frac{\rm dP}{\rm dU} = 0 $ ，通过简单的数学推导可以得出在最大功率点处有下式成立：$\frac{\rm dI}{\rm dU} = \frac{I}{U}$.因此，将该式作为判定光伏电池是否工作在最大功率点的依据，并对系统进行相应的控制，即可以实现对最大功率点的跟踪。

关于实现最大功率点跟踪的方法还有很多种以及各种改进。但是很多方案在电赛的短短四天三晚的时间里面无法实现，所以我们小组只能选择一个较为简单的方式去进行控制，这也导致了我们的最终效果其实并不理想。具体的最大功率点跟踪方案请参考相关论文。
相关的论文：[几种光伏系统 MPPT 方法的分析比较及改进](https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CJFD&dbname=CJFD2007&filename=DLDZ200705001&uniplatform=NZKPT&v=ndG04dNQ4IB2BXtqVhJDjdtiktz7IKgJVPT-1DynU24uyqaxw1huS4L0oKLHgF_T)；[基于改进电导增量法的光伏MPPT控制](https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CJFD&dbname=CJFDLAST2021&filename=XBDJ202109008&uniplatform=NZKPT&v=Is2N8VyAT6BkXoAIJiStBTJwWZPgwUxfGJ8AQkMAMvQ2WkwZNbvYGPrlSDIF8QmZ)。

## 相关资料合集

[三端口DC-DC变换器（C题)](2021年C题.docx)  
[2021年全国电子设计大赛赛题](2021竞赛题目（本科）.zip)  
[2021年全国电子设计大赛器材清单](2021电赛器材清单.pdf)  

[2013年全国电子设计大赛赛题全集](2013全国电子设计大赛题目.pdf)  
[2015年全国电子设计大赛赛题全集](2015全国电子设计大赛题目.pdf)  

[BOOST变换器相关资料](http://www.elecfans.com/analog/20171102574041.html)  
[双向DC-DC充放电电路相关资料](http://www.elecfans.com/yuanqijian/dianrongqi/20171202591513_3.html)

[BOOOST变换器](BOOST变换器.png)  
[DC-DC变换器](双向DC-DC变换器.png)  
[MOS管驱动电路](MOS管驱动.png)  
[电压电流检测](电压电流检测.png)  

[几种光伏系统 MPPT 方法的分析比较及改进](https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CJFD&dbname=CJFD2007&filename=DLDZ200705001&uniplatform=NZKPT&v=ndG04dNQ4IB2BXtqVhJDjdtiktz7IKgJVPT-1DynU24uyqaxw1huS4L0oKLHgF_T)
[基于改进电导增量法的光伏MPPT控制](https://kns.cnki.net/kcms/detail/detail.aspx?dbcode=CJFD&dbname=CJFDLAST2021&filename=XBDJ202109008&uniplatform=NZKPT&v=Is2N8VyAT6BkXoAIJiStBTJwWZPgwUxfGJ8AQkMAMvQ2WkwZNbvYGPrlSDIF8QmZ)
