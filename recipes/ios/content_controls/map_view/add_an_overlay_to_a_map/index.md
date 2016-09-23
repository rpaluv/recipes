id:{316BE54A-5E70-440A-4B5E-4F32DAFF6224}  
title:Add an Overlay to a Map  
brief:This recipe shows how to add an overlay to a map.  
samplecode:[Browse on GitHub](https://github.com/xamarin/recipes/tree/master/ios/content_controls/map_view/add_an_overlay_to_a_map)  
article:[Displaying a Location](/recipes/ios/content_controls/map_view/display_device_location)  
article:[Add an Annotation](/recipes/ios/content_controls/map_view/add_an_annotation_to_a_map)  
sdk:[MKMapView Class Reference](https://developer.apple.com/library/ios/#documentation/MapKit/Reference/MKMapView_Class/MKMapView/MKMapView.html)  
sdk:[MKMapViewDelegate Protocol Reference](https://developer.apple.com/library/ios/#documentation/MapKit/Reference/MKMapViewDelegate_Protocol/MKMapViewDelegate/MKMapViewDelegate.html)  

<a name="Recipe" class="injected"></a>


# Recipe

An overlay lets you ‘draw’ over a map. To add an overlay to a
MKMapView:

1. Start with an existing `MKMapView` or review the  [Displaying a Location](/recipes/ios/content_controls/map_view/display_device_location) recipe. </li>

<ol start="2">
	<li>Declare class-level variables for the overlay and its renderer:</li>
</ol>

```
MKCircle circleOverlay;
MKCircleRenderer circleRenderer;
```

<ol start="3">
	<li>Implement MKMapView.OverlayRenderer to provide a renderer for the overlay: </li>
</ol>

```
mapView.OverlayRenderer = (m, o) => {
    if(circleRenderer == null) {
        circleRenderer = new MKCircleRenderer(o as MKCircle);
        circleRenderer.FillColor = UIColor.Purple;
        circleRenderer.Alpha = 0.5f;
    }
    return circleRenderer;
};
```

<ol start="4">
	<li>Create an overlay, in this case a circle positioned near the Pyramids of Giza, and add it to the map: </li>
</ol>

```
var coords = new CLLocationCoordinate2D(29.976111, 31.132778); //giza
circleOverlay = MKCircle.Circle (coords, 200);
mapView.AddOverlay (circleOverlay);
```

 ![](Images/MapOverlay.png)

 <a name="Additional_Information" class="injected"></a>


# Additional Information

The `OverlayRenderer` method must be assigned to prior to adding the `MKOverlay` to the `MKMapView`. If this is not done, the overlay will not appear until the map is moved or scaled in some way.

The `MilesToLatitudeDegrees` and `MilesToLongitudeDegrees` helper methods can be
found in the [Displaying a Location](/recipes/ios/content_controls/map_view/display_device_location) recipe.