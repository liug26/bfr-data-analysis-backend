# BFR Data Analysis Website (Backend)
### Abstract
- Creates an API for frontend to upload and manage the car's run logs (later abbreviated as "data") stored in a MongoDB database:  
   Post data request -> backend uploads data to database & updates master file in the database  
   Delete data request -> backend deletes data from database & updates master file in the database
- Generates real-time customizable time-series graphs and passes to frontend:    
   Get plot request -> backend gets parameters from query -> sends params to a python script -> python script writes HTML to a temporary local file -> backend reads the local file and sends back to frontend
- Ask the master file in the database for a hierarchical list of all existing data:  
   Get datatree request -> backend fetches master file from database -> converts it to a tree-structured JSON and sends back to frontend

### Preparations
- MongoDB database: Create a cluster that contains 2 databases: main (for storing data) and master (for storing what data are stored).
   Master: has one collection called "datalists", which has one document. It has one array entry with key "list" and values of type object: { "collectionName": data's collection's name, its 2 super folders' names separated by a slash, "entryName": data's name }. Each time a data is uploaded/removed, this list will be updated.
   Main: 
