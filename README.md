# CLARI-Project
 - Made in QGIS 3.63.3
   
  QGIS (Quantum Geographic Information System) is a free, open-source software used for mapping and spatial data analysis. It enables users to create, edit, visualize, and analyze geospatial data, supporting a wide range of file formats and databases. QGIS is popular for creating interactive maps, conducting geographic research, and managing spatial information for various applications like urban planning, environmental management, and fieldwork. It’s versatile, extensible through plugins, and can be integrated with other software and online services.
 
# How To Use
  - Download Repository
  - Extract folder
  - Click Index.html to launch in your browser
            OR
  - download the raw project files for qgis
# How It Was Made
  I started with importing the shape files and the excel data into QGIS, once imported I looked for similarites in the excel sheet and the shape files to join the table and the shape file in this case the PID and the Assesment number.

   - You get here by right clicking the shape file and then going to properties and selecting the join table property (Image Below).
     
  ![image](https://github.com/user-attachments/assets/082d7a27-6c36-401f-a7ef-19618b52abc5)
  
   With the excel sheet joined to the shape file all excel data should be part of the shape features table.
   
 ![image](https://github.com/user-attachments/assets/03026daa-3f06-464a-973a-667efd6eb2ef)

To create the 30m shoreline buffer i created a new shapefile and used the trace tool to draw the shoreline. 
 - To get the trace tool you need to right click your toolbar and tick off the "snapping tool bar" once turned on this will allow your newly drawn line to snap to the shapefiles creating a very tight shoreline.(Tip click to make checkpoints and make alot of them to avoid errors!)
 - ![image](https://github.com/user-attachments/assets/741f6a5f-2a94-46ba-a79f-aac628b63108)
 - Once the new shoreline is drawn youll need to use it to create your buffer by going too Vector-> geoprocessing tools -> Buffer set your input layer to be the line shapefile youve just created. (Note: your buffer will be X meters on both sides of your drawn line unless otherwise specified: the image below shows the buffer settings I used)
 - ![image](https://github.com/user-attachments/assets/38e60855-9be0-4bbf-8430-d561c552f13e)
 - To delete the data inside the buffer to avoid overlap go back to Vector -> Geo Processing -> Diffrence this will remove the data inside the buffer zone without deleting the feature all together. You want the input layer to be the original shapefile and the overlay layer to be the buffer layer you made in the previous step.
 - ![image](https://github.com/user-attachments/assets/010c9ba8-dccf-49b9-921b-ae173e75fd98)
 - Once this is done you can add labels to the shapes by clicking the label button and selecting which data in the table you want shown.
 - ![image](https://github.com/user-attachments/assets/47819c58-fe8a-40a8-9fdd-752426643a11)
 - Now to convert this into a interactive version youll need the qgis2webapp plugin. This can be downloaded and installed directly into the app by going to plugins -> manage and install plugins -> search qgis2web -> install
 - ![image](https://github.com/user-attachments/assets/0a0ae60d-344c-4df5-9b0a-17bf0e56d07a)
 - Finally run qgis2web and select your buffer and diffrence layers that you made, choose your settings and needs for the web app youll have open layers and leaflet to choose from for a framework ( i personally prefer leaflet it gives you more features out of the box.( IMPORTANT if your shapefile doesnt show up its because your layer CRS is set incorrectly for the web map so if your preview looks empty check your CRS). Once you select your basic settings and hit EXTRACT qgis will create a basic webapp in html and javascript format so you have full access to the code to add, change and remove features as needed.
 - ![image](https://github.com/user-attachments/assets/ff65e9c3-3384-4fdc-ab0f-c93685eb5b3e)

# How To automatically add geotagged photos

- To add geotagged photos to your web map I recommend you follow this guide "https://opengislab.com/blog/2020/8/23/mapping-and-viewing-geotagged-photos-in-qgis" it shows you how to import geotagged photos to your map and places them based on their longitude and latitude and also how to convert your geotagged images and map into a webapp.

# How To manually add geotagged photos

- Follow the above tutorial until you have completed steps 1, 2 and 3a. (DONT DO STEP 3 JUST 3A unless you know the direction of the geotagged photo) 
- Once thats complete and you have created your geotagged layer right click and goto the attributes table.
- ![image](https://github.com/user-attachments/assets/f05bc69d-7bc4-44b1-a745-07cc5144890b)
- Click on "toggle edit" and then "add feature"
- ![image](https://github.com/user-attachments/assets/76a95bed-6d4f-4527-8ce3-0f696eb5f6c8)
- leave the fid field as "autogenerate"
- click the 3 dots next to photo and select your desired photo
- fill in the filename this can be whatever you want it to be so make it easy to identify in your attribute table
- then fill in the longitude and latitude fields for your images location
- You should have something like the image below
- ![image](https://github.com/user-attachments/assets/bd60f1bf-0284-459c-868b-055084936361)
- make sure youve added all your photos and their latitude and longitudes before moving onto the field calculator section the shapes should be added once all photos are in the table.
- Now we have to give the new attribute in the table a shape to appear on the map.
- open the field calculator
- ![image](https://github.com/user-attachments/assets/334e1c4d-dc00-42ee-b33c-4cd016e11418)
- once open check off "Update existing field" and select "<geometry>" from the drop down
- in the expression window type make_point("longitude", "latitude") this will give the object a shape at the correct location
- ![image](https://github.com/user-attachments/assets/7ff65f64-3fd3-42c0-afa0-263b8f0d7632)
- Save your changes by clicking "save edits"
- Then turn the edit mode off
- ![image](https://github.com/user-attachments/assets/0c4c1f9e-903f-4819-945f-a68850ae403d)
- once everything has been given a shape everything should appear on the map
- ![image](https://github.com/user-attachments/assets/6b978f98-34d7-4922-a110-2430627d53b5)

- (if it doesnt check the crs of the geotagged photo layer or double check the settings you used for step 3a and make sure they are correct)






