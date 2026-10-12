# Lebanon Basin Atlas

A static web map for the Abou Ali, Beirut, Damour, Ibrahim, and Litani basins. The five basin datasets and their intervention PDFs are included in `data/`, so the basin choices appear automatically; visitors do not have to browse to a folder. The interface uses a blue and white palette, with a layer export panel and controls for layer drawing order.

## Run it from Jupyter

1. Open `Start_Basin_Viewer.ipynb` in local JupyterLab on Windows.
2. Run each code cell from top to bottom with **Shift+Enter**.
3. Click the link from the last cell. Choose a basin, expand a category, and turn on layers.

The notebook runs a small local web server. Keep the notebook kernel running while the map is open. The app reads its bundled data from the same folder as `index.html`.

## Publish on GitHub Pages

Keep `index.html` and the complete `data/` folder together in the Pages repository. Each shapefile is packaged as its own ZIP and fetched only when that layer is turned on. The site data package is about 348.5 MiB total; the largest individual file is about 24.1 MiB. The archive was split into 166 layer packages and includes 10 PDF maps.

The packages preserve the source shapefiles and attributes. The browser shapefile reader converts selected data to WGS 84 for display. The supplied projection is WGS 84 / UTM zone 36N (EPSG:32636). `Ranges`, `L1_descr`, and `Descrip` are detected as categorical style fields wherever they occur. Other layers get a default style based on point, line, or polygon geometry. Feature popups show area when the data provides an area field and a short list of key attributes. The export panel lets visitors select a basin, category, and shapefile to download its ZIP package.

To rebuild the `data/` folder from the original archive on Windows, run this in PowerShell from the viewer folder:

```powershell
Set-ExecutionPolicy -Scope Process Bypass
./build-data.ps1 -SourceZip 'D:\MK\Desktop\BASINS.zip'
```

You can skip the rebuild if `data/manifest.json` and the basin folders are already present.

The viewer uses Esri World Topographic Map tiles and loads Leaflet and the shapefile reader from public CDNs, so users need an internet connection. See [GitHub's large-file guidance](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github) and [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits).
