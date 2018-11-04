# GIS Assessment

//OpenLayers.ProxyHost = "/cgi-bin/proxy.cgi?url=";
/*specifying the extent of the map*/
var extents = new OpenLayers.Bounds(4079939, -162296, 4131475, -127987); 

/*loading various controls to the map*/
var control, controls = [];

   var map = new OpenLayers.Map("map" /*this map is the div id in the html code*/, {
        controls: [
            new OpenLayers.Control.Navigation(),
            new OpenLayers.Control.ArgParser(),
            //new OpenLayers.Control.Attribution(),
            new OpenLayers.Control.LayerSwitcher({'div':OpenLayers.Util.getElement('dropdown-content')}),
            new OpenLayers.Control.MousePosition(),
            //new OpenLayers.Control.ScaleLine(),
            new OpenLayers.Control.PanZoomBar(),
             //new OpenLayers.Control.Zoom(),
            new OpenLayers.Control.KeyboardDefaults()
        ],
        maxExtent: extents,
        minExtent: "auto",
        restrictedExtent: extents /*one cannot pan outside the specified extent*/
    },
        {projection: new OpenLayers.Projection("EPSG:900913")}, /*specifying the projection*/
    

        {units: 'm'},
        {allOverlays: true} /*all other data added will overlay on the basemap*/
        );

//var google_sat = new OpenLayers.Layer.Google("Google Satellite",{type:google.maps.MapTypeId.SATELLITE,numZoomLevels:40});

var OSM = new OpenLayers.Layer.OSM("OpenStreetMap");  /*loading the OSM basemap*/

/*loading the overlays from GeoServer.web_map is the workspace name. Loading the layer as a WMS*/
var tm_world_borders = new OpenLayers.Layer.WMS (
        "World Wide",
        "http://localhost:8080/geoserver/map_db/wms",
        {layers:"map_db:tm_world_borders-0.3",transparent: true, format: "image/gif"},
        {visibility: true},
        {'displayInLayerSwitcher':true}
);

var sapad_or_2018_q3 = new OpenLayers.Layer.WMS (
    "World Wide",
    "http://localhost:8080/geoserver/map_db/wms",
    {layers:"map_db:tm_world_borders-0.3",transparent: true, format: "image/gif"},
    {visibility: true},
    {'displayInLayerSwitcher':true}
);
var tm_world_borders_simpl = new OpenLayers.Layer.WMS (
    "World Wide",
    "http://localhost:8080/geoserver/map_db/wms",
    {layers:"map_db:tm_world_borders_simpl-0.3",transparent: true, format: "image/gif"},
    {visibility: true},
    {'displayInLayerSwitcher':true}
);

/*adding the data to the map object*/ 

map.addLayers([OSM,sapad_or_2018_q3,tm_world_borders,tm_world_borders_simpl,]);

/*specifying the center of the map and a zoom level of 11*/

map.setCenter(new OpenLayers.LonLat(4099485,-142884),11 );

Dataset: Base layer, OpenStreetMap. Metadat: Shapefile for SOuth Africa
Setup: Run Geoserver on the local host, Run Postgresql on PgAdmin, Load shapefile using Postgis loader and open the index html from the appication to run the application
