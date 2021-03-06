### raincatcher-mongoose-store


One stop shop for all Mongoose schemas 

### Run tests

Ensure Mongo is running on your machine, type the following command

```bash
npm test
```

### Models

Mongoose models can be found in `models` directory. To add a new model use the same naming convention for desired dataset. ie. `workorders` model for `workorders` dataset / collection. Then require the directory and access the model using the name applied.

### API

#### connect

To connect to mongo


```javascript

var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var customSchemas = {
    //The key is the same as the datasetId (e.g. workorders)
    workorders: function(mongooseConnection) {
        var customWorkorderSchema = new Schema({
            ...
            name: {type: String}
            ...
        },  {timestamps: true});
        
        mongooseConnection.model('CustomWorkorderModel', customWorkorderSchema);
    }
    ... 
    //Any other custom schemas
    ...
};

Connector.connect('mongodb://mongoUriGoseHere:27017/db', {}, customSchemas)
  .then(function() {
    // connected successfully
  }, function(error) {
    // An error occurred when connecting
  });
```

#### getDAL

Get the Data access layer object for a collection/dataset.

```javascript

var datasetId = "workorders";

Connector.getDAL(datasetId).
  then(function(_dal) {
    // do stuff with dataset dal
  }, function(error) {
    // handle error
  });
```

#### disconnect

```javascript
Connector.disconnect()
  .then(function() {
    // disconnected
  }, function(error) {
    // something went wrong
  });
```
