
var nicfi = ee.ImageCollection('projects/planet-nicfi/assets/basemaps/americas');

// Filter basemaps by date and get the first image from filtered results
var basemap= nicfi.filter(ee.Filter.date('2022-09-01','2022-09-30')).first();

//Clip using the geometry with draw tool
var basemap_clip = basemap.clip(geometry)

//See the results
Map.centerObject(geometry, 10)

var vis = {"bands":["R","G","B"],"min":64,"max":5454,"gamma":1.8};

Map.addLayer(basemap_clip, vis, '2022-10 mosaic');
Map.addLayer(
    basemap_clip.normalizedDifference(['N','R']).rename('NDVI'),
    {min:-0.55,max:0.8,palette: [
        '8bc4f9', 'c9995c', 'c7d270','8add60','097210'
    ]}, 'NDVI', false);
    

//Export
Export.image.toDrive({
  image: basemap_clip, 
  scale: 5, 
  description: 'Basemap_Planet_092022', 
  fileNamePrefix: 'Basemap_Planet_092022',
  crs: geometry.crs,
  folder: 'Planet',
  region: geometry, 
  maxPixels: 1e12,
  skipEmptyTiles: true,
  formatOptions: {
    cloudOptimized: true,
  }
});
