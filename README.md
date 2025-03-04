# Python MindsDB SDK

The Python MindsDB SDK allows you to connect to a MindsDB server from Python using the HTTP API.

## Installation

```
pip install mindsdb_sdk
```

## Example

### Connecting to the MindsDB server

You can establish a connection to the MindsDB server using the SDK. Here are some examples:

#### Connect to a local MindsDB server

```python
import mindsdb_sdk
server = mindsdb_sdk.connect()
server = mindsdb_sdk.connect('http://127.0.0.1:47334')
```

#### Connect to the MindsDB Cloud

```python
import mindsdb_sdk
server = mindsdb_sdk.connect(email='a@b.com', password='-')
server = mindsdb_sdk.connect('https://cloud.mindsdb.com', login='a@b.com', password='-')
```

####  Connect to a MindsDB Pro server

```python
import mindsdb_sdk
server = mindsdb_sdk.connect('http://<YOUR_INSTANCE_IP>', login='a@b.com', password='-', is_managed=True)
```

## Basic usage

Once connected to the server, you can perform various operations. Here are some examples:

```python
# Get a list of databases
databases = server.list_databases()

# Get a specific database
database = databases[0]  # Database type object

# Perform an SQL query
query = database.query('select * from table1')
print(query.fetch())

# Create a table
table = database.create_table('table2', query)

# Get a project
project = server.get_project('proj')

# Perform an SQL query within a project
query = project.query('select * from database.table join model1')

# Create a view
view = project.create_view('view1', query=query)

# Get a list of views
views = project.list_views()
view = views[0]
df = view.fetch()

# Get a list of models
models = project.list_models()
model = models[0]

# Use a model for prediction
result_df = model.predict(df)
result_df = model.predict(query)

# Create a model
timeseries_options = {
    'order': 'date',
    'window': 5,
    'horizon': 1
}
model = project.create_model(
    'rentals_model',
    predict='price',
    query=query,
    timeseries_options=timeseries_options
)

```

You can find more examples in this [Google colab notebook](
https://colab.research.google.com/drive/1QouwAR3saFb9ffthrIs1LSH5COzyQa11#scrollTo=k6IbwsKRPQCR
)

## API Documentation

The API documentation for the MindsDB SDK can be found at https://mindsdb.github.io/mindsdb_python_sdk/. You can generate the API documentation locally by following these steps:

### Generating API docs locally:

```commandline
cd docs
pip install -r requirements.txt
make html
```

The online documentation is automatically updated by pushing changes to the docs branch.


## Testing

To run all the tests for the components, use the following command:

```bash
env PYTHONPATH=./ pytest
```

## Contributing

We welcome contributions to the MindsDB SDK. If you'd like to contribute, please refer to the contribution guidelines for more information.

## License

The MindsDB SDK is licensed under the MIT License. Feel free to use and modify it according to your needs

