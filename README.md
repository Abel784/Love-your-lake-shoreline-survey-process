# CLARI-Project
 - Made in QGIS 3.63.3

# How To Use
  - Download Repository
  - Extract folder
  - Click Index.html to launch in your browser

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





