# mahout入门示例

## 推荐系统简介
### 运行第一个推荐引擎

1. 创建示例数据
1,101,5.0
1,102,3.0
1,103,2.5
2,101,2.0
2,102,2.5
2,103,5.0
2,104,2.0
3,101,2.5
3,104,4.0
3,105,4.5
3,107,5.0
4,101,5.0
4,103,3.0
4,104,4.5
4,106,4.0
5,101,4.0
5,102,3.0
5,103,2.0
5,104,4.0
5,105,3.5
5,106,4.0

保存为文件intro.csv, 文件格式为逗号分隔的三列, 分别为user ID, item ID, user对item的打分.假设这是一个用户对书本的打分记录, 经过一些学习之后，趋势就显现出来了。用户1和用户5具有相同的兴趣。他们都喜欢101这本书，对102的喜欢弱一些，对103的喜欢更弱。同 理，用户1和4具有相同的兴趣，他们都喜欢101和103，没有信息显示用户4喜欢102。另一方面，用户1和用户2的兴趣好像正好相反，用户1喜欢 101，但用户2讨厌101，用户1喜欢103而用户2正好相反。用户1和3的交集很少，只有101这本书显示了他们的兴趣。

2. 创建一个maven工程
在pom文件中加入mahout的依赖

        <dependency>
            <groupId>org.apache.mahout</groupId>
            <artifactId>mahout-core</artifactId>
            <version>0.7</version>
        </dependency>

下面是第一个推荐器的代码,

    public static void main(String[] args) throws Exception {
        String recsFile = "intro.csv";
        DataModel model = new FileDataModel(new File(recsFile)); // A

        UserSimilarity similarity = new PearsonCorrelationSimilarity(model);
        UserNeighborhood neighborhood = new NearestNUserNeighborhood(2, similarity, model);

        Recommender recommender = new GenericUserBasedRecommender(model, neighborhood, similarity); // B

        List<RecommendedItem> recommendations = recommender.recommend(1, 1); // C

        for (RecommendedItem recommendation : recommendations) {
            System.out.println(recommendation);
        }

    }


A 加载数据文件
B 创建推荐系统引擎Create the recommender engine
C 对user1, 推荐一个item

我们可以总结一下每个模块所扮演的角色。DataModel存储了所有的偏好信息，提供了对user 和item信息的访问。UserSimiliarity提供了两个用户如何相似的概念，这可能基于很多可能的矩阵和计算之一。 UserNeighborhood定义了一个给定用户的用户组的概念。最终，一个推荐系统将这些模块组合在一起将items推荐给users和相关功能。

运行程序的输出应该是：RecommendedItem[item:104, value:4.257081]
请求一个推荐结果并得到一个。推荐系统引擎将书104推荐给用户1。甚至，这样做是因为推荐系统引擎将用户1对书104的偏好是4.3，这是所有推荐结果的最高打分。
这个结果并不算坏。107没有出现，本应该也是可以推荐的，但它只是和另一个具有不同爱好的user相关联。选104而不是106，因为104的打分高一些。还有，输出结果包含了一个用户1喜欢104的评估值 — 是介于用户4和5所表示的介于4.0和4.5的一个值。

### 评价推荐系统

大部分的推荐引擎通过给item评价打分来实现。所以，评价推荐引擎的一种方式是评价它的评估偏好值的质量 — 评价评估偏好和实际偏好的匹配度。
“真实偏好”并不充分，没有人会知道你将来是否会喜欢一些新的item。推荐引擎可以通过设置一部分真实数据作为测试数据。这些测试数据偏好在训练集中并不展示偏好值 — 要求推荐系统对这些缺少偏好值的数据作出评估，并比较和实际值的差距。
对于推荐系统产生一系列打分是很简单的。例如，计算评估值和实际值之间的平均距离，在这种方法下，分值越低越好。0.0表示非常好的评估 — 评估值和实际值根本没有差距。
均方根（root-mean-square）也是一种方法，也是分值越低越好。

