[![](https://img.shields.io/badge/Python-3.8.3-informational)](https://www.python.org/)
[![](https://img.shields.io/badge/PyInstaller-4.2-informational)](https://www.pyinstaller.org/)
[![](https://img.shields.io/github/license/Ich73/docker-pyinstaller?label=License)](/LICENSE)
# PyInstaller Docker Images

The images are Docker containers to ease compiling Python applications to binaries / exe files.

Current Python version used: `3.8.3`.  
Current PyInstaller version used: `4.2`.


## Build
To build a docker image, download the folder you want, enter it, and run:
```
docker build -t <docker-image-name> .
```

For example:
```
docker build -t pyinstaller42-py383-win64 .
```


## Usage
To build your application, you need to mount your source code into the `/src/` volume.

The source code directory should have your `.spec` file that PyInstaller generates. If you don't have one, you'll need to run PyInstaller once locally to generate it.

If the `src` folder has a `requirements.txt` file, the packages will be installed into the environment before PyInstaller runs.

In the folder that has your source code, `.spec` file and `requirements.txt` run:
  * Linux: `docker run -v "$(pwd):/src/" <docker-image-name>`
  * Windows: `docker run -v "%cd%:/src/" <docker-image-name>`

##### How do I install system libraries or dependencies that my Python packages need?

You'll need to supply a custom command to Docker to install system pacakges. Something like:
```
docker run -v "$(pwd):/src/" --entrypoint /bin/sh <docker-image-name> -c "apt-get update -y && apt-get install -y wget && /entrypoint.sh"
```
Replace `wget` with the dependencies / package(s) you need to install.
