[<-- table of content](Annexes.md)

# Queries with big loads

Imagine you want to paginate your query server side.
That means you don't want to execute the query one but for each page.

To do so : 

Create your datasource with the query you want. ([how to add a datasource](Create%20a%20datasource.md))

**In the components that uses the big query**

* go to the Advanced properties

![](https://i.imgur.com/VUGZNLe.png)

* scroll to "*Paginate server side*" and set it to "*True*"

![](https://i.imgur.com/niOYjuP.png)
