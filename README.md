Notes from DearJohn-2
=====
<a href="https://dearjohnsonny.github.io/Notes-from-DearJohn/">Notes from DearJohn</a>

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187057747-7cb5e02e-5596-4bc4-a9b4-219cb731ee6c.png" width="1500">
</div>


## 基于*CRISPR*的基因编辑
基于CRISPR的基因编辑方式主要有四种，包括：**nucleases(核酸酶), base editors(碱基编辑器)**, transposases/recombinases(转座子/重组酶类) and prime editors(引物编辑器).

Homology-directed repair (HDR); cytosine base editor (CBE); adenine base editor (ABE); end-joining (EJ); prime editor (PE); uracil glycosylase inhibitor (UGI); **protospacer adjacent motif (PAM)**.

![1](https://user-images.githubusercontent.com/111955215/187057959-382192c9-397a-4806-9f42-76560272313f.png)

### 通过CRISPR–Cas核酸酶来实现基因编辑
家族Ⅰ用多种蛋白质进行核酸的切割，而家族Ⅱ用一种蛋白质进行切割（下图还应该补充下，classⅡ中还有typeⅣ，如Cas-13）

![image](https://user-images.githubusercontent.com/111955215/187058140-b2c8f4a8-70f9-4476-a906-cbe32609aa85.png)
#### Cas9家族
Cas9在protospacer序列上产生切割，大约在PAM前3bp的位置，且会用Cas9上两个不同的结构域（RuvC and HNH）进行切割产生非粘性末端。目前使用最广泛的 CRISPR-Cas 核酸酶 SpCas9含有1,368个氨基酸，识别相对常见的 NGG PAM，可以与 sgRNA 或 crRNA/tracrRNA 对一起使用，与20-nt 间隔物最佳地起作用，具有强大的 DNA 靶向和切割活性，并支持相对高水平的脱靶编辑

![image](https://user-images.githubusercontent.com/111955215/187072763-d23e58d2-bbbd-4ebd-9e5c-5eb508856bb0.png)

几种Cas9家族的结构域

![image](https://user-images.githubusercontent.com/111955215/187073720-dd142f67-b156-4ad3-b898-9a3874fad9c3.png)

#### Cas12家族
Cas12在远离PAM序列的位置产生切割，且只有RuvC进行切割，导向核酸也是crRNA而不是gRNA；Cas12核酸酶通常产生交错切割，这与Cas9的blunt切割不同。**Cas12a**通常使用富含T的PAM，这与大多数 Cas9的PAM不同。一般而言，Cas12a 变异体已被报道与许多 Cas9直系同源物相比产生少量脱靶编辑事件。

#### 修复方法
* 修复方法有两种：**非同源末端连接**（Non-homologous End Joining, **NHEJ**)和**同源引导修复**homology-directed repair(**HDR**)；
* 非同源末端连接又分为经典非同源末端连接(classical nonhomologous end-joining, **c-NHEJ**)和微同源末端连接(microhomology-mediated end-joining, **MMEJ or alt-NHEJ**)
* 同源引导修复又分为单链寡核苷酸供体（single-stranded oligonucleotide donors, ssODNs）和双链DNA供体

![image](https://user-images.githubusercontent.com/111955215/187058510-3ce609ca-8e92-44a2-a1b4-3ae0f0271c15.png)

#### 其他相关
高浓度的dsDNA容易产生毒性，而ssODN会好很多。
**以RNP复合物形式递送 CRISPR-Cas 系统通常导致更低水平的脱靶修饰（如下图）**

* 电转的方式将RNP和dsDNA一起递送

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187063342-9f486748-b1b0-45c3-85d4-7b4384a25ed2.png" width="900">
</div>

* 在RNP上修饰一个NLS（细胞核定向序列），帮助定向到细胞核中

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187063236-27eb9bbf-f091-4b78-a684-87cb053f21bb.png" width="900">
</div>

* 单链的HDR毒性更低，因此可以采用这个思路：两端是dsDNA从而带有CTS（Cas9 targeted sequence）
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187073916-7561faa5-642f-4217-be03-089a053ea6cb.png" width="500">
</div>

### 通过Cas相关的碱基编辑器来实现基因编辑
* 碱基编辑器精确地导致靶点突变，而不需要 DSB 或供体 DNA 模板，也不依赖 HDR。
* 目前的碱基编辑器包含与单链 DNA 脱氨酶融合的几乎丧失催化能力的CRISPR-Cas核酸酶(不能制造DSB) ，在某些情况下还会与能修复DNA的蛋白机器融合。
* 迄今为止已经开发了两类主要的碱基编辑器: 胞嘧啶碱基编辑器(CBE) ，其催化C•G碱基对转化为T•A碱基对；和腺嘌呤碱基编辑器(ABEs)，其催化A•T到G•C转化。CBE 和 ABE 可以有效地介导所有四种可能的转换突变(C → T，A → G，T → C，G → A) ，这些突变约占目前注释的人类致病变体的30%
* 在CBE和ABE中，催化受损的Cas核酸酶结构域将ssDNA脱氨酶定位到感兴趣的基因组靶序列。在Cas结合后，引导RNA间隔区与目标DNA链的杂交导致含有PAM的基因组DNA链的位移以形成ssDNA的R环。PAM远端核苷酸暴露为ssDNA并且可以进入碱基编辑器的脱氨酶结构域。


#### CBE
CBE使用**胞苷脱氨酶**将R环内的胞嘧啶转化为尿嘧啶，聚合酶将其读作胸腺嘧啶。但是在实际使用时，这种突变有可能会被修复，这种突变出来的尿嘧啶会被尿嘧啶糖基化酶(uracil DNA N-glycosylase, UNG2)从基因组中切除掉，因此CBE往往会引入尿嘧啶糖基化酶抑制蛋白(UGI)以减少尿嘧啶的清除

![image](https://user-images.githubusercontent.com/111955215/187060191-7240f4b4-a781-489f-b955-36f3c5822089.png)
#### ABE
类似地，ABE使用实验室进化的 TadA**脱氧腺苷脱氨酶**将R环内的腺苷转化为肌苷，通过聚合酶将其读作鸟嘌呤。而肌苷清除的速率远低于尿嘧啶，所以不需要其他的修饰。

![image](https://user-images.githubusercontent.com/111955215/187060202-02d09a03-f312-4170-8a20-abf8eb9e324c.png)

#### 常见的碱基编辑器的序列

![image](https://user-images.githubusercontent.com/111955215/187112477-2167805c-ee39-41fa-9d54-0ce374340e1c.png)

#### 碱基编辑器的选择
碱基编辑器可以根据几个标准来选择，包括所需的编辑(C•G-to-T•A或A•T-to-G•C)，目标序列中合适的 PAM 的可用性，围绕目标核苷酸的序列基序，目标核苷酸在原型间隔区内的位置，不希望的旁观者突变的可能性以及需要尽量减少脱靶DNA或RNA编辑。该流程图可以指导候选基本编辑器的识别。根据应用程序的不同，一些标准将优先于其他标准，可能需要在效率和特定性之间进行权衡。SpCas9 CBE 的标准编辑窗口通常是原型间隔区位置4-8，对于SaCas9 CBE 是位置3-12，对于 Cas12a CBE 是位置8-13。SpCas9 ABEs 的标准编辑窗口通常是原型间隔区位置4-7，对于 SaCas9 ABEs 是位置6-12，对于 Cas12a ABEs 是位置8-13。

![image](https://user-images.githubusercontent.com/111955215/187060579-48a2284c-6ca5-4a66-87a0-bb3583a00b04.png)

#### Cas相关的转座酶
Tn7样转座子通常含有 tnsA、 tnsB、 tnsC、 tnsD 和 tnsE 基因，以及其他遗传货物。通常，TnsA 和 TnsB 形成特异性识别左端(LE)和右端(RE)基序的 TnsAB 复合物，其侧翼转座子并催化从供体基因座切除转座子。TnsB 是逆转录病毒整合酶超家族的成员，并催化磷酸二酯骨架的3’切割，而 FokI 样蛋白 TnsA 随后催化5’末端的切割。然后，TnsB 将转座子 DNA 的游离3’末端连接到由 TnsD 或 TnsE 底物分配结构域确定的靶 DNA 底物，在5’连接处留下小的间隙。这些缺口的修复导致特征性的5-bp 目标位点重复。TnsC 是一种与 TnsAB 复合物、双链 DNA 和 TnsD 或 TnsE 中的一种相互作用的 ATP 酶

Cas 转座酶包括 Cas 蛋白和转座酶相关组分。Cargo DNA 由其左端(LE)和右端(RE)序列鉴定，并与转座酶蛋白(Tns)结合。Cas 蛋白以 PAM 依赖的 RNA 定向方式定向到感兴趣的靶基因座。Cas 结合将转座酶蛋白定位到感兴趣的目标序列，并促进目标位点的Cargo DNA整合进入基因组。

![image](https://user-images.githubusercontent.com/111955215/187115301-543520ce-7ece-41d1-970d-21ebdd16aebd.png)

<div align=center>
<img src="ttps://user-images.githubusercontent.com/111955215/187116466-90df7aa1-947d-4001-9d59-d6bab6d435bc.png" width="1500">
</div>

## crispr工具的补充-迷你核酸酶IscB和TnpB
来自于IS200/605转座子家族的IscB和TnpB，它们在微生物中广泛分布，被认为是CRISPR/Cas9和Cas12系统的起源。它们的最大特点是非常短的CDS序列，在1.2kb左右，体积不到spCas9的1/3，留下了巨大的改造空间。
Zhang Feng将这个系统称为Ω系统。Ω系统与其他已知RNA引导的DNA靶向系统的比较（CRISPR系统通过捕获间隔序列并储存在CRISPR阵列基因座中，与CRISPR系统不同，Ω系统可以将它们的基因座转置到靶标序列中，将靶标转化为ωRNA guides）

![image](https://user-images.githubusercontent.com/111955215/187116932-8787573f-16eb-45bd-b258-4af059a1cc35.png)
### IscB
从蛋白结构预测分析中，我们能够看到IscB同样存在RuvC和HNH两个酶活性位点

![image](https://user-images.githubusercontent.com/111955215/187115991-0b0afac8-aa91-45a2-a963-198956b0399a.png)

借助RNA测序和RNA-pulldown等技术手段，研究者也找到了IscB对应的sgRNA，其结构比spCas9的sgRNA还要更加复杂，被作者称为ωRNA

![image](https://user-images.githubusercontent.com/111955215/187116044-606d96dc-9b4c-458f-a841-d0f3cbf10c83.png)

通过体外DNA切割实验，研究者发现IscB具备由ωRNA引导识别(下图)并切割特定DNA双链序列的能力，其PAM序列也被作者称为TAM(target-adjacent motif)。不同于spCas9的是，IscB的切口是粘性末端(下图)。

![image](https://user-images.githubusercontent.com/111955215/187117727-5e5e0dcb-de0c-4f8d-b36c-c30a5922ac74.png)

![image](https://user-images.githubusercontent.com/111955215/187117793-13a82a7d-7b79-4cf5-a156-6f24385789b8.png)

从目前的结果来看，部分IscB蛋白能够编辑人细胞的基因组序列，但编辑效率还明显低于spCas9，最高也只有2%左右。

SUM UP: IscB已经具备了很多spCas9的优点，比如有两个酶活性位点，分别负责一条DNA单链的切割；又比如ωRNA的结构较为复杂，便于进行改造。而IscB最大的优势还是其非常小的体积，为递送提供了极大的便利，同时也就腾出了巨大的改造空间。

### TnpB
IS200/IS605家族的Deinococcus radiodurans ISDra2中包含tnpA和tnpB基因，以及位于两侧的LE（Left element）和RE（Right element）。crispr依赖的转座酶（上一part）也是这样的序列结构。

![image](https://user-images.githubusercontent.com/111955215/187117222-64c33d7c-be0c-455e-85b0-ad12f35923d5.png)

在纯化TnpB的过程中，作者发现有许多RNA也被一同纯化。对TnpB结合的RNA进行small RNA测序（sRNA-seq）分析，发现它们大多是长度约为150nt的长非编码RNA，来源于ISDra2中的RE序列，作者将这些RNA称为reRNAs（right element RNA）。reRNA 3’端的16nt来源于IS200/IS605转座子的侧翼DNA序列，其余序列与TnpB基因的3’端和RE序列匹配，说明TnpB可以与转座子3’端来源的reRNA形成RNP复合物。

PAM（protospacer adjacent motif）序列是Cas9或Cas12核酸酶启动DNA切割所必须的，那么TnpB发挥作用可能也需要类似的序列。通过PAM鉴定实验，作者观察到在目标基因5’端上游富集了大量的TTGAT序列，并称之为**Transposon Associated Motif (TAM)**。体外DNA切割实验证实**TnpB具备RNA引导的靶向dsDNA的核酸酶活性**。进一步分析发现，将TnpB序列中的RuvC-like活性位点突变后，TnpB失去了切割能力，说明RuvC模块与TnpB的活性相关。研究人员发现实现TnpB的DNA切割功能需要同时满足两个条件：（1）TAM序列；（2）与靶基因匹配的位于reRNA 3’端的序列。


随后，作者对切割产物进行了测序分析，结果显示，TnpB采取的是一种交错切割模式，在NTS（non-target strand）的多个位置和 TS (target strand) 的单个位置进行切割，最终产生5’-悬挂端（overhangs）
