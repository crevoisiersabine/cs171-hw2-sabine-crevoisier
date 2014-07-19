###1. Which graph-related tasks does an ideal GitHub Network Graph need to address?

Low-level tasks:
- sort: temporal or sequential
- retrieve value of a particular commit: when it occurred and what the commit was
- filter: by date, by branch

Topology-based task:
- connectivity: it is important to get an overview of the connectivity of the commits to get a sense of the branching and forking of a particular repository.

Browsing task:
- follow path: from a particular node, we might want to follow a particular branch to see the sequence of commits
- revisit: we might want to return to a particular node to follow a different branching off

###2 + 3. What do you notice about the three repositories? How does this impact your graph?

The repositories are much larger than the ones that we have been working with; as a result the visualisation becomes too cluttered, the nodes too close together to view in the screen and covered by the link arrows. It is therefore difficult to see the invididual commits and the colour coding according to the authors.
The links also are not so useful anymore as they become too closely packed due to the high density of commits and therefore it is difficult to see where the source and target nodes are and it is no longer possible to trace a particular commit history.
Also it takes a longer time for the API calls to be made.

###4. How would you improve your visualization to address issues with the larger and more complex data?

The vertical space is not used very effectively for larger and more complex data because most commits from other branches have been incorporated into the master and therefore the master is very dense and other branches are very sparse of commits.
Therefore it would be more useful to use the y-coordinate to encode by author. However because in repositories it is also apparent that there are only a handful of main contributors, there ends up being a lot of empty white space. I think for these larger repositories, the y-coordinate should actually not be used to encode data: I think it is best to just use colour to encode different authors and rely on the tooltip to show what branch we are looking at. Instead I suggest using the y-coordinate by placing each branch at a given y-coordinate such that for the length of the branch, there are no other branches that interfere with it along the x-axis; that way, the empty y space would be removed. The width of the svg would then be determined by the number of branches as well as how wide each one is (requiring more space), rather than only how many branches there are. This would make the graphical representation more compact. By hovering over a coloured cluster (corresponding to a particular author), a tooltip would reveal the authors name (as in this new case, the author's name would not revealed by the position on the y-axis as the y-axis coordinate may share more than one author).
The links also contribute to cluttering the graph and therefore I think it would be best for them not to appear at first and only show themselves upon hovering over a node, revealing the commit history for that node.
Also the arrows hide the nodes (and hence the colour encoding) and so should only appear when the distance between the nodes is larger than the arrow width; a zoom option could be included so that we could zoom in to a particular area of the graph, at which point the arrows would become apparent and the links would be revealed to enable following and revisiting tasks. However upon zoom out, the links and arrows would again disappear; the arrows would remain invisible whereas the links would show upon hovering over the relevant nodes as explained above.