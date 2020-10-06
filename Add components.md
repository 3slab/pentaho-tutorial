[<-- table of content](Create%20a%20dashboard.md)

# Add components

First, we have to create a datasource from where the data will be sourced.

To do so :
1. click on the 3rd tab "*Datasource Panel*"
2. click on the type of database you're using, for exemple "*SQL Queries*" and "*sql over sqlJndi*"
3. in the properties, set a name
4. setup the connection (depens of the type of the database you're using)
	* under "*Jndi*" enter the name of the database you're using
5. enter the query you want to work with
	* **remember** : you can only put one query per datasource, if you need to add another query you'll need to add another datasource

Here is a video that show the steps :

![](https://i.imgur.com/l9bSUEC.gif)

The we need to create the component itself :
1. go to the 2nd panel "*Components Panel*"
2. select the type of component you want on the left side of the screen
3. under "*Datasource*" enter the name of the datasource (there is autocompletion)
4. under "*HtmlObject*" enter the name of the panel you want your component in

Here is a video that show the steps :

![](https://i.imgur.com/nJUX23f.gif)

