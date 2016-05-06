## Usage

For exmaple:

```
docker run --shm-size 1024MB --rm -ti -p 8888:8888 -v ${PWD}:/home/linuxbrew/workdir zyxue/python-data-analytics-env:latest /bin/bash

cd workdir/

jupyter notebook --ip 0.0.0.0 --no-browser
```
