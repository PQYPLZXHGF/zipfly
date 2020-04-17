# Buzon - ZipFly

ZipFly is a zip archive generator based on zipfile.py.
It was created by Buzon.io to generate a file zip on-the-fly or on-demand in a python application.


# Install
    pip install zipfly

# Basic usage

```python
    import zipfly
    
    # key : filesystem -> path from your disk
    # key : name -> This is how it will appear in the zip file\

    paths = [ 
        {
            'filesystem': 'file.mp4', 
            'name': 'movies/file.mp4', 
        },       
        {
            'filesystem': 'background.jpg', 
            'name': 'pictures/background.jpg', 
        },          
    ]

    zfly = zipfly.ZipFly(paths=paths)

    # write a file in disk
    with open("test.zip", "wb") as f:
        for i in zfly.generator():
            f.write(i)

```

## Examples


### File-zip size before creating it

```python
    import zipfly
    
    files_size_in_bytes = 9000000 # file.mp4 + background.jpg
    
    zfly = zipfly.ZipFly(paths=paths, store_size=files_size_in_bytes)

    # total file-zip's size
    print ( zfly.buffer_prediction_size() )


```


### Django - Streaming multiple files in a zip

```python
    
    from django.http import StreamingHttpResponse
    import zipfly


    zfly = zipfly.ZipFly(mode='w', paths=paths)
    
    # create generator by chunks
    z =  zfly.generator()

    response = StreamingHttpResponse(
        z, content_type='application/octet-stream'
    )          

    return response 
```

### Streaming a large file
#### Efficient way to read a large binary file python

```python
    import zipfly

    # Efficient way to read a large binary file python

    file_location = '/home/newton/Documents/file-15GB.csv'

    go_to_streaming = zipfly.from_one_file(file_location)
    # >>> <generator object from_one_file at 0x7f85aad34a50>
    
```



# Requirements
Python > 3.5

# License
This library was created by Buzon.io and is released under the MIT. Copyright 2019 Grow HQ, Inc.