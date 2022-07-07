# BitcoinTrustedNetwork (Data analysis project to keep the Bitcoin app as trusted as we can).

  1. **Data overview:**
        We keep tracking rates of each user to others to state whether each user is a trusted one or not and that's because users are anonymous on those platforms. **it's a weighted directed graph.**

      1.1 **Records**: source(who rates), target(who be rated), rate( in a scale of -10 (total distrust) to +10 (total trust)), time.
      
      1.2 **Nodes and edges**: it has 3783 nodes, and 24186 edges. And surely the graph density (number of edges/ number of edges of a complete connected that has same node numbers)(connectivity ratio) is low = 0.0016904649973936393.
  2. **Algorithm(the weight should already be in the range of -1 to 1):**
      It computes the fairness and goodness of each nodes. We mainly focus on calculating how much each node is trusted based on what others say, but the FGA (fairness-goodness algorithm) considers how much the rater itself is fair about what it says as a parameter in calculating trust level. and It does make sense. ![image](https://user-images.githubusercontent.com/64162529/177713927-ce68c7d3-4148-415a-817d-8c55f953398e.png)
  


  3. **Data statistical info:**
     
     **Fairness** --> mean= 0.9424351096233645 , std =0.07784591103411552 (high mean, low spread --> data lay in the most right corner of the fairness range[0,1])
     
     **Goodness** --> mean =0.11825600878727517 , std = 0.2050096801218226 (middle mean, nearly high spread(in comparison to fairness)--> data lay in the middle of the goodness range [-1,1])
     
      So, to state whether a node is fair or good, its values should be above or equal to these mean values.
     
   4. **Centrality  measure:**
      we get those nodes that are most popular(Degree Centrality), influential to the network flow (Betweenness Centrality), and the best placed to influence the entire network(Closeness Centrality, Eigen Centrality), then check thier fairness and goodness and if those nodes are below goodness level so the entire network will be affected.
     
 4.1. degree centrality(most popular and to hold most information): I calcuated both the out-degree (to check thier fairness value) and the in-degree (to check goodness value). I've found that (high in-degree centrality--> high fairness) but not vice versa, and those which have high indegree and low fairness threaten the network trust because those spread rumors.
      ![image](https://user-images.githubusercontent.com/64162529/177731595-37c9055a-338b-49e0-a2e3-fba37fc0f2ac.png)

  4.2.
  
  4.3 Eigen Centrality --> Degree centarlity+ its own neighbors degree centrality + etttccc

  5. **Thoughts about the algorithm**
      
   5.1. I see the goodness mean is low because -from the goodness equation- the node is affected with its own in-degree of each node. It's like considering node has just 1 in-degree more trusted, because there that indegree edge comes from a fairing node, than those which are popular and well connected to the whole network.
      
  For example, indegree of **1** =398 and the goodness =0.17517626437834855 , while **795** indgree= 1 and the goodness =0.9937443255477516!!!!
      
  The goodness should instead affected by the in-degree centrality.
    
  5. **Links:**
      
      data --> https://snap.stanford.edu/data/soc-sign-bitcoin-alpha.html
      
      Algorithm research paper -->  https://cs.stanford.edu/~srijan/wsn/
      
      Centrality Measure -->  https://cambridge-intelligence.com/keylines-faqs-social-network-analysis/#:~:text=Centrality%20measures%20are%20a%20vital,but%20they%20all%20work%20differently.
