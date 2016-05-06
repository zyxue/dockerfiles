## Usage

For exmaple:

```
docker run --shm-size 1024MB --rm -ti -v ${PWD}:/home/linuxbrew/workdir zyxue/python-data-analytics-env:latest /bin/bash

cd workdir/

jupyter notebook --ip 0.0.0.0 --no-browser
```
