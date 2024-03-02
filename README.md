# GEE
using Google Earth Engine to Generate Slope for Date (2019 and 2024)
// Load SRTM DEM data
var dem = ee.Image('USGS/SRTMGL1_003');

// Define the date for which you want to calculate slope
var startDate = '2019-10-24';

// Calculate slope for the start date
var slopeStart = ee.Terrain.slope(dem);

// Define visualization parameters
var visParams = {min: 0, max: 45, palette: ['blue', 'yellow', 'orange', 'red']};

// Add the layer to the map
Map.addLayer(slopeStart, visParams, 'Slope - Start Date');

// Set map center
Map.centerObject(dem, 8);

// Export the slope data to Google Drive
Export.image.toDrive({
  image: slopeStart,
  description: 'slope_start_date',
  folder: 'GEE_exports', // Change to your desired folder name
  scale: 30, // Adjust scale as needed
  region: dem.geometry().bounds(), // Export the data within the bounds of the DEM
  crs: 'EPSG:4326' // Set CRS to WGS84
});
