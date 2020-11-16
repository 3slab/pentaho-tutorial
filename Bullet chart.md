[<-- table of content](Annexes.md)

# Bullet chart

* go to the component panel
* select *"CCC Bullet Chart"* under *Charts*

![](https://i.imgur.com/PVIYnnY.png)

* main properties (in advanced properties)

![](https://i.imgur.com/cfe6mvk.png)

* *Name* : Name of the bullet chart
* *Title* : Title of the bullet chart
* *Width* : Width in pixels
* *Height* : Height in pixels
* *Bullet Measures* : The observed measure for this performance indicator
* *Bullet Markers* : A marker, such as a target value for this performance indicator
* *Bullet Ranges* : A coloured range showing ranges values, example below

 ![](https://i.imgur.com/cvWLHsZ.png)
 
+ *HtmlObject* : Name of the placeholder for the graph
+ *Orientation* : Horizontal or Vertical
+ *Extension Points* : some examples to set some colors

Parameter                | Value              | Description
-------------------------|:----               | ---
bulletRange_fillStyle    | `function(){ return ["#9C9384","#DED2A0","#F2EED5","#FEFDF9"][this.index]; }` | Changes the fill color for the ranges defined in Bullet Ranges
bulletMeasure_fillStyle  | Hex like `#43578A` | Color of the bar
bulletMarker_shape       | `Bar`              | Shape of the Marker (Target) symbol
bulletMarker_lineWidth   | `3`                | Width of the Marker symbol
bulletMarker_strokeStyle | Hex like `#A11E13` | Color of the line

> ⚠️ Note : Bullet chart component doesn't support percentages, the datasource has to return a number or a float.
