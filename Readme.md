Este es mi CV, esta basado en [friggeri-resume-cv](https://www.latextemplates.com/template/friggeri-resume-cv)

# Compilación

## Local

Para construir localmente utilizar el comando, estando en root del repositorio.

```bash
docker run --mount src=$(pwd)/src,target=/usr/src/tex,type=bind dxjoke/tectonic-docker /bin/sh -c "tectonic cv.tex"
```

## GitHub Actions (Automatizado)

El proyecto ahora utiliza GitHub Actions para compilación automática y releases:

### Pre-releases (Main Branch)
- **Trigger:** Cada push a la rama `main`
- **Output:** Pre-release con nombre `CV Build - YYYY-MM-DD (commit: hash)`
- **Contenido:** PDF compilado con metadata de build

### Official Releases (Tags)
- **Trigger:** Push de tags con formato `v*` (ej: `v1.3`)
- **Output:** Release oficial con nombre `Version v1.3 - YYYY-MM-DD`
- **Contenido:** PDF compilado como asset oficial

### Workflow Features
- ✅ Validación automática de PDF (tamaño mínimo)
- ✅ Artifacts con metadata de build
- ✅ Cache de Tectonic para builds más rápidos
- ✅ Soporte para bibliografía con Biber
- ✅ Releases automáticos con información detallada

# Referencias
* https://hub.docker.com/r/dxjoke/tectonic-docker
* https://github.com/WtfJoke/setup-tectonic
* https://www.latextemplates.com/template/friggeri-resume-cv
* https://docs.github.com/en/actions
