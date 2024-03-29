Notes from DearJohn-2
=====
<a href="https://dearjohnsonny.github.io/Notes1-Biotech/">Notes1-Biotech</a>

<a href="https://dearjohnsonny.github.io/Notes3-Statistics/">Notes3-Statistics</a>

<a href="https://dearjohnsonny.github.io/Notes4-Linear-Algebra/">Notes4-Linear-Algebra</a>


# 数据库操作
## PDB
PDB格式以文本格式给出信息, 每一行信息称为一个 记录(record). 一个PDB文件通常包括很多不同类型的记录, 它们以特定的顺序排列, 用以描述结构.具体见下面的链接
<a href="https://blog.sciencenet.cn/blog-548663-895916.html">PDB文件格式说明</a>

关于原子比较细节，可以看下面这张图：

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/617e2c35-42cd-46a4-a2d4-354afa74741f" width="1500">
</div>

# 基础知识
## 脱Boc保护的方法

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/44aa033f-80c5-42b1-a1a1-d200c07e74da" width="600">
</div>

<a href="http://muchong.com/html/201607/10459732.html">小木虫的脱Boc的方法</a>

## 激发、发射与吸收
首先根据紫外可见吸收谱，以最大吸收波长作为荧光发射谱的激发波长，在此激发波长下测量荧光强度和发射波长的关系得到荧光发射谱，即可知道荧光发射波长。然后测量在此最大发射波长下的激发波长与荧光强度的关系即得到激发光谱。

## 关于激发和发射
分子S0和S1态中各振动能级能量间隔的分布情况相似，故最终的两光谱峰型相似且对称

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/f359c3fd-cd50-4c82-a18d-4890db1d6de7" width="1500">
</div>

## 关于CLIP
CLIP（全称叫做Crosslinking immunoprecipitation-high-throughput-sequencing，交联免疫共沉淀）是一种分子生物学的方法，其通过结合UV交联和免疫共沉淀的方法来分析蛋白与RNA相互作用的结合位点。从而研究ribonucleoprotein (RNP)复合物在转录及相关细胞过程中的相互作用。

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/59ec9832-00e3-4f2a-810f-d1c85e5d0c2d" width="1500">
</div>

**workflow**
* 首先使用UV在体内交联RNA与蛋白复合物，UV曝光后会在相近的蛋白以及核酸之间形成共价键
* 随后裂解交联的细胞，片段化RNA，免疫沉淀分离目标蛋白。
* 接下来为逆转录做准备，在RNA的3'末端添加RNA接头并标记RNA确保结合蛋白的RNA的信息被保留。
* 随后去除蛋白部分，使用凝胶电泳和膜转移后将RNA蛋白复合物与游离的RNA分离开，再使用蛋白酶K将蛋白去除掉。这一步会在交联部分会留下一些氨基酸，从而导致交联的核酸部分有cDNA的truncation
* 之后cDNA被重新合成用于后续高通量测序，通过生物信息学的方法可以分析具体的作用位点。

**下面这个图更好点**

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/4ad5bdfd-68e7-4b6d-addd-c419bdd3e412" width="1500">
</div>


**2021年有一篇，快速的CLIP，从该工作可以得知adaptor的组成**

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/5132b227-c759-47ad-97d5-ed6477805811" width="1500">
</div>

<a href="https://doi.org/10.1038/s41467-021-21623-4">Nat Commun 12, 1569 (2021)</a>

### 鉴别具体的RBP结合位点：借助ADAR的TRIBE方法（targets of RBPs identified by editing）

现有的方法一般是将ADAR的catalytic domain融合到RBP上去，然后根据A-G的位点判断RBP的具体结合位点

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/10992a1b-692e-4215-90d3-551884dafdcb" width="1500">
</div>

**2023-6有一篇nature chemical biology介绍了一种更优的方法，将RBP和ADAR分开，用Rapamycin来介导信号的触发**

<a href="https://www.nature.com/articles/s41589-023-01372-9">Profiling dynamic RNA–protein interactions using small-molecule-induced RNA editing</a>

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/da4ebd8c-65ea-4e86-ab9f-25f8bee51d9a" width="700">
</div>

## 单细胞测序
### why single-seq？
传统的研究方法，是在多细胞水平进行的。因此，最终得到的信号值，其实是多个细胞的平均，丢失了异质性的信息

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204177452-03336866-06d6-4283-8012-bdfd1291930a.png" width="400">
</div>

### 具体原理
对于3’单细胞转录组来说，每一个凝胶珠携带足量条的核酸链，而每条核酸链由read1 primer，细胞标签（barcode），分子标记（UMI），poly(dT)组成。一个凝胶珠上所有的核酸链的细胞标签（barcode）是相同的序列，而不同于其他凝胶珠上的细胞标签（barcode），用于标记细胞。一个凝胶珠上所有的核酸链的分子标记（UMI）是不同的，用于标记不同的RNA序列。

下图中的PCR和T7是用来后续扩增用的

一个液滴中只有一个凝胶珠和一个细胞（也是单克隆）

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204175994-5a40caa8-5a85-4720-994a-f85288a21304.png" width="1500">
</div>

## 荧光
### FRET 荧光共振能量转移
荧光共振能量转移技术，是采用物理方法去检测分子间的相互作用的方法。他适用于在细胞正常的生理条件下，验证已知分子间是否存在相互作用。此方法的检测原理如下：
将我们要检测的蛋白（如图X和Y），分别偶联上D和A荧光蛋白，D和A是一对荧光物质，我们称之为供体（donor）和受体（acceptor）。当用430nm的紫光去激发X融合蛋白时，它能够产生490nm的蓝色荧光；同样，当我们用490nm的蓝光去激发Y融合蛋白时，它能够产生530nm的黄色荧光。

当蛋白X和Y间没有相互作用时（两者的空间距离>10nm），融合蛋白X和Y分别产生相应的荧光而被检测到，如果蛋白X和Y间存在相互作用（两者的空间距离需<10nm，结合图2），用紫光激发融合蛋白X其产生的蓝光会被融合蛋白Y吸收，从而产生黄色荧光，这时，在细胞内将检测不到蓝色荧光的存在。这时因为能量从X融合蛋白转移到了Y融合蛋白，这就是荧光共振能量转移技术。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199228152-b3e86e8f-da8c-4f41-b532-953d096ad452.png" width="500">
</div>

### 分子间荧光四联体 Fluorescent Intramolecular Tether (SNIFITs) 
靶蛋白 —— 荧光供体（如GFP）—— 拉拢荧光基团的配体 —— 荧光配体 —— 靶蛋白配体 

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199228244-59f79695-16a4-498f-b879-04289a6d245b.png" width="1200">
</div>

## 其他
* 等温滴定量热法（ITC）：可用于直接测定配体溶液加入蛋白质溶液中时所释放的热量，从而得到熵和焓，从而得到热力学相关指标。
* R·L —— R + L，Kd = [R][L]/[RL], Ka = [RL]/[R][L]，配体浓度越高，则R的利用率越高。因此配体即药物的浓度需要高过Kd10倍，从而[RL]:[R]大于10，超过90%的受体将被结合
* on-rate = Kon[R][L],off-rate = Koff[RL]，Kd = Kon/Koff
* crLacZ一般用作non-targeting control，作为没有靶向互补序列但可以招募Cas蛋白的阴性对照，序列为cgaatacgcccacgcgatgggt
* Halo Tag标签蛋白是一种脱卤素酶的遗传修饰衍生物，可与多种合成的Halo Tag配基有效地共价结合。这个分子量为33KDa的单体蛋白能融合在重组蛋白的N端或C端，并在原核和真核系统中表达。HaloTag配基是小分子化学物，能够在体外或体内与Halo Tag蛋白共价结合。这些配基由两个关键组分组成：(1)一个是通用的Halo Tag反应联结子，结合Halo Tag蛋白；(2)一个是功能基团,例如荧光染料或亲和媒介。
* 基于RNA的纳米结构需要二价阳离子(如Mg2+)来稳定结构


# 杂谈

## DARPin药物
DARPins是眼科和肿瘤学领域，抗病毒药物领域正在开发的一种新型治疗药物，由molecular partners公司研发，全称“designedankyrin repeat proteins”，即经设计的锚蛋白重复折叠蛋白。它们在结构上不同于抗体，由连接的DARPin结合域的单链组成。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204174248-5aa4dbf0-af63-4da0-b887-133f7c9e382c.png" width="1500">
</div>

### 锚蛋白重复结构域
天然存在的锚蛋白重复结构域以高丰度存在于各种种属，在人类中，145个基因编码共计404个锚蛋白重复结构域。在自然界中，锚蛋白重复结构域经常出现在多功能蛋白质的环境中，这启发了研究人员通过设计锚蛋白重复折叠蛋白作为治疗候选药物

AR蛋白是由33个氨基酸重复序列堆积而成，每个重复序列形成一个β转角，然后是两个反向平行的α螺旋和一个到达下一个重复序列β转角的环。在大多数已知的复合物中，β-转角和第一个α-螺旋介导与靶的相互作用，不同数量的相邻重复参与结合。已经报道的天然AR蛋白的靶结合亲和力在低纳摩尔范围内

实验者设计了一个共有AR模块，该模块由6个不同的潜在相互作用残基（可以是除半胱氨酸、甘氨酸和脯氨酸以外的任何氨基酸）和27个框架残基（26个是固定的，一个允许是天冬酰胺、组氨酸或酪氨酸）组成。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204172948-bb3b3f05-b710-4bb8-b778-0747c5d72093.png" width="600">
</div>

