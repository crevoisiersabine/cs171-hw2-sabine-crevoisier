###For each of the 5 visualizations listed above plus the calendar map, answer the following questions:

##Who is the audience and What data have been used ?

 - The **calendar view** is useful for the user themselves to get an idea of how often they commit to github and get an overview of their activity over the past year across different days of the week. Likewise it can be useful for project managers to understand workloads and perhaps identify periods in the year or in the week that are more or less heavy and plan accordingly. It can also be useful for prospective employers to use this particular type of visualisation to get a quick idea of whether the user is comfortable regularly commiting to github or whether they normally commit everything in bulk at once; and get a sense of how long they have been practised at using git within github. And finally I think the visualisation is also useful generally to visitors to get a sense of the user's proficiency with git and github. The visualisation also shows the longest streak that the user has been active and the current streak.
 
 The **data** that has been used can be otbained from the github API, using my username as an example, with the following ural request:
 https://api.github.com/repos/crevoisiersabine/:repo/commits
 where the list of all repos that I have (to include in :repo above), I can use the following request:
 https://api.github.com/users/crevoisiersabine/repos
 
 The above will count the commits from my personal repos; we could also find commits that I have made to other organisations:
 by finding public organisations that I belong to: https://api.github.com/users/crevoisiersabine/orgs
 then finding repos belonging to these organisations: https://api.github.com/orgs/:org/repos
 and then querying my commit contributions: https://api.github.com/repos/:owner/:repo/commits?author=crevoisiersabine
 
 Finally the calendar plot also shows opened issues and pulled requests.
 To find out about open issues per repo: https://api.github.com/repos/crevoisiersabine/:repo/issues
 To find out about pulled requests: https://api.github.com/repos/crevoisiersabine/:repo/pulls

 The visualisation shows data for the past year. In order to get that data, you would have to filter using the parameters "since" and "until" as described in the Github API:
 As an example the following code returns all the commits to my CS106A repo since the 1st June 2014, which is empty:
 https://api.github.com/repos/crevoisiersabine/CS106A/commits?since=2014-06-01T00:00:00Z
 compared with all commits since the repo was created:
 https://api.github.com/repos/crevoisiersabine/CS106A/commits

- The **contributors** view would be useful to a project manager to gain insight on which individuals were contributing to what parts of a project and at what point in the project, helping to resource the next project. It may also be useful for training staff, for example to identify what contributors are better at contributing to the start of a project versus the end of a project, by resourcing people to an stage of the process that they might be less comfortable with; also this may help with pairing people with different skillsets again for training and coaching. This visualisation is also nice to see who is mostly contributing to a project, which could be interesting to visitors to gain insight about contributors' skillsets.

The Github API query is given by: https://api.github.com/repos/:owner/:repo/stats/contributors

- The **commits** view provides a nice timeline to see what periods required most commits; again this would be useful for project managers to manage worloads. It is nice that you can click on the bars and have a breakdown of when the commits were made by day of the week, as this may also help with resourcing and gain insight about whether a certain project is broken down into a "design and code on paper" stage followed by a period of implementation and committing, or whether instead it follows a more regular pattern of code and commit. This may provide insight into the different kinds of projects.
This visualisation may also be useful for the individual to gain insight about when they mostly commit, whether they are regularly committing or bulk committing at the end of the week for example?

The Github API query is given by: https://api.github.com/repos/:owner/:repo/stats/commit_activity

- The **code frequency** view shows additions and deletions to the code. I think this would be mostly useful to the user themselves to see whether they tend to generally tidy up their code as the project progresses (and therefore have a relatively symmetrical delete and add distribution) or whether they only tend to delete as they built the project very bottom up, perhaps including too many lines of unnecessary code, hence with more deletions than additions as project continue; or perhaps whether they build the project systematically top down, by adding small chunks at a time that are very lean, hence requiring very few deletions as the project moves forward?

The Github API query is given by: https://api.github.com/repos/:owner/:repo/stats/code_frequency

- The **punch card** is probably mostly useful for project managers to get an overview of when their team mostly commits; again this can be usef for resourcing but also for planning around times when perhaps people are less likely to be very productive and not interrupt contributors in a period when they are likely to be very focused. It could also be useful for the contributors themselves out of curiosity to see when they are most productive. This plot may be interesting for people that work across different time zones to identify whether most productive times (in terms of commits) happen during times where people can collaborate or instead work independently; this may differ across projects.

The Github API query is given by: https://api.github.com/repos/:owner/:repo/stats/punch_card

- The **pulse view** is mostly useful for the contributors I think to keep track of what issues they have opened and what new issues are coming up, which ones have been closed etc... For tracking purposes this may be useful for project managers but probably not so relevant to visitors.

This visualisation uses **data** for open or closed pull requests: https://api.github.com/repos/:owner/:repo/pulls?state=open (or closed)
Open or closed issues: https://api.github.com/repos/:owner/:repo/issues?state=open (or closed)


I think all the above **views** also cater for curious visitors who had some interest in the project; I don't think the intended audience of any of these visualisations is the general public.

##What happens if suddenly a contributor pushes many commits in a short time interval?

If suddenly a contributor pushes many commits at once, this will obsure the detail in the rest of the graph. A way to overcome this may be to change the scale to a logarithmic one to dampen this effect. Also it may be possible to have an overview graph that shows the whole timeline, illustrating that there was a period with a large commit at once, but then provide a zooming view where the detail can be explored.
Another way could be to use a colour scale where the maximum colour is given by the upper quartile, to avoid this outlier obsuring the rest of the datapoints; for example in the calendar plot, dark green would be given for any commits > quartile 3 of the dataset (say that's 50 commits a day) and therefore if a day received 50,000 commits, that point would still show dark green and not dwarf all previous points by forcing them to white. The disadvantage of this is that 50,000 commits would look no different on the colour scale to 50 commits.
A combination of visualisation would probably be the best way to address this issue.
