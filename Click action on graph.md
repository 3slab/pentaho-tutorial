[<-- table of content](Advanced%20functionalities.md)

# Click action on graph
* [Prerequisite](#prerequisite)
* [Setup a new parameter](#setup-a-new-parameter)
* [Create the table component](#create-the-table-component)
* [Create the dynamic datasource](#create-the-dynamic-datasource)
* [Make the piechart clickable and update data in the table](#make-the-piechart-clickable-and-update-data-in-the-table)
* [Test](#test)

--- 
### Prerequisite

This part will be based on the work done in Part *[Dynamic parameters for queries](Dynamic%20parameters%20for%20queries.md)*.

* We add a column in the second row for the future table
> Note the size of the column named *table* : `7`
> That means that the other one, named *piechart*, has to have a size of : `12 - 7 = 5`

![](https://i.imgur.com/57QAZNk.png)

* We should have this 

![](https://i.imgur.com/em8Qk2D.png)

* The query for the table
```sql
select "IdIntervention", "CodeIntervention", "LibelleIntervention", "Geographie"
from intervention
where to_char("DateDebutIntervention", 'YYYY-MM-DD') >= '2020-08-01'
  and to_char("DateFinIntervention", 'YYYY-MM-DD') <= '2020-08-01'
  and "DateDebutIntervention" IS NOT NULL
  and "DateFinIntervention" IS NOT NULL
  and "CodeCommune" = '35'
;
```
> We will make the query dynamic later.

### Setup a new parameter

To make this query dynamic we need three parameters and two of them were already created in the previous example.

* create a "*Simple Parameter*" in the component panel

![](https://i.imgur.com/Czoxw1q.png)


### Create the table component

* add a "*Table component*", under *Standard*, in the component panel

![](https://i.imgur.com/OPr9mmS.png)

* select the parameters to listen to
> Listener are parameters that your component will watch and each change will update the component.

![](https://i.imgur.com/9TkbD1P.png)

* add parameters
> "_Arg_" : name of the parameter in the query | "_Value_" : name of the parameter component

![](https://i.imgur.com/gYjzWNs.png)

### Create the dynamic datasource

Now that we have created all the needed parameters, we can create the datasource.

* The query for the table
```sql
select i."IdIntervention", i."CodeIntervention", i."LibelleIntervention", i."Geographie"
from intervention i
where to_char(i."DateDebutIntervention", 'YYYY-MM-DD') >= ${start} 
  and to_char(i."DateFinIntervention", 'YYYY-MM-DD') <= ${end}
  and "DateDebutIntervention" IS NOT NULL
  and "DateFinIntervention" IS NOT NULL
  and 1 = CASE
            WHEN ${code_comm} != '1111' AND "CodeCommune" = ${code_comm} THEN 1
            WHEN ${code_comm} = '1111' AND "CodeCommune" IS  NULL THEN 1
            ELSE 0
          END
;
```
> The `CASE` is here to manage `code_comm`, as it is nullable, **in a single query**.
> We will see later how to change it's value if it's null.

* create the datasource, in the datasource panel

![](https://i.imgur.com/hJIUHMP.png)

* enter the query (above), in the "*Query*" section
* set the parameters

![](https://i.imgur.com/QrOOFex.png)

* we then have this datasource

![](https://i.imgur.com/zjNFmMy.png)

**Go back to the component panel** :
* edit "*intervention_table*" with the proper datasource and html object

![](https://i.imgur.com/VcEbkHn.png)

* we now have when we preview

![](https://i.imgur.com/kTVh2e6.png)


If you want to hide the `geographie` column you can do so in the table properties

* click on "*Column Headers*"

![](https://i.imgur.com/vjjpLIL.png)


Rename in order of appearition, from left to right, the columns you want to display

> if you want the two first columns 
> 
> ![](https://i.imgur.com/PFH4ggf.png)
> 
> which will give 
>
> ![](https://i.imgur.com/SMDjM5L.png)

In this case we need the first three columns
* edit "*Column Headers*"

![](https://i.imgur.com/KV9wWrw.png)

* preview result

![](https://i.imgur.com/Zatzsiy.png)

### Make the piechart clickable and update data in the table

Here we will see how to change the `code_comm` by clicking on a slice of the pie chart.

* click on the pie chart component in the component panel

![](https://i.imgur.com/k31PVhL.png)

* set "*Clickable*" to *True*

![](https://i.imgur.com/ZUUPMp4.png)

* click on the box with three dots under "*Click Action*" and paste the code below

> This code will be executed when you click on a slice of the pie chart

```js
function setparamcodecomm(scene) {
    //store in a variable the value of the selected slice
    var category = scene.vars.category.value;
    
    //if the value if null, change to a dummy value
    //it will be useful for the CASE in the query
    if(category === 'null') {
        category = '1111';
    }
    
    //equivalent to console.log (which also work)
    Logger.log("Selected category" + category);
	
    //dashboard is the JS object for your dashboard
    //fireChange is a built-in function to the value of a parameter
    //then we edit the value of code_comm parameter with the value stored before
    dashboard.fireChange('code_comm', category);
}
```

### Test
In order to see the results change in the table you will need to click on a slice of the pie chart.

![](https://i.imgur.com/aITXsew.png)

> The slice the cursor is flying over indicate us that there a count of 2 for the Codecommune = 3
> Then we should have two lines in the table on the right

Result after clicking 

![](https://i.imgur.com/P5eawvA.png)

The table has been updated, simply by changing the value of the parameter as it listens parameters.