通常来说，DARPin的结构包含4到6个重复结构，其中第一个(N-cap加帽重复结构)和最后一个(C-cap加帽重复结构)用于保护疏水蛋白核心不受水环境的影响，屏蔽疏水蛋白核心。少于3个重复序列的蛋白质不能形成足够稳定的三级结构。而DARPin的近似分子量取决于重复数。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204173095-9e14569e-44a0-4ec6-9fb5-c3fef579f098.png" width="400">
</div>

由于一个组件的分子量仅高于3.5kDa，DARPin由4 - 6个组件组成，因此它们的分子量范围为14 - 21 kDa，这大约是常规IgG抗体大小的十分之一，或Fab片段大小的三分之一，Fab片段是目前批准用于治疗用途的最小抗体片段

### 与普通单抗的优劣势
常用的单克隆抗体是IgG抗体，其制备相对困难，成本很高；其结构域依赖于二硫键，因此在制备过程中需要避免还原性的胞内环境；一些抗体在加入特定的结构域之后会倾向于聚集；一些抗体在原核生物的表达系统中难以形成正确的三级结构。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204173841-e25144a5-0029-4faf-9d48-35a990c110bc.png" width="700">
</div>

### 应用

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/204174707-b969b14f-8d9e-473b-b2dc-f0561a3d2242.png" width="1500">
</div>

(A)显示了作为拮抗剂的单价DARPin，其结合受体（蓝色）或配体（绿色），其中一个DARPin示意性地被PEG化用于半衰期工程。

(B)描述了多特异性DARPin，其在两个位点结合靶点以获得额外的功效

(C)结合靶细胞（例如肿瘤细胞）的细胞表面抗原的DARPin配备有融合剂，其可以是蛋白质（毒素、细胞因子或酶）

（D）放射性配体

（E）小分子量毒素。

(F)三特异性DARPin可携带对肿瘤抗原的特异性，另一种用于募集效应细胞，而结合血清蛋白的第三种DARPin可被添加用于血清半衰期工程。(G)由两种不同的中等亲和力肿瘤靶向结合剂组成的双特异性DARPin可显示出比单价高亲和力结合剂增强的肿瘤选择性，因为只有两种抗原的组合才排他地存在于肿瘤表面，从而增加了双特异性构建体的高亲和力结合，即使单独的单个抗原也在健康组织中表达。

## 丝氨酸整合酶及DNA整合

### 一些关于attB和attP的简介
<a href="https://blog.addgene.org/plasmids-101-gateway-cloning">An introduction to Gateway technology</a>

图一：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/203915172-eb2ea5cb-50cc-4d02-83c1-35aeb5f085c9.png" width="1200">
</div>

图二：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/203915753-741766a3-9345-4f56-8468-be1a7ad99267.png" width="600">
</div>

图三：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/203916682-9f92a653-c782-42c6-b55f-6380e75a345b.png" width="1200">
</div>


## 相分离 phase separation

<a href="https://mp.weixin.qq.com/s/Fkq5m2I3HulsKHrCYDEycg">相分离微信公众号</a>

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/202605637-684165c1-77cd-425e-92f2-05f85958c388.png" width="1200">
</div>

“液-液相分离”，是工程学、化学、物理学中的基本概念。只要两种液体间存在使它们分离的力，“相分离”就会发生，最常见的例子就是油漂在水面上。

### 胞内的相分离
在原来的细胞概念中，细胞内环境杂乱而无序，太多的分子在其中无规律的游走，那么到底是什么 帮助了生物学反应的进行，并且避免了来自那些不需要的物质的干扰呢?

通过 "相分离" ，也许可以提供一种方式让细胞内的特定分子聚集起来，从而在 “混乱的" 细胞内 部形成一定 "秩序"

* 最近的最大进展应该就是相分离和转录Q之间的关系了，当时一出来真的是举世皆惊。在超级增强子调控的转录复合物中，转录辅激活因子BRD4和MED1存在固有无序区域，能够形成相 分离的液滴，从而调控相应基因的转录作用。
* 麻省总医院的分子生物物理学家Susanne Wegmann和她的同事们发现阿尔茨海默病患者脑
* “相分离”异常还可能导致某些肿瘤。19年，麻省总医院的分子病理学家Miguel Rivera和他的团队发现了一种与尤文肉瘤有关的蛋白。这种蛋白聚集在与肿瘤发生相关的基因组附近时可以激活致癌基因表达，而异常的“相分离”就可能促使这种蛋白在这些区域附近聚集。

综合这些将“相分离”与肿瘤或神经退行性疾病联系起来的研究，Hyman和MPI-CBG的Simon Alberti提出，衰老相关疾病事实上也可能与细胞无法控制“相分离”相关。机体一直在努力保持正常细胞结构，但“在某个时点，整个体系就那么失控了”，Alberti说。

在人体细胞中，形成液滴更多的是一种细胞构架方式。19年，加州大学旧金山分校生物化学家Geeta Narlikar和她的团队发现，“相分离”帮助封存人体部分基因组，这些基因组永久不会被激活，主要发挥结构性作用。香港科技大学结构生物学家Mingjie Zhang的团队发现，帮助大脑细胞接收信号的一种细胞机制是通过“相分离”建立的。

## 共价药物
共价药物结合了轻度反应性官能团，该官能团与蛋白质靶标形成共价键，以赋予药物结合所涉及的非共价相互作用以外的其他亲和力。研究者偶然发现的许多早期的共价药物可以结合活性位点抑制酶促活性。这些药物通常模仿底物过渡态，以实现催化氨基酸残基的共价修饰。在过去的30年中，共价药物的合理设计引起了越来越多的兴趣，共价靶向非保守氨基酸以增加选择性已变得司空见惯

**亲电优先**：靶向共价抑制剂通常是通过将亲电试剂掺入配体中而通过结构指导的设计发现的，否则该配体将可逆地结合目标蛋白。掺入的亲电试剂不可逆地与目标蛋白上的氨基酸结合，从而引入共价相互作用。共价配体筛选是另一种越来越普遍的配体发现方法，其中使用各种方法从**亲电化合物**的文库中发现共价配体。这种 “亲电子优先” 方法部分地通过开发化学蛋白质组学平台来促进，该平台能够快速鉴定靶标并对共价ligands14-18进行选择性分析。

**针对“undruggable”的蛋白**：通过共价修饰的有效抑制作用已使传统上 “不可治疗” 的蛋白质成为可靶向药物，例如sotorasib (Amgen) 的批准，sotorasib是突变KRAS(G12C) 的抑制剂

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199140062-8b8ebcb6-6dfa-455a-93cb-21101e065e9f.png" width="1500">
</div>

* 阿司匹林：通过在环氧合酶1的底物结合通道中乙酰化Ser529发挥抗炎作用，阻止底物花生四烯酸转化为前列腺素
* 由青霉菌产生的 β-内酰胺类抗生素如青霉素与青霉素结合蛋白 (PBPs) 结合，PBP参与细菌细胞壁合成。所有PBPs均含有可被青霉素酰化的活性位点丝氨酸残基，从而抑制PBP活性并导致细胞膜破裂
* 奥美拉唑，一种用于预防中风和心脏病发作的抗血小板药物（在共价效果被发现之前用于cure胃食管返流），在肝脏中被细胞色素P450酶激活，产生具有生物活性的硫醇代谢物

### Covalent EGFR inhibitors
从第一代到第二代的 抑制剂的发展涉及添加反应性丙烯酰胺亲电试剂以共价结合半胱氨酸残基 (Cys797)。在从第二代到第三代EFGR抑制剂的过程中，喹唑啉部分被嘧啶单元取代，以为T790M突变体提供选择性。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199140999-8a59fade-44ac-4345-8f97-37f8ad3f6194.png" width="1500">
</div>

## Phenotypic drug discovery(PDD)
<a href="https://www.cn-healthcare.com/articlewm/20210309/content-1197023.html">使用表型筛选发现全新的药物及靶点</a>

### TDD和PDD各有优缺点
基于靶点的药物发现TDD优点在于因为靶点和机理已知，所以很容易设计高通量的筛选试验，而且过去三十年间，有大量成功的案例，而缺点在于由于靶点一般来自于理想模型的机理研究，所以真的回到人体环境的疾病中，这个靶点可能根本不相关; 很多报道的靶点无法在实验室中重复出来；一般这样的靶点都是单一、简单的原理，在复杂的疾病中很容易被代偿绕过去。像NASH或者肿瘤微环境这样多细胞多通路参与的，有无数文献看起来极其有潜力的靶点，死在药物开发的各个阶段。还有一点就是已验证的好靶点数目是非常有限的，所以会造成很多家公司在竞争同样的靶点。

而基于表型筛选的药物发现，优势在于筛选出来的药物靶点直接和疾病生物学模型相关（因为就是拿疾病生物学模型筛到的），而且一次筛选筛到的几个药物可能针对多个靶点，多种机制。这些靶点很可能是全新的，所以潜在的竞争要少很多。但它也有自己的问题，比如靶点和机理未知在后面进一步开发的时候可能会有困难，尤其找到已经筛选到的药物作用的靶点实际是个非常有挑战性的工作，即使找到了靶点，进一步的靶点验证可能还是必须的。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199137790-ae0fc08d-37d2-4aab-a823-0f3dc78a7c97.png" width="1500">
</div>

