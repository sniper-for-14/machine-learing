# machine-learing
模式：可以用关联规则的形式表示
  
  支持度和置信度是规则兴趣度的两种度量，他们分别反映规则的有用性和确定性
  
  有趣的：如果他满足最小支持度阈值和最小置信度阈值
    
    computer=>antivirus_software[ support=2% ; confidence=60% ]

频繁项集：如果项集I的相对支持度满足预定义的最小支持度阈值，则I是频繁项集
    
    confidence(A=>B)=P(B|A)=support(AUB)/support(A)=support_count(AUB)/support_count(A)
    
    由频繁项集产生强关联规则：根据定义，这些规则必须满足最小支持度和最小置信度
     
闭频繁项集：
    项集X在数据集D中是闭的，如果不存在真超项集Y是的Y与X在D中具有相同的支持度计数，而且X是频繁地，则X是数据集D中的闭频繁项集。
   
极大频繁项集（极大项集）：
    如果X是频繁地，并且不存在超项集Y使得X含于Y并且Y在D中是频繁地
    
Apriori算法：————频繁项集的挖掘
    Apriori算法是一种称为逐层搜索的迭代方法，期中k项集用于探索（k+1）项集。
    
    先验性质：频繁项集的所有非空子集也一定是频繁的
    即如果一个集合不能通过测试，则他的所有超集也都不能通过相同的测试  ————  反单调性
    
code：
  D:事务数据库
  min_sup:最小支持度阈值
  输出：L,D中的频繁项集
  
  L1=find_frequent_1_itemsets(D)
  for(k=2;L(k-1)><NULL;k++){
    C(k)=aproiri_gen(K(k-1));
    for each事物t属于D
    {
      C(t)=subset(C(k),t);
      for each 候选c属于C（t）
      c.count++;
    }
    L(k)={c属于C（K）|c.count>=min_sup}
  }
  return L=U(k)L(k)
procedure apriori_gen(L(k-1:frequent(k-1)itemset))
    for each项集l（1）属于L（k-1）
      for each项集l（2）属于L（k-1）
        if （(l（1）[1]=l(2)[1])^(l（2）[1]=l(2)[2])^……^(l（1）[k-2]=l(2)[k-2])^(l（1）[k-1]><l(2)[k-1])）then{
        c=l(1)链接l(2)
        if has_infrequent_subset(c,K(k-1))then
          delete c
        else add c to C(k)
        }
      return  C(k)
