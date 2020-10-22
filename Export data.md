[<-- table of content](Advanced%20functionalities.md)

# Export data

* [Export Button component](#export-button-component)
	* [How to create an export button](#how-to-create-an-export-button)
	* [Settings of export button](#settings-of-export-button)
* [Export Popup component](#export-popup-component)
	* [How to create an export popup](#how-to-create-an-export-popup)
	* [Settings of export popup](#settings-of-export-popup)


## Export Button component

Export of data can be done only for a component, so the results of only a query and not the full dashboard will be exported.
When using the "*Export Button Component*" component, you can export data to one of **two formats** : **csv** or **xls**, no other format is available on this component.

### How to create an export button

* go to the component panel.
* add a "*Export Button Component*" under *Standard*

![](https://i.imgur.com/pO5QPB6.png)

### Settings of export button

The properties that you need to set are : 
* "*Label*" : The text that will be displayed on the button. 

* "*Component name*" : The name of the component from where to export the data.

* "*Output type*" : The format to export data to.

![](https://i.imgur.com/XpgTOIQ.png)

## Export Popup component

The "*Export Popup button*" component is more flexible and will let you have more options.
With this export popup button you will get a popup with the options to export to different formats, and one option should be selected to make the export.
The formats available are : **csv**, **xls**, **json**, and **xml**. And you can also export a chart to **svg** or **png** format.

### How to create an export popup

* go to the component panel.
* add a "*Export Popup Component*" under *Standard*

![](https://i.imgur.com/K3a4Z6x.png)

### Settings of export popup

*You need to go to the advanced properties of the component*.

![](https://i.imgur.com/0D3Mz2T.png)

The properties that you need to set are :
* "*Title*" : Text that will be displayed on the dashboard.

* "*Gravity parameter*" : Set the position where the popup will jump from.

* "*Chart component to export*" : Name of the chart to export.

* "*Chart export label*" : Set the text that will be displayed and to make possible the export of the chart.

* "*Chart export type*" : Set the format to export the chart to svg or png.

* "*Data component to export*" : Name of the component from where data will be exported.

* * "*Name for data export attachment*" : Name of the file that will be exported. It will force the format if informed.

* "*Data export label*" : Set the text that will be displayed and to enable exporting the data.

* "*Data export type*" : Set the format to export the data to csv, xls, json, or xml.

* "*Content links*" : This an advanced option allows you to specify the text to be displayed and a function that will be executed when the respective link is clicked. Inside this function you will be able to define the component from where to export, the format, and the filename to export to.

Setup *Content links* : 

![](https://i.imgur.com/WqYKcX6.png)

Each new line will be an option, and for each line you need to specify an argument and a value :
* In "*Arg*" you need to specify the text to display as the link.
* In "*Value*" you need to specify the function. 

Example of function you put in value :
```js
function() {
   /*myTable is the name of the component*/
   var comp = dashboard.getComponentByName('${c:myTable}');
   
   /*get chart or query definition if the component
     is a chart or a table*/
   var cd = comp.chartDefinition || comp.queryDefinition;
   var query = dashboard.getQuery(cd);
   
   query.exportData('csv', {}, {filename: "filename.csv"});
}
```

![](https://i.imgur.com/5zmvLWw.png)

Then when you preview :

![](https://i.imgur.com/zd4bYhu.png)

You have three choices :
* Export chart : comes from these options

![](https://i.imgur.com/VE6b5B8.png)

* Export table : comes from these options

![](https://i.imgur.com/X4T9jjy.png)

* export inter table come from 

![](https://i.imgur.com/22Nr5Vs.png)

> ⚠️ Note : the preview of export chart to png or svg is only working when you preview the `.wcdf` file.
> 
> ![](https://i.imgur.com/PRf0YdP.png)
> 
> The export preview will not work if you do it in the editor (where the tab is named with "*Editing:* name").