### 关于PDD细节
什么样的assay才是最relevant的assay? 每一种疾病可能都不太一样，和疾病生物学更相关assay可能通量不够大，敏感度不够高。所以一个好的初筛assay，需要平衡的方面很多：生物学相关性，敏感度，成本，可重复性等等。一个可以考虑的策略是使用基于靶点的药物开发中使用过的，证明高度相关的assay。

下图为例子：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199137171-f4266675-2fb7-40bd-890c-6131fbc9d7b7.png" width="900">
</div>

## 靶向RNA的方法

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/198944569-aed05e46-a0f7-4508-99d2-9274d5d35f6b.png" width="1500">
</div>

IRE (iron- responsive element; translational regulation)

splicing modulators (alternative pre- mRNA splicing including those that interact with U1 small nuclear RNA (snRNA))

RNA repeat expansions (aberrant gain- of- function; microsatellite disorders) and Drosha and Dicer processing sites in microRNA (miRNA) precursors

## snRNA家族
真核细胞有细胞核和细胞浆中都含有许多小RNA，它们约有100到300个碱基，每个细胞中可含有 $10^5 - 10^6$ 个这种RNA分子。它们是由RNA聚合酶Ⅱ或Ⅲ所合成的，其中某些像mRNA一样可被加帽。在细胞核中的小RNA称为snRNA，而在细胞浆中的称为scRNA。但在天然状态下它们均与蛋白质相结合，故分别称为snRNP和scRNP。某些snRNPs和剪接作用有密切关系。snRNAs中最受注意的一个是U1，它普遍存在于哺乳动物、鸟类和昆虫细胞中。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/198943203-a85d04a3-74ff-45de-8769-350462e047f6.png" width="1500">
</div>

### U1 snRNA and U1 snp
应该是可以在RNA前体的剪接时抑制外显子的过早被加上Poly A，从而表达完整的mRNA

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/198942604-e9955497-9356-4a4d-b019-88983f7273be.png" width="1500">
</div>

以及辅助内含子的切除：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/198943535-97afeb6a-1583-4fd7-b64b-9af47e4ff47c.png" width="1500">
</div>

##  Xeno Nucleic Acids (XNAs) 

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197179127-8fbcda6e-0f18-48c3-9785-d683d96765ab.png" width="900">
</div>

### XNA polymerase的筛选方法

#### 传统的Compartmentalized Self-Tagging(CST)

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197184198-fba181f6-8654-4daf-acf3-3ff3dc605b2b.png" width="1500">
</div>

需要在细胞中实现，判断是否有聚合活性靠的是再捕获，若有活性则可以延伸，从而与质粒可以结合配对

同时由于质粒可以被recover，从而所获得的质粒编码的序列就是有活性的酶序列。这样可以实现具有活性的酶与其序列的对应性

**Overview of the CST protocol**：
* Polymerase repertoires are generated (A10) and expressed (B14) in bacterial cells. 
* Bacterial cells are compartmentalized in a water-in-oil emulsion with synthetic nucleotide triphosphates (xNTP) and a short biotinylated selection primer (C22) for isolating genotype-phenotype combinations.
* Cells are disrupted by heat denaturation, allowing polymerase access to substrates (C23).
* Active polymerases, capable of incorporating the xNTPs, extend the selection primer, stabilizing its interaction with the plasmid. Inactive polymerase variants do not extend the primer (or do so poorly).
* Emulsions are disrupted and all plasmid DNA isolated. Excess unextended selection primers are removed by gel filtration (D27), and remaining biotinylated primers are captured (E33), using streptavidin-coated paramagnetic beads. 
* Recovery of biotinylated primers also recovers plasmids still bound to the primer. Beads are washed in stringent conditions (TBT2 supplemented with 20% v/v formamide) to remove loosely bound plasmids, enriching the population for the genetic information of active polymerases (E34). 
* Recovered plasmid DNA is amplified and used to start a new round of selection or screening.

#### 新的筛选方法

本方法使用珠子上的特有序列来分别捕获质粒、以及作为延伸引物来合成新的XNA链，同时用这种级联放大的方式来增强荧光

本方法好在既可以将phenotype and genotype联系起来，又可以不破坏珠子

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197186288-7d92fcdd-b10c-40ba-b921-aa796c88c78c.png" width="1500">
</div>

### XNA polymerase和逆转录酶都被筛出来啦

根据以上的CST方案，研究者以TgoT为模板突变出来了Pol6G12等酶，从而实现了以XNA为模板的复制和逆转录

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197190385-24a17f58-672b-492b-8577-d1415d197a95.png" width="1500">
</div>

### 在上述基础上筛选XNAZymes
XNAZymes的好处之一是可以减少被体内核酸酶切掉的现象，延长半衰期

下图是大概的筛选流程：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197193321-55f22407-4d5b-486d-a923-78952fbeaf0f.png" width="1500">
</div>


针对不同的筛选目的（看不懂可以看看<a href="https://www.nature.com/articles/nprot.2015.104">原文</a>），可以设计不同的模板（后续的步骤也比较类似就不展开了）

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197194321-ba863fa5-5529-46ce-91af-861a4305535a.png" width="1500">
</div>

## TALE protein
### 简介
TALE (Transcription Activator Like Effectors)植物致病菌Xanthomonas通过III型分泌系统注入到宿主细胞内的一种蛋白质。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/196022733-2b860e11-e161-4527-a049-69fe7f1190a9.png" width="900">
</div>

TALE蛋白的奇特之处在于它的DNA结合结构域——该DNA结合结构域不同于其他已知的DNA结合结构域。它是由不同数量的重复单元组成，每一个重复单元特异识别一个DNA碱基对。大多数情况下**每个重复单元由34个氨基酸**组成。这34个氨基酸中除了第12，13位的氨基酸变化较大之外，其他氨基酸高度保守。这**两个不保守的氨基酸被命名为RVD**（repeat variable diresidue）。