下面是代码示例：

    public static void main() throws Exception {
        String recsFile = "intro.csv";
        DataModel model = new FileDataModel(new File(recsFile));
        RandomUtils.useTestSeed(); // A

        RecommenderEvaluator evaluator = new AverageAbsoluteDifferenceRecommenderEvaluator();

        RecommenderBuilder builder = new RecommenderBuilder() { // B
            public Recommender buildRecommender(DataModel model) throws TasteException {
                UserSimilarity similarity = new PearsonCorrelationSimilarity(model);
                UserNeighborhood neighborhood = new NearestNUserNeighborhood(2, similarity, model);
                return new GenericUserBasedRecommender(model, neighborhood, similarity);
            }
        };
        double score = evaluator.evaluate(builder, null, model, 0.7, 1.0); // C
        System.out.println(score);
    }

大部分的操作发生在evaluate()这个方法中。内部，RecommenderEvaluator将数据划分为训练集和测试集，创建一个新的训练DataModel和推荐引擎测试，比价评估结果和实际结果。
注意，没有将Recommender传给方法，这是因为在其内部，将基于创建的训练集的DataModel创建一个Recommender。所以调用者必须提供一个RecommenderBuilder对象用于从DataModel创建Recommender。

程序打印出了评估结果：一个表明推荐系统表现如何的打分。在这种情况下你能看到很简单的1.0。尽管评价器内部有很多随机方法去选择测试数据， 结果可能是一致的因为RandomUtils.useTestSeed()的使用，每次选取的随机数都一样。这只用于示例、单元测试来保证重复的结果。不 要在真是数据上用它。
AverageAbsoluteDifferenceRecommenderEvaluator
基于AverageAbsoluteDifferenceRecommenderEvaluator实现，得到的这个值是什么含义？1.0意味着，平均意义上，推荐系统评估偏好和实际偏好的的距离是1.0.
.. 1.0在1-5规模上并不大，但是我们的数据太少。如果数据集被随机划分结果可能不一样，因此训练、测试数据集可能每次跑都不一样。

### 评估准确率和召回率

借用更普遍的看法，我们接收经典的信息检索矩阵去评价推荐系统：准确率和召回率。这些是用于搜索引擎的术语，通过query从众多可能结果中返回最好结果集。
一个搜索引擎不应该在靠前的结果中返回不相关的搜索结果，即使他致力于得到尽可能多的相关结果。”准确率”是指在靠前的结果中相关结果所占的比 例，当然这种相关是某种程度上我们定义的相关。”precision at 10″应该是从前10个结果中判断得到的准确率。“召回率”是指靠前的结果中相关结果占的比例。
这些术语也可以应用到推荐系统中：准确率是靠前的推荐中好的推荐所占的比例，召回率是指出现在靠前推荐中好的推荐占整个好的推荐的比例。
    public static void main(String[] args) throws Exception {
        String recsFile = "intro.csv";
        DataModel model = new FileDataModel(new File(recsFile));
        
        RandomUtils.useTestSeed(); 
        RecommenderIRStatsEvaluator evaluator = new GenericRecommenderIRStatsEvaluator();

        RecommenderBuilder builder = new RecommenderBuilder() { // B
            public Recommender buildRecommender(DataModel model) throws TasteException {
                UserSimilarity similarity = new PearsonCorrelationSimilarity(model);
                UserNeighborhood neighborhood = new NearestNUserNeighborhood(2, similarity, model);
                return new GenericUserBasedRecommender(model, neighborhood, similarity);
            }
        };
        IRStatistics stats = evaluator.evaluate(builder, null, model, null, 2,
                GenericRecommenderIRStatsEvaluator.CHOOSE_THRESHOLD, 1.0); // A
        System.out.println(stats.getPrecision());
        System.out.println(stats.getRecall());
    }

评估方法最后会打印出这个推荐器的准确率和召回率.
