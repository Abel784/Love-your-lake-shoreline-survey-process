# CLARI-Project-**Made in QGIS 3.63.3**

QGIS (Quantum Geographic Information System) is a free, open-source software used for mapping and spatial data analysis. It enables users to create, edit, visualize, and analyze geospatial data, supporting a wide range of file formats and databases. QGIS is popular for creating interactive maps, conducting geographic research, and managing spatial information for various applications like urban planning, environmental management, and fieldwork. It’s versatile, extensible through plugins, and can be integrated with other software and online services.

# How To Use
-**Download Repository**

-**Extract Folder**

-**Click `Index.html` to launch in your browser**  

  OR  
  
-**Download the raw project files for QGIS**

# How It Was Made

-**I started by importing the shapefiles and the Excel data into QGIS.** Once imported, I looked for similarities in the Excel sheet and the shapefiles to join the table and the shapefile—in this case, the PID and the Assessment number.

  -**You can join the table by right-clicking the shapefile, going to Properties, and selecting the Join Table property** (Image Below).

  ![image](https://github.com/user-attachments/assets/082d7a27-6c36-401f-a7ef-19618b52abc5)
  
-**With the Excel sheet joined to the shapefile, all Excel data should be part of the shape features table.**

  ![image](https://github.com/user-attachments/assets/03026daa-3f06-464a-973a-667efd6eb2ef)

-**To create the 30m shoreline buffer, I created a new shapefile and used the Trace tool to draw the shoreline.**  

-**To get the Trace tool, right-click your toolbar and check off the "Snapping Toolbar."** Once turned on, this will allow your newly drawn line to snap to the shapefiles, creating a very tight shoreline. *(Tip: Click to make checkpoints, and make a lot of them to avoid errors!)*  

- ![image](https://github.com/user-attachments/assets/741f6a5f-2a94-46ba-a79f-aac628b63108)
  
-**Once the new shoreline is drawn, you'll need to use it to create your buffer.** Go to `Vector -> Geoprocessing Tools -> Buffer`, and set your input layer to be the line shapefile you've just created. 
*(Note: Your buffer will be X meters on both sides of your drawn line unless otherwise specified. The image below shows the buffer settings I used.)*  

- ![image](https://github.com/user-attachments/assets/38e60855-9be0-4bbf-8430-d561c552f13e)
  
-**To delete the data inside the buffer to avoid overlap, go back to `Vector -> Geo Processing -> Difference`.** This will remove the data inside the buffer zone without deleting the feature altogether. Set the input layer to the original shapefile and the overlay layer to the buffer layer you made in the previous step.
  - ![image](https://github.com/user-attachments/assets/010c9ba8-dccf-49b9-921b-ae173e75fd98)
  
-**Once this is done, you can add labels to the shapes by clicking the label button and selecting which data in the table you want shown.**  
- ![image](https://github.com/user-attachments/assets/47819c58-fe8a-40a8-9fdd-752426643a11)
  
-**Now to convert this into an interactive version, you'll need the `qgis2webapp` plugin.** This can be downloaded and installed directly into the app by going to `Plugins -> Manage and Install Plugins -> Search qgis2web -> Install`.
  - ![image](https://github.com/user-attachments/assets/0a0ae60d-344c-4df5-9b0a-17bf0e56d07a)
  
-**Finally, run `qgis2web` and select your buffer and difference layers that you made.** Choose your settings and needs for the web app. You'll have OpenLayers and Leaflet to choose from for a framework. *(I personally prefer Leaflet as it gives you more features out of the box.)*

**IMPORTANT:** If your shapefile doesn't show up, it's because your layer CRS is set incorrectly for the web map. If your preview looks empty, check your CRS. Once you select your basic settings and hit EXTRACT, QGIS will create a basic web app in HTML and JavaScript format, giving you full access to the code to add, change, and remove features as needed.
  - ![image](https://github.com/user-attachments/assets/ff65e9c3-3384-4fdc-ab0f-c93685eb5b3e)

# How To Automatically Add Geotagged Photos
-**To add geotagged photos to your web map, I recommend following this guide:** 
[Mapping and Viewing Geotagged Photos in QGIS](https://opengislab.com/blog/2020/8/23/mapping-and-viewing-geotagged-photos-in-qgis).  
  It shows you how to import geotagged photos to your map, place them based on their longitude and latitude, and convert your geotagged images and map into a web app.

# How To Manually Add Geotagged Photos
-**Follow the above tutorial until you have completed Steps 1, 2, and 3a.**

*(DON'T DO STEP 3, JUST 3A, unless you know the direction of the geotagged photo.)*

-**Once that's complete and you have created your geotagged layer, right-click and go to the Attributes Table.**  
- ![image](https://github.com/user-attachments/assets/f05bc69d-7bc4-44b1-a745-07cc5144890b)
  
-**Click on "Toggle Edit" and then "Add Feature".**  
- ![image](https://github.com/user-attachments/assets/76a95bed-6d4f-4527-8ce3-0f696eb5f6c8)
  
-**Leave the FID field as "Autogenerate".**

-**Click the three dots next to "Photo" and select your desired photo.**

-**Fill in the "Filename."** This can be whatever you want it to be, so make it easy to identify in your Attribute Table.

-**Then fill in the "Longitude" and "Latitude" fields for your image's location.**

-**You should have something like the image below.**  
- ![image](https://github.com/user-attachments/assets/bd60f1bf-0284-459c-868b-055084936361)
  
-**Make sure you've added all your photos and their latitudes and longitudes before moving on to the Field Calculator section.** The shapes should be added once all photos are in the table.

-**Now, we have to give the new attribute in the table a shape to appear on the map.**

-**Open the Field Calculator.**  
- ![image](https://github.com/user-attachments/assets/334e1c4d-dc00-42ee-b33c-4cd016e11418)
  
-**Once open, check off "Update Existing Field" and select "geometry" from the dropdown.**

-**In the expression window, type `make_point("longitude", "latitude")`.** This will give the object a shape at the correct location.
  - ![image](https://github.com/user-attachments/assets/7ff65f64-3fd3-42c0-afa0-263b8f0d7632)
  
- **Save your changes by clicking "Save Edits".**
  
- **Then turn off Edit Mode.**
  - ![image](https://github.com/user-attachments/assets/0c4c1f9e-903f-4819-945f-a68850ae403d)
  
- **Once everything has been given a shape, everything should appear on the map.**
  - ![image](https://github.com/user-attachments/assets/6b978f98-34d7-4922-a110-2430627d53b5)

- *(If it doesn't, check the CRS of the geotagged photo layer or double-check the settings you used for Step 3a and make sure they are correct.)*
