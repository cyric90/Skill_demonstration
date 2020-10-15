
Input：

1. Node info: reprsenting each author. It inlcudes:

• their id in the graph

• the number of years since their first and last publication to 2017 (e.g. first:3 means author published first
paper at 2014)

• their number of publications in total, num_papers

• presence of specific keywords in the titles and abstracts of their publications (denoted keyword_X where X ∈
{0, 1,..., 53}, each being a binary value and only listed if its value is 1)

• publication at specific venues (denoted venue_X where X ∈ {0, 1,..., 303}, each being a binary value and only
listed if its value is 1)

2. Graph data:
For exampe 
1 2
2 1 3 4
3 2 5
4 2 5
Means there is a link between node 1 and 2, 2 and 3, 2 and 4 and so on.



Output:

Unseen graph data predictioin to decide whether there is a link between node A and B or the link does not exist. 


