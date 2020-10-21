
[<-- table of content](Advanced%20functionalities.md)

# Dynamic parameters for queries

* [Prerequisite](#prerequisite)
* [Create the Date Range Input component](#create-the-date-range-input-component)
* [Create the parameters](#create-the-parameters)
* [Link the date range input component to the parameters](#link-the-date-range-input-component-to-the-parameters)
* [Link the pie chart component to the parameters](#link-the-pie-chart-component-to-the-parameters)
* [Make the query dynamic](#make-the-query-dynamic)
* [Test](#test)

--- 

### Prerequisite

Parameters are like local variables, they are **reusable inputs** connected only to a component.
When defining a parameter, you can assign it a default value to use in the event that one is not fetched for it.

In this part, we will setup a simple double parameter dashboard.

* layout used (*help [here](Create%20a%20new%20dashboard.md#how-to-customise-the-dashboard-layout)*)

![](https://i.imgur.com/CzD7f51.png)

* datasource used
```
select COALESCE("LibelleCommune",'null') as LibelleCommune, COALESCE("CodeCommune", 'null') as CodeCommune, count(*)
from intervention
where to_char("DateDebutIntervention", 'YYYY-MM-DD') >= '2020-08-01'
  and to_char("DateFinIntervention", 'YYYY-MM-DD') <= '2020-08-01'
  and "DateDebutIntervention" IS NOT NULL
  and "DateFinIntervention" IS NOT NULL
GROUP by "LibelleCommune", "CodeCommune"
order by "LibelleCommune" ASC
;
```

The goal is to make the query dynamic, we want to link a date range selector with this query.

First create the datasource with the query above (*help [here](Create%20a%20datasource.md)*) :

![](https://i.imgur.com/9UHeLOd.png)

* create the component

We will use a piechart with a simple configuration (*help [here](Add%20components.md)*) :

![](https://i.imgur.com/gc7UVG1.png)

### Create the Date Range Input component

* add a "*Date Range Input Component*" in the component panel (under "*Selects*")

![](https://i.imgur.com/wLgVLZ3.png)

### Create the parameters

As a date range outputs two dates we have to create two parameters `startDate` and `endDate`.

* add two "*Date Parameter*" in the component panel (under "*Parameters*")

![](https://i.imgur.com/DLngEYd.png)

> Note : you can set the "*property date value*" to different things, it will be the default value for this parameter (value when page is loaded)
> ![](https://i.imgur.com/v3fiSav.png)

### Link the date range input component to the parameters

* click on the "*Date Range Input*" component to show properties 

![](https://i.imgur.com/e6QyUko.png)

* click on parameters, select the two we have created and "*OK*"

![](https://i.imgur.com/KUFpBap.png)

* verify that the parameters appear as an array

![](https://i.imgur.com/Z4SH59a.png)

> Linking the date range input with the parameters allows us to change the value on the go and not stick with the default value.

### Link the pie chart component to the parameters

* click on the "*CCC Pie Chart*" component to show properties 

![](https://i.imgur.com/Wo9AjJo.png)

* click on listeners, select the two parameters we have created
> Listener are parameters that your component will watch and each change will update the component.

![](https://i.imgur.com/PFhvdEt.png)

* click on parameters, name the parameters for the query
> "*Arg*" : name of the parameter in the query | "*Value*" : name of the parameter component

![](https://i.imgur.com/m6mUcUv.png)

* verify that the listeners and parameters appear as arrays

![](https://i.imgur.com/eYEA2DR.png)

### Make the query dynamic

* select the query in the Datasource panel

![](https://i.imgur.com/ysrAcEN.png)

* click on Paramaters in the properties
> "*Name*" : put the name of the parameters (the ones in the pie chart)
> "*Value*" : here you can force the parameter name
> "*Type*" : type passed in the query

![](https://i.imgur.com/YCeKz8I.png)

* edit the query

We will change the static date value to the parameter value

---> This :
```
where to_char("DateDebutIntervention", 'YYYY-MM-DD') >= '2020-08-01'
  and to_char("DateFinIntervention", 'YYYY-MM-DD') <= '2020-08-01'
```
---> Becomes :
```
where to_char("DateDebutIntervention", 'YYYY-MM-DD') >= ${start}
  and to_char("DateFinIntervention", 'YYYY-MM-DD') <= ${end}
```

### Test
* Load the preview

![](https://i.imgur.com/WV2YRnb.png)

* To change the date range, simply click on the select in the first row

![](https://i.imgur.com/kJhTb9s.png)

> A specific date also work for a date range

* Changing the date in the select will update the graph

![](https://i.imgur.com/SZyfMpv.png)