![image](https://user-images.githubusercontent.com/111955215/196022435-b52cd1e5-b924-45f7-aee0-3785bdcbb33d.png)

每个重复序列中12，13位的氨基酸和识别的核苷酸种类有特殊的一一对应关系。(NI for A, HD for C, NG for T, and NN for G)。

下图为TALE文库的构建：

![image](https://user-images.githubusercontent.com/111955215/196022466-e97c8fdb-7204-45bb-a4be-7ba9a4857879.png)
### 应用
TALE蛋白的特异DNA序列识别以及灵活的可组装性为它们在分子生物学中的应用提供了巨大的前景，科学家们可以设计组装任意的TALE单元去识别目标DNA双螺旋序列。这一特性已经被用来构造切割特异双链DNA序列的**DNA酶TALEN** (TALE nuclease)，成功用于在细胞基因组中引入定点突变、定点敲除等操作（引入双链DNA断裂DSB之后用NHEJ或者HDR的方法进行编辑即可）。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/196022931-fe60aab6-5cd5-4179-bcc9-4297229973d9.png" width="900">
</div>

## BRD4蛋白
BET（Bromodomains and Extraterminal）家族成员，BRD4的特征是有两个串联溴结构域（BD1 and BD2）。

### 关于溴结构域和BET家族

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193969353-d77671e5-0ee0-4ab4-a81e-3dab04e18f70.png" width="1500">
</div>

* **与组蛋白赖氨酸残基的的乙酰化部位结合**：溴结构域家族的蛋白可以与沿染色质的高乙酰化组蛋白区域相互作用，结合乙酰化的赖氨酸残基，包括组蛋白。**BRD4调节转录很大程度上依赖于其能和组蛋白赖氨酸残基的乙酰化部位结合的特性**。

* **募集转录调节复合物**：BET家族可以招募转录机器，从而上调转录；而TFⅡD也含有BRD亚基，其通过与核心启动子序列结合并募集其他转录调节因子来促进转录起始（ZMYND8和NuRD是下调转录的）

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193974002-1028bdd2-5167-4d68-abad-efa826dd3acd.png" width="800">
</div>

(A) Brd2和Brd3促进基因转录。组蛋白中它们的溴结构域 (BD) 与乙酰化赖氨酸 (Ac) 之间的相互作用促进了RNA Pol II通过高乙酰化核小体延长新生转录本。箭头指示转录的方向;

(B) Brd4在起始和延伸过程中调节基因转录。在启动子近端区域，由于正转录延伸因子b (P-TEFb) 的失活，RNA Pol II暂停，与7SK小核RNA (snRNA) 和HEXIM1蛋白形成复合物。Brd4增强对P-TEFb的募集会导致Pol II中的Ser2磷酸化，从而导致Pol II从转录延伸的停顿中释放出来。P-TEFb与Brd4和JMJD6与远端增强剂相关的相互作用也支持了暂停释放。Brd4通过其溴结构域 (Brd4中的红色圆圈) 与乙酰化赖氨酸相互作用，而P-TEFb与Brd4 CTD (Brd4中的绿色区域) 相互作用。此外，Brd4通过其溴结构域促进沿超乙酰化核小体上基因的新生RNA合成。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193975036-fad31cf1-88ba-4c60-854c-285341b0795e.png" width="800">
</div>

* BRD4与组蛋白和TFs的同时结合将稳定TFs与ENHs的结合，从而维持这些元件的转录活性。

**总结一下：**

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193976853-143eeffd-88e4-403d-97a8-beaf90a707d8.png" width="1500">
</div>

抑制BET家族的蛋白活性之后可以降低其激活效应，可以通过下图的方式抑制BET家族蛋白作用

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193970686-bf380918-8a10-4f12-aea7-a48e55d9d4f9.png" width="800">
</div>

### BRD4的具体作用
#### BRD4在炎症和免疫调节NF-κb途径中的作用
BRD4通过至少四个途径调节TLR配体引起的NF-κb途径的激活:(1) BRD4通过其非典型组蛋白乙酰转移酶活性直接乙酰化RELA; 

(2)BRD4直接促进RELA的磷酸化；

(3-4)BRD4通过抑制NFKBIA的翻译和增加NFKBIA和IKBKB的磷酸化来促进RELA的磷酸化。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193994186-6ee17905-c934-45ab-87f3-285b6450601b.png" width="1500">
</div>

缩写: CDK9，细胞周期蛋白依赖性激酶9; CHUK，核因子κB激酶复合物的抑制剂; CycT1，cyclin T1; IKBKB，核因子κB激酶调节亚基β的抑制剂; IKBKG，核因子κB激酶调节亚基γ的抑制剂; NFKBIA，NFKB抑制剂α；NFKB1，核因子κB亚基1; p-TEFb，正转录延伸因子b; RELA，RELA原癌基因; RNA pol II，RNA聚合酶II; TLR，toll样受体

#### BRD4在炎症和焦化中调节NLRP3途径的作用
a在TNF引发的大鼠髓核细胞中，尿酸钠诱导急性痛风性关节炎，大脑中动脉闭塞诱导神经胶质活化，BRD4抑制RELA介导的NLRP3转录和随后的CASP1-dependent炎症小体活化。b在肾细胞癌组织和细胞中，RELA介导的NLRP3转录和随后的CASP1-dependent炎性体激活和GSDMD介导的焦磷酸病需要BRD4。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193994919-159b85cf-d5fe-4d67-b38f-f500f886d26d.png" width="1500">
</div>

缩写: BETi，bromodomain和extraterminal抑制剂; CASP1，caspase 1; GSDMD，gasdermin D; GSDMD-NT，gasdermin D的N-末端结构域; IL1B，白细胞介素1β; IL18，白细胞介素18; NLRP3，NOD样受体热蛋白结构域相关蛋白3（NLRP3）; PYCARD，PYD和CARD结构域; RELA，RELA原癌基因; TNF，肿瘤坏死因子

#### BRD4在抗病毒免疫中调节STING1途径的作用

来源于各种病毒的细胞质DNA激活CGAS，产生内源性环二核苷酸cGAMP，与位于内质网的STING1结合，进而促进STING1从ER到核周区的二聚和易位。在转运过程中，STING1招募并激活TBK1，刺激IRF3的磷酸化和核易位，并在较小程度上刺激NFKB1，从而导致1型IFN和其他炎性细胞因子 (例如IL) 的产生。IRF3和NFKB1的核活性被brd4抑制。此外，在BRD4抑制后，DDR的激活可诱导宿主dsDNA从细胞核释放到细胞质，导致CGAS-STING1途径进一步激活以限制病毒感染。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193994989-90813bf7-5da5-42f8-9ded-3db5a84e2fe5.png" width="1500">
</div>

缩写: cGAMP，环GMP-AMP; CGAS，环GMP-AMP合酶; DDR，DNA损伤反应; dsDNA，双链DNA; IFN，干扰素; IL，白细胞介素; IRF3，干扰素调节因子3; NFKB1，核因子κB亚基；STING1，干扰素反应刺激因子cGAMP交互因子1; TBK1，TANK结合激酶1

## 糖基化
在蛋白质的多种翻译后修饰中，糖基化（glycosylation）是非常重要的一种。糖基在酶的催化下，与蛋白质上的某些残基形成共价连接，通常是糖苷键。

据估计，哺乳动物中的糖链大约有七千多种结构，其结构单体约为10种单糖（包括糖衍生物）：葡萄糖（Glc）、半乳糖（Gal）、甘露糖（MAN）、木糖（Xyl）、岩藻糖（Fuc）、N-乙酰氨基葡萄糖（GlcNAc）、N-乙酰半乳糖胺（GalNAc）、葡萄糖醛酸（GlcA）、艾杜糖醛酸（IDOA）、唾液酸（SA）。其中两种糖醛酸主要分布在蛋白聚糖中。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193834469-4423defd-e218-4670-953b-841a70c161f6.png" width="800">
</div>

在基本氨基酸中，至少有9种氨基酸残基可以被糖基修饰。糖基可以通过多种方式与蛋白质相连，例如与Asn侧链的酰胺键相连（N-糖基化），通过糖苷键与Ser、Thr、羟基赖氨酸（胶原）或Tyr（糖原蛋白）的羟基相连（O-糖基化），或通过C-C键连接到Trp的C2位置（C-甘露糖基化）。另外，还可以通过糖基磷脂酰肌醇（GPI）锚间接与蛋白质相连。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193842458-9e9a580d-4ef0-48b8-9c39-7e46a594578f.png" width="1500">
</div>

### 分类
* N-连接的糖基化（N-linked glycosylation）：与天冬酰胺残基的NH₂连接，连接的糖为N-乙酰葡糖胺(GlcNAc)

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193840066-6f2cc2f5-cd1c-49a0-b252-9f09b6c2a72f.png" width="1500">
</div>

* O-连接的糖基化（O-linked glycosylation）：与Ser、Thr和Hyp的OH连接，连接的糖为半乳糖或N-乙酰半乳糖胺(GalNAc)，在高尔基体上进行O-连接的糖基化。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193839249-273f379e-b260-43e3-99f2-1978cbc38319.png" width="700">
</div>

### 功能
糖基化的作用可概括为3点：①使蛋白质能够抵抗消化酶的作用；②赋予蛋白质传导信号的功能；③某些蛋白只有在糖基化之后才能正确折叠。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193846567-1cd9d141-98ba-456f-a812-ac8a5a081ad5.png" width="1100">
</div>

## 核糖开关
 核糖开关（Riboswitches）是一类非编码RNA元件，主要存在于细菌mRNA（DNA也有，因此不仅可以影响翻译，还可以影响转录）的5′非编码区（5′UTR），通常由适配体（aptamer）和表达平台（expression platform）两个功能域组成。当特定分子（ligand，配体）结合适配体域时，会引起表达平台域的局部构象发生变化，从而打开或关闭下游基因的表达。核糖开关广泛存在于细菌中，它们在细菌的硫代谢、辅酶合成、氨基酸合成等基础代谢中发挥着非常重要的调控作用，迄今为止，已有20余类感应不同分子的核糖开关在细菌中被确认。

### 常规作用机制

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192923251-90ece5c4-a1a1-455c-a0f9-031e7c894f56.png" width="1500">
</div>

PS：
* Shine-Dalgarno （SD）是细菌和古细菌中信使RNA中核糖体结合位点序列。通常位于翻译起始密码子AUG上游约8~10个碱基位置。SD序列帮助招募核糖体RNA，并将核糖体比对并结合到信使RNA（mRNA）的起始密码子，从而开始蛋白质合成。

### 非常规的核糖开关作用机制

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192923743-92565861-64cd-4444-a150-1aed4706cb42.png" width="1500">
</div>

### 总结一下riboswitch的特点

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192927937-3eb25c40-1e77-4bbf-bdba-4fb139041922.png" width="600">
</div>

* 很少有串联，下面是例外
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192928266-76538b52-029d-4611-8f80-9088e0437d52.png" width="1500">
</div>

* 自剪接的情况也不多（PS：大多数核酶的活性都是自剪接的活性），下面是例外
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192928082-61a2fec2-d807-45ed-a46a-4c19339261f8.png" width="1500">
</div>

## 黄素Flavin
黄素是大多数生命形式所需要的黄色杂环分子，它们提供多种特定的催化任务。
对于人类来说，黄素是从饮食中获得的维生素 B2。黄素蛋白在细胞中的辅基有黄素单核苷酸（FMN）或黄素腺嘌呤二核苷酸（FAD）。FMN和FAD分别附着有磷酸盐或二磷酸腺苷(ADP)，可以与蛋白质非共价或共价连接

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192540999-ca281373-dbca-4c69-bd8c-2738cbd2a5f3.png" width="800">
</div>

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192550807-a5a95a48-e437-48b6-a27f-6a3289b802d0.png" width="400">
</div>


FAD 和 FMN 在 pH7.0溶液中双电子还原的氧化还原电位分别为 -219mV12和 -205mV。相较之下，完全还原/氧化是一个双电子过程，在 pH7的水溶液下，其中点电位约为 -200mV。

氧倾向于参与包含一个电子，一个氢转移的逐步进行的反应。核黄素的化学特性非常适合这种反应。因此，在生物系统中添加含有核黄素的辅因子后，系统可以利用涉及离子氢化物转移(通过 NAD 或 NADP) ，自由基氢离子转移(通过 FMN，FAD)或抗坏血酸和一个电子加一个质子转移(通过 FMN 或 FAD)的机制进行一系列氧化还原反应。比如生物氧化过程中的电子传递链上的复合体Ⅰ和复合体Ⅱ

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/192544648-e47a51cc-a56b-4364-8366-8c362aadf48f.png" width="800">
</div>

## 内含肽
内含肽，即蛋白质内含子，是存在于前体蛋白质中的一段氨基酸序列，在前体蛋白转变为成熟蛋白的过程中，它靠自我剪切的方式从前体蛋白中释放出来，同时两端的肽链以肽键的方式相连，该过程即为蛋白质剪接。蛋白质剪接不同于RNA剪接，前者的剪接发生在蛋白质水平，而后者的剪接发生在RNA水平：它也不同于蛋白质翻译后加工，后者往往只是切除前体蛋白端或C端的一些片段，通常没有多肽链的形成：而且也不同于酶原活化，蛋白质剪接有新肽键的形成。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/190904759-5b423651-80c8-4afe-91ea-6d90d81e01d9.png" width="500">
</div>

与内含肽相对应的是蛋白质外显肽，即内含肽两侧的氨基酸序列。位于内含肽端的序列称为N-外显肽，位于内含肽C端的序列称为C-外显肽。N-、C-外显肽在内含肽的作用下通过肽键连接成完整的成熟蛋白。内含肽有8种存在状态：剪接反应前称为融合内含肽，剪接反应后称为游离内含肽。两者的一级结构相同但功能却不同，前者可以自催化蛋白质前体的剪接反应，后者可作为归巢核酸内切酶参与内含肽归巢。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/190904838-b7185854-f114-4257-9c63-74c4978b2d8b.png" width="500">
</div>

# 信号通路
## P53
### 野生型和突变型p53在细胞生长方面的作用
野生型p53 (wtp53) 主要充当限制癌细胞增殖和存活的转录因子。还涉及许多非转录作用。Wtp53可以通过与凋亡调节BCL-2家族的多结构域成员 (例如BCL-2和BCL- X) 相互作用来促进线粒体诱导的凋亡，从而释放促凋亡的BH3-纯蛋白 (例如BAK和BAX) 的活性。Wtp53还可以在压力下增加Ca2负荷，从而诱导细胞凋亡。此外，wtp53是自噬的重要调节因子

突变型p53 (mutp53) 可以通过搭载其他转录因子 (TFX) 来调节转录，也可以通过非转录机制促进癌症。Mutp53可以抑制过氧化物酶体增殖物激活的受体-γ 共激活因子1α (PGC1α)，这是线粒体生物发生和氧化磷酸化的主要调节剂。此外，与wtp53相反，mutp53通过调节未折叠蛋白反应 (UPR) 抑制内质网 (ER) 应激诱导的凋亡，从而增加ER应激时的细胞存活率。Mutp53还诱导许多编码蛋白酶体亚基的基因的转录。由mutp53与转录因子核因子红细胞2相关因子2 (NRF2) 结合介导的这种转录激活导致蛋白酶体活性升高和肿瘤抑制蛋白降解增强。wtp53和mutp53均影响多个细胞器和区室，并且还可以通过分泌可溶性分子和外来体或胞外囊泡携带的各种分子来引起非细胞自主作用。wtp53的存在抑制高尔基体支架蛋白的表达，从而抑制高尔基体中的分泌囊泡生物发生，而mutp53可以通过与缺氧反应因子HIF1α 相互作用诱导microRNA miR-30d表达来调节高尔基体的功能。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199143635-cb6062b1-97f2-43dc-9af6-7c3a83927a33.png" width="1500">
</div>

### 野生型和突变型p53在肿瘤微环境方面的作用
p53可以通过调节肿瘤免疫微环境来影响免疫治疗。在p53野生型 (wtp53) 肿瘤中，肿瘤免疫微环境主要具有抗肿瘤作用。这可以归因于几种机制。例如，wtp53可以上调UL16结合蛋白1 (ULBP1) 和ULBP2和microRNA miR-34a的表达。ULBP1和ULBP2是天然杀伤 (NK) 细胞的激活配体，可增强其细胞毒性活性。miR-34阻断PDL1 mRNA的翻译并驱动其降解; 因此，PDL1蛋白水平在保留wtp53的癌细胞中被下调，使这些肿瘤细胞对cd8t细胞介导的杀伤敏感。此外，wtp53还能促进肿瘤细胞因子如肿瘤坏死因子 (TNF) 的分泌，进一步增强肿瘤免疫微环境的抗异质能力

在TP53突变的细胞中，ULBP1和ULBP2下调，PDL1上调，分别引起对NK和CD8 T细胞杀伤的抗性。此外，p53功能的丧失会驱动WNT配体的分泌，WNT配体与巨噬细胞上的同源受体结合，导致它们分泌IL-1β，从而吸引嗜中性粒细胞等促肿瘤细胞。Mutp53蛋白促进可递送microrna (如miR-1246) 的外泌体分泌，其将抗肿瘤M1巨噬细胞转化为促肿瘤M2巨噬细胞。这种前肿瘤巨噬细胞分泌IL-1β，该IL-1β 吸引前肿瘤调节性T (Treg) 细胞，从而抑制抗肿瘤反应并保护肿瘤免受免疫消除。Mhc-i，主要组织相容性复合体I类; RE，反应元件; TCR，T细胞受体。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/199144206-ce917168-aff0-4a70-b12c-661a8e7ea537.png" width="1500">
</div>

# 非编码RNA
## LncRNA
定义：长于200个核苷酸且没有编码蛋白质的RNA。

来自人类基因编码的统计数据表明，人类基因组包含16,000多个lncRNA基因，但其他估计超过100,000个人类lncRNA。

和mRNA一样，LncRNA也会5'端加帽(7-methyl guanosine, m7G) 和3'端加Poly A的尾巴；也会有剪接

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197428984-e58b90a5-a506-4793-9063-8ca6a80679af.png" width="600">
</div>

### 生物学功能
#### 染色体调节
招募染色质调节物：如下图中的HOTTIP这种LncRNA招募激活蛋白让HOXA基因激活

![image](https://user-images.githubusercontent.com/111955215/197430279-77b8f395-8699-4d4f-bdf4-1c41b1bc38e7.png)

诱捕染色质调节剂：如下图的lncPRESS1这种LncRNA将一种组蛋白去乙酰化酶SIRT6给抢走了，导致其无法去掉目标基因序列的乙酰化，从而阻止该基因表达

![image](https://user-images.githubusercontent.com/111955215/197430385-607450b9-546e-4c43-ae5f-fa2fe239029e.png)

LncRNA可以与DNA相互作用，并形成RNA-DNA杂交链，例如R环，从而被染色质修饰剂或转录因子识别，并产生激活或抑制靶基因转录的效应

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197430934-cc53f784-5e32-432f-b7ff-0b12ede5dc5d.png" width="800">
</div>

#### 转录调节

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197432040-2e855065-da13-4365-a60e-fedeb5aee0ac.png" width="1500">
</div>

#### 细胞核的组织

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197432155-98ee8311-de5f-498c-81e2-a2ddfe08dd51.png" width="1500">
</div>

#### 转录后修饰

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197432319-ce6444d7-b023-48a8-a979-05fa044e9809.png" width="1500">
</div>

# 酶进化系统

## PACE
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191239383-4fe2630b-c719-4d49-a698-3b8136cba33b.png" width="1000">
</div>

“泻湖”被新鲜宿主细胞的培养物不断地稀释。所有在泻湖内复制的DNA都通过工程诱变质粒进行诱变，以提供遗传多样性。只有编码功能性POI变异体的含SP基因能够比稀释速率更快地复制，从而使它们能够在泻湖中持续存在
为了同时进化和选择功能，宿主细胞还含有诱变质粒(MP)。MP使宿主细胞中的所有DNA发生随机突变，包括SP和宿主细胞基因组，以及细胞含有的任何质粒
MP在阿拉伯糖启动子的控制下表达诱变基因，在生长培养基中加入阿拉伯糖后诱变发生以保证突变的可控性。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191239799-d399706d-cf47-4969-a10c-21621fba69c9.png" width="1000">
</div>
阴性选择：由于进化酶的目标包括酶的特异性，因此研究者大多需要将用于进化的初始酶活性排除掉，因此需要阴性选择。即将原活性与一段无法表达的gⅢ基因联系起来，导致具有原活性的酶基因在筛选过程中无法富集

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191239813-07fd6595-2666-43f2-a20f-ce9d221b11a6.png" width="1000">
</div>

### 用于不同PAM序列的Cas蛋白筛选

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191392406-41428edb-2d19-48a2-8d1b-9fd065632bfa.png" width="800">
</div>

当突变后的Cas蛋白能够和目标的dsDNA结合并产生一定的构象变化时，与之连接的RNA聚合酶的亚基也会受到激活，从而导致RNA聚合酶的活性，从而gⅢ基因能够表达

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191392823-957da485-74f5-4e61-9f8c-117500dc9d54.png" width="800">
</div>

由于Cas蛋白激活聚合酶的机制未知，研究者又开发出了更高效的筛选方法——功能化的筛选。由于筛选的Cas蛋白主要用于碱基点突变，因此在筛选时将点突变与Cas蛋白的活性联系起来。此处是有两段内含肽包裹的PAM序列以及中止密码子，只有成功将终止密码子点突变的Cas蛋白才可以使内含肽开始剪接并产生完整的gⅢ蛋白。

提高筛选强度：两个密码子，同时减少数量
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191393464-63333f94-7b58-43d8-85af-e413dda0e97a.png" width="1500">
</div>

下图也是一样的思路：
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191393552-8e17d94c-4655-4d8b-80b0-59c5b28711b9.png" width="1500">
</div>

# 靶向蛋白降解
靶向蛋白质降解(targeted protein degradation TPD)目前主要通过泛素蛋白酶体和溶酶体降解目标蛋白，根据具体作用原理又可细分为近10个不同技术路线，其中发展最快的是分子胶和PROTAC技术。在真核细胞中，受损的蛋白质或细胞器主要通过两条相互独立，但又相互关联的途径进行清除，即蛋白酶体途径和溶酶体途径。一般来说，蛋白酶体通过泛素-蛋白酶体系统降解短寿命蛋白和可溶性错误折叠的蛋白，而溶酶体则通过内吞、吞噬或自噬途径降解长寿命蛋白、不溶性蛋白聚集体，以及其他大分子化合物和细菌、细胞器等。
![image](https://user-images.githubusercontent.com/111955215/188146827-89721640-25dc-4b3d-b4c0-ca9cf8831aed.png)

## 体内的蛋白酶体途径降解
在生物体内，E3泛素连接酶复合物通过识别degron（降解子）来选择用于降解的蛋白质。

降解子可能是常规序列：degrons是嵌入在促进泛素化和降解的底物中的**特定氨基酸序列**。底物蛋白的N基端的部分短序列是最早发现的降解子，最近（2018）已经<a href="https://www.sciencedirect.com/science/article/pii/S009286741830521X?via%3Dihub">报道</a>
了识别C末端降解子的E3连接酶。


<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/197369621-20b1f8e0-ec04-4b6b-8d29-a942a8335119.png" width="800">
</div>


也可能是翻译后修饰（PTM）产生的**特定基团**。<a href="https://www.nature.com/articles/s41586-022-05333-5">2022年的文章</a>发现CRBN的在生物体内的目标蛋白包括蛋白质C基端通过翻译后修饰产生的环状酰亚胺(cyclic imide)。这些PTM由特定的酶产生，在蛋白质ageing期间或在特定的蛋白质剪接(例如，内蛋白切除) 期间自发环化。

## 分子胶
### 免疫调节的酰亚胺类药物Immunomodulatory imide drugs (IMiDs)
主要包括沙利度胺及衍生物（来那度胺、泊马度胺），其作为分子胶的**单亲性**体现在和E3 ligand（即CRBN）的结合上

沙利度胺及衍生物（来那度胺、泊马度胺）作为分子胶可靶向降解的蛋白质有：Ikaros 锌指蛋白 Ikaros (IKZF1) 、 Aiolos (IKZF3)、casein kinase 1A1 (CK1α)、translation factor GSPT1 (G1 to S phase transition 1)

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191903012-e751ac03-b66c-4b25-864c-4024ed823662.png" width="800">
</div>

GSPT1 shares no obvious homology to IKZF1,IKZF3, or CK1α and cannot be targeted for degradation by other IMiDs, such as lenalidomide and pomalidomide

### 芳基磺酰胺Aryl Sulfonamide
此药名曰：indisulam

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191905075-12e86fa2-3ab9-4017-af22-fd7f9cdf81ee.png" width="800">
</div>

E3 ligand为DCAF15，降解的靶蛋白为splicing factor RNA binding motif protein 39 (**RBM39**)

与 IMiD 不同，磺胺类药物是 DCAF15 的弱配体，与DCAF15的亲和力也不强，而 RBM39 与DCAF15的结合亲和力也很弱。但是Indisulam 能够在DCAF15表面诱导一个浅袋并增强两种蛋白质之间的 PPI（主要是非极性相互作用）。

### 直接到DDB1而绕过E3 ligand_CDK12/13:DDB1 glues trigger cyclin K degradation

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191904547-e8782f1d-247f-44b3-a3ea-20896cb6f89e.png" width="800">
</div>

最近出现了一种有趣的靶向蛋白质降解的替代机制，发现小分子可以将靶蛋白直接招募到 DDB1 衔接蛋白，绕过对专用底物受体的要求

CR8 通过含有 DDB1 的 cullin-RING 连接酶触发细胞周期蛋白 K 的选择性降解

## PROTAC
### 泛素
泛素化作为蛋白翻译后修饰（PTM）的方式之一，不仅参与蛋白质的降解，在调节细胞功能方面也发挥着重要作用

泛素为含76个氨基酸、大小约为8.6 kDa的小蛋白质，在真核生物中普遍存在且高度保守。人类基因组中的四个基因编码泛素：UBB，UBC，UBA52和RPS27A。

泛素氨基酸序列：
MQIFVKTLTGKTITLEVEPSDTIENVKAKIQDKEGIPPDQQRLIFAGKQLEDGRTLSDYNIQKESTLHLVLRLRGG

泛素具有7个赖氨酸残基（K6，K11，K27，K29，K33，K48，K63）和一个甲硫氨酸残基（M1）。泛素之间主要通过赖氨酸残基和甲硫氨酸残基进行各种连接。由此产生的泛素链产生一定的拓扑结构，可通过对蛋白底物进行修饰并决定底物的功能。
泛素蛋白的结构：

![image](https://user-images.githubusercontent.com/111955215/188146930-f1a3176b-1ee8-48e1-9ff7-53822411c14c.png)

泛素的功能位点：

![image](https://user-images.githubusercontent.com/111955215/188147023-32ccb586-94e3-42a0-a09e-e25f97fdc130.png)

泛素系统降解蛋白质的机制：

![image](https://user-images.githubusercontent.com/111955215/188147254-50b82ed7-c8d5-42d9-9096-6c0d24f828d4.png)

### PROTAC的优点
* 极大地扩展了可成药蛋白靶点的范围。目前已鉴定出超过4000种疾病相关蛋白但只有约10%被成功开发，许多蛋白由于结构复杂、没有活性位点等原因无法被传统抑制剂靶向，而PROTAC只要能结合目标蛋白就可以诱导降解，可大大拓展可成药靶点的范围。
* 传统小分子抑制剂只能阻断靶蛋白的部分功能，而PROTACs降解靶蛋白后可消除其所有功能。
* 传统的激酶抑制剂容易因靶蛋白突变或过度上调而耐药，但PROTAC可通过降解靶蛋白来最大限度减少潜在的耐药性。
* PROTAC理论上是可以循环使用的，因此催化剂量即可发挥作用，可提高药物的安全性。

### 应用
* 制备减毒活流感疫苗
将可以靶向VHL（E3 ligand）序列的一段序列TPD（序列为ALAPYIP）插入到病毒基因组，从而将相应的病毒蛋白靶向到泛素-蛋白酶体途径中进行降解；同时为方便生产，再引入一段TEVp序列（序列为ENLYFQG）特定的菌可以表达这种TEVp蛋白，从而将TPD这段序列切掉，因此病毒的基因组完整，正常复制，便于生产。

![image](https://user-images.githubusercontent.com/111955215/188148639-4bd07226-a478-4ab8-9b18-5514b29b5c64.png)

### E3 ligand
#### CRBN的lignand
沙利度胺（其实这几种也可以作为分子胶）：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191497823-0683ea0d-f24b-4c12-94d2-405283142865.png" width="400">
</div>

泊马度胺(沙利度胺衍生物)：

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191496847-fd5eecde-7da7-46c6-acad-ba583ac23c47.png" width="400">
</div>

来那度胺(沙利度胺衍生物)：
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/191497158-e2f5e5d5-ff81-4a95-ae46-04616430c7a0.png" width="400">
</div>

### 泛素-蛋白酶体系统
E3-E2之间的蛋白复合体有：E3(CRBN VHL MDM2 IAP DCAF15等) - DDB1 - CUL4A/B - N8 - RBX1 - E2
![image](https://user-images.githubusercontent.com/111955215/191650230-5621bd70-8deb-462c-b986-58972fdafe36.png)

## 溶酶体途径
![image](https://user-images.githubusercontent.com/111955215/188148140-5da3caae-dfe1-4a4b-9065-a64ed8686c1e.png)

# 关于肿瘤
## 肿瘤微环境 Tumor microenvironment
![1](https://user-images.githubusercontent.com/111955215/188036946-1f24a06e-7458-410c-96a9-3df616d4f2d4.png)

肿瘤微环境中**营养**和**氧气**的平衡控制着免疫细胞的功能：
* 肿瘤细胞对葡萄糖和氨基酸的消耗超过浸润免疫细胞，特别是剥夺它们的营养以促进其效应功能。氧气不足的肿瘤微环境会驱动肿瘤细胞、巨噬细胞和 T 细胞中的缺氧反应程序。
* 由于缺氧或其他机制而增加的 HIF-1a 活性促进糖酵解并增加抑制性代谢物的浓度和局部环境的酸化。
* 作为糖酵解的副产物，乳酸浓度增加，被肿瘤细胞协同利用以促进其代谢，促进巨噬细胞极化，并直接抑制 T 细胞功能。
* T细胞靶向肿瘤的能力进一步受限于它们对共抑制受体的上调以及与邻近肿瘤细胞和巨噬细胞上的配体的结合。随着 T 细胞逐渐进入功能失调状态，它们的线粒体质量和氧化能力下降，最终导致它们无法满足维持效应功能和控制肿瘤细胞生长的生物能量需求。


# 关于T细胞和细胞治疗

## T细胞受体信号
![image](https://user-images.githubusercontent.com/111955215/187328881-50cf2797-5fb7-42ca-a9f8-0013f3683008.png)

![image](https://user-images.githubusercontent.com/111955215/187206889-ab90a064-9beb-4b21-8674-b91f0b6d200d.png)

**关于Zap70**：
(A) Lck 和 Zap70 存在于严格的信号层次结构中。 (B) Zap70经历逐步激活，这需要将其募集到 TCR 复合物中的磷酸化免疫受体酪氨酸激活基序 (ITAM) 及其Lck 磷酸化。 (C) Zap70 包含一个对其底物特异性很重要的高度碱性区域。 Zap70 的基本区域充当静电过滤器确保对 LAT 和 SLP-76 中磷酸位点的特异性，并防止 ITAM 和 Zap70 激活环的磷酸化。 (D) Zap70 Y126 的磷酸化是建议使其从 TCR 复合物中释放，使其可以迁移并遇到 LAT 使其磷酸化。同时，额外的Zap70分子能够结合TCR复合物并被激活，表明 TCR 信号放大模式


### 动态隔离模型“size exclusion” model
 当 TCR 复合物与 pMHC 复合物结合后， 会与抗原提呈细胞之间形成免疫突触。动态隔离模型（kinetic segregation model）可描述为在免疫突触中， TCR 处于中心位置并形成“紧密结合区域”（close contact zones），进而排斥一些大分子蛋白，如磷酸酶 CD45 分子。这种机制最终导致的结果即为TCR/CD3 近端的激酶和磷酸酶平衡失调，从而使得 CD3 被磷酸化，促进 T 细胞活化和信号转导。在CAR 与靶细胞特异性表达抗原结合的表面，CD45 同样处于被排除状态以促进信号转导。因此，动态隔离模型在 CAR 信号中也许同样重要。
 
 天然的TCR长度是相对固定的，但是人工设计的Car的长度可以改变。有研究者提出Car的长度与激活的关系：Car足够短，才能在与抗原peptide和MHC结合时将CD45排除在外，有用的磷酸酶才可以过来将Car磷酸化，产生激活信号。
 
 ![image](https://user-images.githubusercontent.com/111955215/187327934-0a825e56-8dc3-419c-ba2e-3374665df2b7.png)

![image](https://user-images.githubusercontent.com/111955215/187329398-cfe0fe6c-d563-4975-94d6-75772768b771.png)
### 共受体扫描模型
低亲和力的抗原在共受体的扫描下会离去而不会导致信号通路激活。
Lck是一种丝氨酸蛋白激酶，位于胞内且可以和CD4/8共受体结合，其激活也依赖自身被磷酸化。Lck活化越多T细胞越容易被激活。

![image](https://user-images.githubusercontent.com/111955215/187329817-ddd641b8-1de3-4ea6-9d26-2d8527853d12.png)

### 动力学校对模型
![image](https://user-images.githubusercontent.com/111955215/187332536-1958948c-4cf1-4586-bbb8-e55fd973a40a.png)


### 串行参与模型（serial engagement model）
常与动力学校对机制并列提及。该模型阐述 TCR 与pMHC 达成紧密结合就像接力一样，即单个 pMHC 可与多个 TCR 进行连续性的接触，而这些连续性接触积累起来的结果，使得 TCR 与 pMHC 达到紧密结合，最终导致 T 细胞的完全活化

## Car-T
![123](https://user-images.githubusercontent.com/111955215/187198651-62752b2b-988d-4f0f-bd8b-037fbd688aeb.png)

按照每个元件所处的位置，CAR主要分为三个功能区域，分别是：胞外结构域 、 跨膜结构域 和 胞内结构域 。

![image](https://user-images.githubusercontent.com/111955215/187200834-9bd29eca-83bf-46e9-84c7-9b6ae890b38d.png)

胞外结构域由负责识别并结合抗原的单克隆抗体的单链可变片段（single-chain variable fragment，scFv）及一段起连接作用的铰链区（Hinge）构成。
scFv由单克隆抗体的轻链（VL）和重链（VH）通过多肽连接而成，保留有抗体对抗原的特异性和亲和力。CAR-T细胞通过scFv对靶抗原的识别结合不依赖MHC抗原呈递，一方面避免了肿瘤细胞通过调节MHC分子发生逃逸，另一方面赋予了CAR-T细胞识别非肽抗原的能力（虽然目前主要还是识别CD19）。

胞内结构域由共刺激结构域（Costimulatory Domain）和信号转导结构域（Signaling Domain）构成。

### Car-T的问题
* **无法深入实体瘤内部，因此对实体瘤作用效果差**：CAR对抗原的亲和力则是极其强大，有时强大到它和抗原拽都拽不开；因为强大的亲和力，CAR-T细胞常常阻滞在实体瘤的外周，而不像TCR-T那样毫无羁绊。同时许多实体瘤内部存在**异质性**，即会有不同类型的肿瘤细胞，这些细胞相互之间携带的抗原和表达水平都有所不同，如果CAR-T仅对部分肿瘤细胞有效，治疗就很难成功。肿瘤细胞适应了瘤内弱酸性、低氧、缺乏营养的**特殊肿瘤微环境**，同时还有不利于CAR-T细胞生存的抑制因子和抑制细胞。 
* **脱靶效应**：CAR-T靶向肿瘤相关抗原，并非肿瘤细胞特异性的，正常细胞也可能受到攻击
* **稳定性差**：引入的CAR受体为外源性分子，具有一定的免疫原性，机体会产生针对CAR的抗抗体，会影响CAR-T细胞的存活。此外CAR分子使用的scFV不稳定，容易发生自身聚集，引发CRS。

![1](https://user-images.githubusercontent.com/111955215/187201339-b35a7ff0-6634-448d-85c5-319ed79544fa.png)

## TCR-T
### 关于T细胞
![image](https://user-images.githubusercontent.com/111955215/187206889-ab90a064-9beb-4b21-8674-b91f0b6d200d.png)

### TCR与CAR的异同
![image](https://user-images.githubusercontent.com/111955215/187206729-806e37c9-03a0-49dc-b863-0961077517de.png)

不同于CAR-T细胞只能识别细胞膜外的蛋白质，TCR-T细胞的主要优势是能够识别细胞外和细胞内的蛋白，而超过85%的细胞蛋白位于细胞内，所以对于实体瘤，TCR-T可以发挥更好的作用。

TCR的效力依赖于它与肽-主要组织相容性复合体（pMHC）的相互作用，pMHC即为肽结合于MHC形成的复合物。来自T细胞的TCR必须与患者的人类白细胞抗原（HLA）等位基因匹配，识别这些pMHC并杀伤癌细胞。因此rTCR需要MLA和抗原同时表达，但是CAR-T直接识别膜蛋白

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187208815-1fc7ad11-0845-4a3b-8ea6-9a4c3d61273d.png" width="700">
</div>

总结如下：
<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187209038-c76e0355-7b17-4260-8156-fa358a07ba53.png" width="700">
</div>

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/187209528-ade34db8-c836-4908-aa16-795f5cd5281f.jpg" width="1500">
</div>


# 基因编辑
## Cas 13
Cas13a 是一种VI-A型CRISPR-Cas RNA引导的 RNA 核糖核酸酶，降解CRISPR RNA(crRNA)靶向的侵袭性RNA

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193724181-3090ceba-1439-4bbd-851c-922116690812.png" width="800">
</div>

其crRNA有一段repeat sequence，剩下的部分和target RNA形成RNA双链

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193725159-473ca881-4e43-4f2a-89ab-f2d8be2d9921.png" width="400">
</div>


### 用于检测

这个位于靶激活的 Cas13复合物外表面的催化囊可以非特异性地切割任何周围的 RNA 分子，产生特征性的“**附带效应**”(collateral effect)。这种靶向触发的侧支活动，最初是一种旨在诱导宿主休眠和防止侵入噬菌体繁殖的免疫防御机制，已经被迅速开发用于体外检测核酸分子。例如，Cas13-crRNA复合物在靶标识别时被激活，并进行由单链RNA(ssRNA)连接的附近染料猝灭剂对的侧切以快速产生可测量的荧光或比色信号（如下图）

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193726537-8241af81-80b2-478a-9f97-1c15aaacc906.png" width="1200">
</div>

#### 对比下Cas13a和Cas12

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193726479-219e6502-74a7-4890-8e2e-88c690e3df7e.png" width="800">
</div>

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193725974-5f45b122-9153-44ed-bd61-a510128f6fb0.png" width="800">
</div>

## 基于TALE的基因编辑

### 用TALE蛋白与脱氨酶DddA组成碱基编辑器
2018年，de Moraes发现DddA具有催化胞嘧啶脱氨转变为尿嘧啶的活性，而且有意思的是，与其他的脱氨酶不同，这种作用可以直接在DNA双螺旋上发生，不需要解旋。

Bacterial toxin DddA-derived cytosine base editors (DdCBEs)—composed of split DddAtox (a cytosine deaminase specifc to double-stranded DNA), custom-designed TALE (transcription activator-like efector) DNA-binding proteins, and a uracil glycosylase inhibitor。其可直接针对双链DNA将C-G碱基对编辑为T-A碱基对，而且编辑效率很高，也几乎没有脱靶效应

该技术可以用于解决线粒体DNA的编辑问题（Cas9解决不了）：要想解旋DNA，就得带上Cas9酶；可带上了Cas9酶，就进不去线粒体

要实现该方法还需要解决三个问题：
* 毒性：胞苷脱氨酶对哺乳动物细胞来说是有生物毒性的。为了避免这种毒性，研究者们想出的办法是把DddA一拆两半，两个没有活性的部分在编辑位点重组恢复脱氨活性
* 进线粒体的膜：加上线粒体靶向信号（MTS）蛋白序列，就能够利用线粒体的蛋白质吸收机制穿过线粒体的双层膜了
* 为了保住DddA的作用不被干扰，还要再加上尿嘧啶糖基化酶抑制剂（UGI），把U保住

![image](https://user-images.githubusercontent.com/111955215/196023581-2a80e559-4e82-4d56-aa38-8d6cf7d7a47b.png)

仍然存在的问题：该技术在不破坏DNA的情况下将一个核苷酸碱基转换为另一个核苷酸碱基。然而，这种技术也有其局限性。它不仅局限于C→T转换，而且大多局限于TC基序，使它实际上成为TC→TT转换器。这意味着它只能纠正90个确认的致病性线粒体点突变中的9个（10%）。

### 韩国人在DdCBE的基础上开发TALED
<a href="https://www.cn-healthcare.com/articlewm/20220429/content-1346554.html/">新型线粒体碱基编辑器</a>

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
Cas12a，也叫Cpf1，会切割顺式的目标DNA和反式的非目标单链 DNA (ssDNA) 

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/c16c6e1f-f578-412e-885a-591f935ee4c7" width="400">
</div>

**文献见下链接**
<a href="https://www.sciencedirect.com/science/article/pii/S1097276518309912?via%3Dihub">Mechanistic Insights into the cis- and trans-Acting DNase Activities of Cas12a</a>

Cas12在远离PAM序列的位置产生切割，且只有RuvC进行切割，导向核酸也是crRNA而不是gRNA（也就是说不需要tracrRNA，只用crRNA的反向互补的那点就够了）；Cas12核酸酶通常产生交错切割，这与Cas9的blunt切割不同。**Cas12a**通常使用富含T的PAM，这与大多数 Cas9的PAM不同。一般而言，Cas12a 变异体已被报道与许多 Cas9直系同源物相比产生少量脱靶编辑事件。

![image](https://user-images.githubusercontent.com/111955215/194810928-dcf231b9-e23a-4914-b844-51236b49da06.png)

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

#### ACBE

刘如谦团队在2023年6月又开发了一种ABE，可以实现从AT-CG的，这个过程和以往的AT-GC不同

<a href="https://www.nature.com/articles/s41587-023-01821-9">Adenine transversion editors enable precise, efficient A•T-to-C•G base editing in mammalian cells and embryos</a>

以前的碱基编辑策略比较有限：

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/1aead431-407a-4361-ba05-9516720c18e8" width="500">
</div>

但实际上各种碱基突变的情况都有：

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/c2cbeea0-d721-45c4-b3f6-0c0be3ddf966" width="500">
</div>

主要的原理就是在以往的TadA8e的基础之上进化了另一种糖基化酶，可以把突变后的I碱基给踢掉，而之后会被修复成为嘧啶，那么无论是修复成为T还是C，都可以达成目标：修复成为C，达成；修复成为T，则相当于AT-TA，之后再来一次脱氨反应，则TA-CG，相当于AT-CG，达成。

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/c90c4f0a-2af1-45f4-9977-b7276b151776" width="500">
</div>

<div align=center>
<img src="https://github.com/DearJohnsonny/Notes2-Biotech/assets/111955215/2cb71ec5-e291-4280-ac02-6ff908b2f794" width="500">
</div>


#### 常见的碱基编辑器的序列

![image](https://user-images.githubusercontent.com/111955215/187112477-2167805c-ee39-41fa-9d54-0ce374340e1c.png)

#### 碱基编辑器的选择
碱基编辑器可以根据几个标准来选择，包括所需的编辑(C•G-to-T•A或A•T-to-G•C)，目标序列中合适的 PAM 的可用性，围绕目标核苷酸的序列基序，目标核苷酸在原型间隔区内的位置，不希望的旁观者突变的可能性以及需要尽量减少脱靶DNA或RNA编辑。该流程图可以指导候选基本编辑器的识别。根据应用程序的不同，一些标准将优先于其他标准，可能需要在效率和特定性之间进行权衡。SpCas9 CBE 的标准编辑窗口通常是原型间隔区位置4-8，对于SaCas9 CBE 是位置3-12，对于 Cas12a CBE 是位置8-13。SpCas9 ABEs 的标准编辑窗口通常是原型间隔区位置4-7，对于 SaCas9 ABEs 是位置6-12，对于 Cas12a ABEs 是位置8-13。

![image](https://user-images.githubusercontent.com/111955215/187060579-48a2284c-6ca5-4a66-87a0-bb3583a00b04.png)

### Cas相关的转座酶
Tn7样转座子通常含有 tnsA、 tnsB、 tnsC、 tnsD 和 tnsE 基因，以及其他遗传货物。通常，TnsA 和 TnsB 形成特异性识别左端(LE)和右端(RE)基序的 TnsAB 复合物，其侧翼转座子并催化从供体基因座切除转座子。TnsB 是逆转录病毒整合酶超家族的成员，并催化磷酸二酯骨架的3’切割，而 FokI 样蛋白 TnsA 随后催化5’末端的切割。然后，TnsB 将转座子 DNA 的游离3’末端连接到由 TnsD 或 TnsE 底物分配结构域确定的靶 DNA 底物，在5’连接处留下小的间隙。这些缺口的修复导致特征性的5-bp 目标位点重复。TnsC 是一种与 TnsAB 复合物、双链 DNA 和 TnsD 或 TnsE 中的一种相互作用的 ATP 酶

Cas 转座酶包括 Cas 蛋白和转座酶相关组分。Cargo DNA 由其左端(LE)和右端(RE)序列鉴定，并与转座酶蛋白(Tns)结合。Cas 蛋白以 PAM 依赖的 RNA 定向方式定向到感兴趣的靶基因座。Cas 结合将转座酶蛋白定位到感兴趣的目标序列，并促进目标位点的Cargo DNA整合进入基因组。

### Prime editting
以前的技术要么一次只改变一个碱基，要么是需要引入修复模版。通过将具有双重功能的融合蛋白（脱氨酶活性和内切酶活性）和经过修饰的RNA结合起来，Prime Editing允许引入所有突变类型，包括插入、缺失和12种碱基-碱基转换

![image](https://user-images.githubusercontent.com/111955215/187614760-9750f2d6-7a62-4413-ab4c-d0c835d26364.png)

![image](https://user-images.githubusercontent.com/111955215/187591916-f67a0f9e-bedc-4517-a7a2-41cdc40fc6c7.png)

在这个新方法中，sgRNA被prime editing guide RNA (pegRNA)取代，pegRNA不仅驱动内切酶，还包含引物结合位点(primer binding site, PBS)区域。PBS区域引入可以和逆转录酶(RT)结合序列，并以pegRNA的序列作为模板直接从pegRNA复制信息来引入到目标序列中。这种技术在人类细胞中可以引进12个点突变，实现范围是PAM上游3bp到下雨29 bp，插入达44 bp，缺失达80 bp。值得注意的是，Prime Editing的效率与碱基编辑器相似，但特异性比以往系统更高。特异性提高的原因是以往的CRISPR/Cas系统中，只有一种杂交即sgRNA与靶DNA的杂交。而在Prime Editing系统中，有三种杂交事件:靶DNA和pegRNA的间隔序列之间的杂交;目的DNA与PBS之间的杂交;靶DNA与RT产物之间的杂交。（但是效率更低）

![image](https://user-images.githubusercontent.com/111955215/187591887-eb8379b6-a3e4-4ad8-952a-de50ab7c5e0c.png)

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193016887-8b69d823-7dc4-44a3-b634-86360e2dfdcc.png" width="1500">
</div>

#### 关于提高prime editing的编辑效率
研究者利用indel的MMR(mismatch repair)效率高于base-base的效率，开发了一种能提高base-base的prime editing效率的方法，即引入更多的同义突变(same-sense mutaion,ssm)，从而使得细胞的MMR从base-base变成indel repair，从而提高效率；而SSM又不会改变最终的蛋白表达，其转录组情况也得到验证为安全。对于不同的ORF，应该选择不同的突变策略。

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193042058-2e4c9c5e-b47b-4357-9731-070213cf32ad.png" width="1000">
</div>

<div align=center>
<img src="https://user-images.githubusercontent.com/111955215/193041244-659dd8a0-c644-42ed-987f-fa833b96a3d8.png" width="800">
</div>

## crispr工具的补充-迷你核酸酶IscB和TnpB
来自于IS200/605转座子家族的IscB和TnpB，它们在微生物中广泛分布，被认为是CRISPR/Cas9和Cas12系统的起源。它们的最大特点是非常短的CDS序列，在1.2kb左右，体积不到spCas9的1/3，留下了**巨大的改造空间**。
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

PAM（protospacer adjacent motif）序列是Cas9或Cas12核酸酶启动DNA切割所必须的，那么TnpB发挥作用可能也需要类似的序列。通过PAM鉴定实验，作者观察到在目标基因5’端上游富集了大量的**TTGAT**序列，并称之为**Transposon Associated Motif (TAM)**。体外DNA切割实验证实**TnpB具备RNA引导的靶向dsDNA的核酸酶活性**。进一步分析发现，将TnpB序列中的RuvC-like活性位点突变后，TnpB失去了切割能力，说明RuvC模块与TnpB的活性相关。研究人员发现实现TnpB的DNA切割功能需要同时满足两个条件：（1）TAM序列；（2）与靶基因匹配的位于reRNA 3’端的序列。

TnpA 介导的 ISDra2的“剥离和粘贴”转座机制。TnpA 二聚体在 DNA 复制过程中催化从滞后链切除转座子，形成环形单链 DNA 中间体和供体关节。切除的转座子圆在受体连接处插入落后的 DNA 链3′至 TTGAT 序列，完成转座周期。转座子切除/插入位点用红色三角形标记。
![image](https://user-images.githubusercontent.com/111955215/187118202-db16d521-124d-42f6-8dee-543945e0a835.png)


随后，作者对切割产物进行了测序分析，结果显示，TnpB采取的是一种交错切割模式，在NTS（non-target strand）的多个位置和 TS (target strand) 的单个位置进行切割，最终产生5’-悬挂端（overhangs）

![image](https://user-images.githubusercontent.com/111955215/187118227-4f60f867-c9ea-45a2-8062-9772c22aad24.png)
