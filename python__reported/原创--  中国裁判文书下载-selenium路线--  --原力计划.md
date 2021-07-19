# 原创

： 中国裁判文书下载：selenium路线 ：

原力计划

# 中国裁判文书下载：selenium路线

### 中国裁判文书下载：selenium路线

成功现状：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200605182147178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 一、requests路线

requests路线需要对js进行解密，对js解密时遇到三个参数

```
docid
cipher
__RequestVerificationToken

```

这三个参数主要是针对文书列表页面的<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200605174601208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
试图在这个页面获取相应的链接，<br/> js解密后，其中ciphertext参数需要感谢大神：越学越害怕<br/> 后面的docid和__RequestVerificationToken都非常简单

但是将这些参数传入后，请求仍然出现状态码202或者状态码200但是内容为None<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200605175347154.png"/>

最后放弃了requests路线

# 二、selenium路线

## 问题一：namespace error 命名空间错误

参见《selenium的namespace错误与无法定位：NamespaceError: An attempt was made to create…andUnable to locate
elemen》，链接: [link](https://blog.csdn.net/python__reported/article/details/106402222).

虽然原因不明，不知道为什么报这个错误，但是这个错误与标签有关，只要不是特殊标签即可<br/> 如果存在特殊标签，比如裁判文书网中的下面这个元素的初始标签：diy:lawyee

```
&lt;diy:lawyee id="_view_1545184311000" var-name="_var_name_1545184311000" style="display: inline;"&gt; &lt;div class="LM_con clearfix" style="background: none;"&gt; &lt;div class="fl con_left clearfix" style="display: none;"&gt; &lt;a href="../181217BMTKHNT2W0/index.html"&gt; &lt;/a&gt; &lt;a id="chartListBtn" href="javascript:;"&gt; &lt;/a&gt; &lt;/div&gt; &lt;div class="fr con_right"&gt;共检索到 &lt;span&gt;1559125&lt;/span&gt; 篇文书，显示前600条&lt;/div&gt; &lt;/div&gt; &lt;div class="LM_tool clearfix"&gt; &lt;div class="fl tool_PX tool_On" data-value="s50"&gt; &lt;a href="javascript:;"&gt;法院层级&lt;/a&gt; &lt;/div&gt; &lt;div class="fl tool_PX " data-value="s51"&gt; &lt;a href="javascript:;"&gt;裁判日期&lt;/a&gt; &lt;/div&gt; &lt;div class="fl tool_PX " data-value="s52"&gt; &lt;a href="javascript:;"&gt;审判程序&lt;/a&gt; &lt;/div&gt; &lt;!-- &lt;div class="fl tool_PX " data-value="s52"&gt; &lt;a href="javascript:;"&gt;审判程序&lt;/a&gt; &lt;/div&gt; --&gt; &lt;div class="fr tool_All"&gt; &lt;a class="AllSelect" href="javascript:;"&gt;&lt;input type="checkbox" id="AllSelect"&gt;&lt;label for="AllSelect"&gt;全选&lt;/label&gt;&lt;/a&gt; &lt;a class="AllKeep" href="javascript:;"&gt;批量收藏&lt;/a&gt; &lt;a class="AllDownload" href="javascript:void(0);"&gt;批量下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt;   &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 刑事复核 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="3dc5113e6389402aafbeab200113faf6"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=3dc5113e6389402aafbeab200113faf6" class="caseName" target="_blank"&gt;刘永权抢劫在法定刑以下量刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;中华人民共和国最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;（2019）最高法刑核87677387号&lt;/span&gt; &lt;span class="cprq"&gt;2019-10-29&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，原审被告人刘永权以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采取暴力手段强行劫取他人财物，其行为已构成抢劫罪，且属于入户抢劫。刘永权虽不具有法定减轻处罚情节，但其犯罪情节较轻，并能如实供述罪行，认罪态度较好，且已将...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="3dc5113e6389402aafbeab200113faf6" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="3dc5113e6389402aafbeab200113faf6" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 刑事审判监督 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="21e9f0002d8c4d29baf6aabf00c11a3c"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=21e9f0002d8c4d29baf6aabf00c11a3c" class="caseName" target="_blank"&gt;徐国庆 贪污罪 驳回申诉通知书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;（2019）最高法刑申230号&lt;/span&gt; &lt;span class="cprq"&gt;2019-08-14&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院经审查认为，你利用担任河南省宁陵县国有林场场长的职务便利，隐瞒已用林场债权顶抵部分应付款项的事实，多列支出予以报销，&lt;span style="color:red"&gt;非法占有&lt;/span&gt;公款25200元。原审认定你犯贪污罪的事实清楚，证据确实、充分，定罪准...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="21e9f0002d8c4d29baf6aabf00c11a3c" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="21e9f0002d8c4d29baf6aabf00c11a3c" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 刑事审判监督 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="06d6f4b4fa2644708563aa8601126387"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=06d6f4b4fa2644708563aa8601126387" class="caseName" target="_blank"&gt;抢劫刑事决定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;（2017）最高法刑申407号&lt;/span&gt; &lt;span class="cprq"&gt;2019-07-05&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，原审法院认定申诉人刘十民因成某的丈夫冉某勇盗窃其财物，使用暴力拉走成某所收废品的事实清楚，证据确实充分。刘十民所提成某同意其拉走废品和没有使用暴力的申诉理由不成立。鉴于：（1）冉某勇盗窃刘十民的财物，负有返还财产、赔偿损失的义务。成某所收购的废品，属...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="06d6f4b4fa2644708563aa8601126387" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="06d6f4b4fa2644708563aa8601126387" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="143b5d3f9ba64acfae8eaa9a00beb973"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=143b5d3f9ba64acfae8eaa9a00beb973" class="caseName" target="_blank"&gt;赵志红故意杀人、强奸案死刑复核裁定&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-07-02&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为,被告人赵志红故意非法剥夺他人生命，其行为已构成故意杀人罪；违背妇女意志，采用暴力、胁迫等手段强奸妇女，其行为已构成强奸罪；以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采用暴力、胁迫手段劫取他人财物，其行为又构成抢劫...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="143b5d3f9ba64acfae8eaa9a00beb973" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="143b5d3f9ba64acfae8eaa9a00beb973" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="3e068515464d4e03a68eab2700dc9b5e"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=3e068515464d4e03a68eab2700dc9b5e" class="caseName" target="_blank"&gt;王洪喜抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-06-18&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人王洪喜以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采用暴力手段劫取他人财物，并致人死亡，其行为已构成抢劫罪。犯罪性质恶劣，情节、后果严重，社会危害性大，应依法惩处。第一审判决、第二审裁定认定的事实清楚，证据确...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="3e068515464d4e03a68eab2700dc9b5e" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="3e068515464d4e03a68eab2700dc9b5e" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="b8f6b6fe813945109411ab1b00a5d177"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=b8f6b6fe813945109411ab1b00a5d177" class="caseName" target="_blank"&gt;刘乐抢劫、故意杀人死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-06-03&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人刘乐以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采取杀人的暴力手段劫取他人财物，其行为已构成抢劫罪；刘乐故意非法剥夺他人生命，其行为构成故意杀人罪，应依法并罚。刘乐沉迷赌博，杀害妻子，情节恶劣，后果严重；其杀...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="b8f6b6fe813945109411ab1b00a5d177" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="b8f6b6fe813945109411ab1b00a5d177" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="8051cc11053748f7b85cab0901177455"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=8051cc11053748f7b85cab0901177455" class="caseName" target="_blank"&gt;于京平抢劫、强奸死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-04-09&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人于京平以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采用暴力手段劫取他人财物，又强行与被害人发生性关系，其行为已构成抢劫罪和强奸罪，应依法数罪并罚。于京平在抢劫过程中为制服被害人反抗，用随身携带的斧子多次击打被...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="8051cc11053748f7b85cab0901177455" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="8051cc11053748f7b85cab0901177455" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="341ef75432434ac29b87ab0901177549"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=341ef75432434ac29b87ab0901177549" class="caseName" target="_blank"&gt;贾谦龙抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-04-01&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人贾谦龙以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采用暴力手段劫取他人财物，其行为已构成抢劫罪。贾谦龙预谋抢劫，当场杀害一名被害人，犯罪手段残忍，情节、后果严重，罪行极其严重，应依法惩处。第一审判决、第二审裁...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4&gt;[关联文书]&lt;/h4&gt;   &lt;div class="guanLian"&gt; &lt;span&gt;本篇&lt;/span&gt;&lt;b&gt;&lt;/b&gt; &lt;a href="../181107ANFZ0BXSK4/index.html?docId=341ef75432434ac29b87ab0901177549" target="_blank" title=""&gt;&lt;i class="guanlianAnyou"&gt;其他&lt;/i&gt;&lt;i&gt;最高人民法院 &lt;/i&gt;&lt;i&gt;无&lt;/i&gt;&lt;i&gt;2019-04-01&lt;/i&gt;&lt;i&gt;&lt;/i&gt;&lt;/a&gt; &lt;/div&gt;  &lt;div class="guanLian"&gt; &lt;span&gt;&lt;/span&gt;&lt;b&gt;&lt;/b&gt; &lt;a href="../181107ANFZ0BXSK4/index.html?docId=97fe25f949ee4d5fb136a9d300113d78" target="_blank" title=""&gt;&lt;i class="guanlianAnyou"&gt;刑事二审&lt;/i&gt;&lt;i&gt;河北省高级人民法院 &lt;/i&gt;&lt;i&gt;（2018）冀刑终249号&lt;/i&gt;&lt;i&gt;2018-09-13&lt;/i&gt;&lt;i&gt;&lt;/i&gt;&lt;/a&gt; &lt;/div&gt;  &lt;div class="guanLian"&gt; &lt;span&gt;&lt;/span&gt;&lt;b&gt;&lt;/b&gt; &lt;a href="../181107ANFZ0BXSK4/index.html?docId=fe7964f3f00a42c7ac04ab2700b109e2" target="_blank" title=""&gt;&lt;i class="guanlianAnyou"&gt;刑事一审&lt;/i&gt;&lt;i&gt;河北省邯郸市中级人民法院 &lt;/i&gt;&lt;i&gt;（2018）冀04刑初2号&lt;/i&gt;&lt;i&gt;2018-03-28&lt;/i&gt;&lt;i&gt;判决&lt;/i&gt;&lt;/a&gt; &lt;/div&gt;  &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="341ef75432434ac29b87ab0901177549" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="341ef75432434ac29b87ab0901177549" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="fb5ecd6b76fd4709b0f4ab0e00c35e20"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=fb5ecd6b76fd4709b0f4ab0e00c35e20" class="caseName" target="_blank"&gt;张治刚抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-04-01&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人张治刚以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，伙同他人采用暴力手段劫取财物，其行为已构成抢劫罪。张治刚伙同他人经预谋后抢劫无证营运出租车，不顾司机求饶将其杀害，并为掩盖罪证抛尸枯井，犯罪情节恶劣，手段残忍...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="fb5ecd6b76fd4709b0f4ab0e00c35e20" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="fb5ecd6b76fd4709b0f4ab0e00c35e20" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="5b12fee3ad674bb189d7aaf501095b44"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=5b12fee3ad674bb189d7aaf501095b44" class="caseName" target="_blank"&gt;张斌抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-03-31&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人张斌以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采取暴力手段劫取他人财物，其行为已构成抢劫罪。张斌持械入户抢劫并致人死亡，犯罪情节特别恶劣，后果严重，实属罪行极其严重，应依法惩处。第一审判决、第二审裁定认定的...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="5b12fee3ad674bb189d7aaf501095b44" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="5b12fee3ad674bb189d7aaf501095b44" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="76646deadbd2432e8f0eaaf501095bd8"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=76646deadbd2432e8f0eaaf501095bd8" class="caseName" target="_blank"&gt;赵晏飞抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-03-22&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人赵晏飞以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，以暴力手段入户劫取他人财物，致一人死亡，其行为已构成抢劫罪。赵晏飞经预谋，深夜入户抢劫，并持刀捅刺被害人颈部致被害人死亡，犯罪手段残忍，后果严重，情节特别恶劣...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="76646deadbd2432e8f0eaaf501095bd8" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="76646deadbd2432e8f0eaaf501095bd8" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="becc9a11b4bd4696a424aaf501095bc1"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=becc9a11b4bd4696a424aaf501095bc1" class="caseName" target="_blank"&gt;谷宪武抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-03-12&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人谷宪武以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，使用暴力劫取他人财物，其行为已构成抢劫罪。谷宪武因赌博输钱而实施抢劫,并杀害被害人，犯罪动机卑劣，情节特别恶劣，实属罪行极其严重，应依法惩处。原审判决、高级人...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="becc9a11b4bd4696a424aaf501095bc1" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="becc9a11b4bd4696a424aaf501095bc1" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 其他 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="88b891c7c7c74f0d954caaf701657b09"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=88b891c7c7c74f0d954caaf701657b09" class="caseName" target="_blank"&gt;高中强抢劫死刑复核刑事裁定书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;无&lt;/span&gt; &lt;span class="cprq"&gt;2019-01-30&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，被告人高中强以&lt;span style="color:red"&gt;非法占有&lt;/span&gt;为目的，采用暴力手段劫取他人财物，其行为已构成抢劫罪。高中强抢劫并致人死亡，犯罪手段残忍，犯罪情节特别恶劣，实属罪行极其严重，应依法惩处。第一审判决、第二审裁定认定的...&lt;/p&gt; &lt;/div&gt;  &lt;div class="list_Association"&gt;  &lt;h4 style="height: 40px;"&gt;&lt;/h4&gt;   &lt;/div&gt; &lt;div class="List_label2 clearfix"&gt; &lt;div class="fr"&gt; &lt;a data-value="88b891c7c7c74f0d954caaf701657b09" class="a_sc" href="javascript:void(0)"&gt;&lt;i class="fa fa-heart-o"&gt; &lt;/i&gt; 收藏&lt;/a&gt; &lt;a data-value="88b891c7c7c74f0d954caaf701657b09" class="a_xz" href="javascript:void(0)"&gt;&lt;i class="a_xzBox"&gt;&lt;/i&gt; 下载&lt;/a&gt; &lt;/div&gt; &lt;/div&gt; &lt;/div&gt;  &lt;div class="LM_list"&gt; &lt;div class="List_label clearfix"&gt; &lt;div class="labelOne"&gt;&lt;img src="../images/list/one.png"&gt;&lt;/div&gt; &lt;div class="labelTwo"&gt; 刑事再审 &lt;/div&gt; &lt;div class="labelThree"&gt;&lt;img src="../images/list/three.png"&gt;&lt;/div&gt; &lt;!-- &lt;span class="on_1"&gt;推荐案例&lt;/span&gt; --&gt;     &lt;/div&gt; &lt;div class="list_title clearfix"&gt; &lt;a class="AllSelect" href="javascript:void(0)"&gt;&lt;input type="checkbox" class="ListSelect" data-value="971d62400160436aaefda9df0112219c"&gt;&lt;/a&gt;  &lt;h4&gt;&lt;a href="../181107ANFZ0BXSK4/index.html?docId=971d62400160436aaefda9df0112219c" class="caseName" target="_blank"&gt;赵明利诈骗再审刑事判决书&lt;/a&gt;&lt;/h4&gt; &lt;/div&gt; &lt;div class="list_subtitle"&gt; &lt;span class="slfyName"&gt;最高人民法院&lt;/span&gt; &lt;span class="ah"&gt;（2018）最高法刑再6号&lt;/span&gt; &lt;span class="cprq"&gt;2019-01-03&lt;/span&gt; &lt;/div&gt; &lt;div class="list_reason"&gt;  &lt;h4&gt;[裁判理由]&lt;/h4&gt;  &lt;p&gt;本院认为，原审被告人赵明利在与东北风冷轧板公司的冷轧板购销交易过程中，主观上没有&lt;span style="color:red"&gt;非法占有&lt;/span&gt;的目的，客观上亦未实施虚构事实、隐瞒真相的行为，其行为不符合诈骗罪的构成要件，不构成诈骗罪。理由如下：.......... &lt;/diy:lawyee&gt;

```

只要出现这种特殊标签就会报namespace error

## 问题二：元素的动态变化

主要是下一页这个元素，这个元素会动态变化<br/>
第一页的下一页元素为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020060518045578.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
//*[@id="_view_1545184311000"]/div[18]/a[8]

```

第二页的元素为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200605180524115.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
//*[@id="_view_1545184311000"]/div[18]/a[9]

```

由a[8]变为a[9]

一开始试图通过，对于翻页的次数的变化进行更新，但是失败了，失败原因在于只显示前600份裁判文书，但是由于限定条件的不同，查找的裁判文书数量就不同，导致不好判断<br/> 思路是这样的：

```
# 下一页xpath：
            '''
             if 7&lt;=index &lt;36:
                try:
                    button1 = wait.until(EC.presence_of_element_located((By.XPATH, '//div[@class="left_7_3"]/a[14]')))#问题并不是全为a8
                    time.sleep(1)
                    button1.click()
                except:
                    pass

            elif 36 &lt;= index &lt; 40:
                try:
                    button1 = wait.until(EC.presence_of_element_located((By.XPATH, '//div[@class="left_7_3"]/a[%d]' % int(
                        49-index))))
                    time.sleep(1)
                    button1.click()
                except:
                    pass
            elif index ==40:
                pass
            '''

```

然后试图通过分段函数进行解决，就是提取查找到的文书数量计算要翻的页数：

```
"""目的：减少遍历次数"""
        time.sleep(1)
        condition = browser.find_element_by_xpath('//div[@class="LM_con clearfix"]/div[@class="fr con_right"]/span')
        print(condition.text)  # 不能直接//text()原因不明
        conditions = math.ceil(int(condition.text) / 15)  # 最长12，最短6
        print(conditions)

```

但是还是不成功！！！！

最后突然想到，下一页 这个元素正好是最后一个元素可以直接使用xpath语法选中最后一个

```
button_ = wait.until(EC.presence_of_element_located((By.XPATH, '//div[@class="left_7_3"]/a[last()]')))
button_.click()

```

## 问题三、只显示前600份裁判文书

需要爬所有，但是只显示前600份<br/> ，没有办法直接爬取所有，因为裁判文书网限定了只显示前600份

解决方法：通过限定搜索条件如：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200605181459274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这个方法是某个博主（暂时想不起来）给的思路，这个博主是通过北京市的律师来限定的，但是我没有找到律师的名字，所有我是通过限定区域，如xx区县<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200605181707403.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

准确说这样，还是有问题，某些区县仍然超过600，但是相对较少了，即使超过了也不多，通过设置筛选可以进一步等待后续处理，如：

```
"""目的：减少遍历次数"""
        time.sleep(1)
        condition = browser.find_element_by_xpath('//div[@class="LM_con clearfix"]/div[@class="fr con_right"]/span')
        print(condition.text)  # 不能直接//text()原因不明
        conditions = math.ceil(int(condition.text) / 15)  # 最长12，最短6
        print(conditions)
        if int(condition.text) &gt; 600:
            with open('超过600页.txt','a+',encoding='utf-8')as file:
                file.write('出现超过600条的裁判文书,其所在区域为：'+ str(i.strip()) +'，其数量为：'+str(condition.text) + '\n')
            logging.warning('出现超过600条的裁判文书,其所在区域为：'+ str(i.strip()) +'，其数量为：'+str(condition.text))

```

## 问题四：弹出框的处理

参见《selenium弹窗之windows下载文件弹窗点击方法》 ，使用pyautogui进行键鼠自动化

但是据说还有selenium的内部方法

```
"""下载无弹窗
profile = webdriver.FirefoxProfile()
profile.set_preference('browser.download.dir', '‪I:\\360下载\\firefox')
profile.set_preference('browser.download.folderList', 2)
profile.set_preference('browser.download.manager.showWhenStarting', False)
profile.set_preference('browser.helperApps.neverAsk.saveToDisk', 'application/zip')
"""

```

但是不知道为什么我的不行，所以注释掉了

# 三、selenium路线的缺陷

有两个缺陷，一个是速度慢，另一个是弹出框暂时没有办法解决<br/> 后续可能需要使用scrapy+selenium，以及使弹出框不在弹出
