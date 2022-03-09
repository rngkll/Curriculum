Este es mi CV, esta basado en [friggeri-resume-cv](https://www.latextemplates.com/template/friggeri-resume-cv)

# Compilación

## Local

Para construir localmente utilizar el comando, estando en root del repositorio.

```
docker run --mount src=$(pwd)/src,target=/usr/src/tex,type=bind dxjoke/tectonic-docker /bin/sh -c "tectonic cv.tex"
```

## Github actions


# Referencias
* https://hub.docker.com/r/dxjoke/tectonic-docker
* https://github.com/WtfJoke/setup-tectonic
* https://www.latextemplates.com/template/friggeri-resume-cv
