[<-- table of content](Create%20a%20dashboard.md)

# Add components

**First**, we have to __create a datasource__ from where the data will be sourced.

To do so :
1. click on the 3rd tab "*Datasource Panel*"
![](https://i.imgur.com/e5epepa.png)

2. click on the type of database *(left side of the screen)* you're using, for exemple "*SQL Queries*" and "*sql over sqlJndi*"
![](https://i.imgur.com/KzpP7Ob.png)

3. in the properties, set a name
![](https://i.imgur.com/7BieD2G.png)

4. setup the connection (depens of the type of the database you're using)
	* under "*Jndi*" enter the name of the database you're using
5. enter the query you want to work with *(click on the box with 3 dots)*
	* **remember** : you can only put one query per datasource, if you need to add another query you'll need to add another datasource
![](https://i.imgur.com/L3h2t9d.png)

6. put your query in the *Sql Editor*
![](https://i.imgur.com/gLSoSXu.png)

Here is a video that show the steps with an exemple :

![](https://i.imgur.com/l9bSUEC.gif)

===

The we need to create the component itself :
1. go to the 2nd panel "*Components Panel*"
![](https://i.imgur.com/06JSgtD.png)

2. select the type of component you want on the left side of the screen
![](https://i.imgur.com/1hGbwPa.png)

3. under "*Datasource*" enter the name of the datasource (**to see all datasources you've created type backspace**)
![](https://i.imgur.com/HWPYL9G.png)

4. under "*HtmlObject*" enter the name of the panel you want your component in
![](https://i.imgur.com/vGIIjEJ.png)

Here is a video that show the steps :

![](https://i.imgur.com/nJUX23f.gif)
