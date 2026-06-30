# codespace-pixi
A codespace with a locked pixi python environment

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/uw-escience-cloudbank/codespace-pixi?quickstart=1)

https://pixi.prefix.dev/latest/integration/editor/vscode/#devcontainer-extension

## Troubleshooting:

Test building docker image locally:

```bash
docker buildx build --load -t codespace-pixi:test -f .devcontainer/Dockerfile .
docker images codespace-pixi:test
docker run --rm -it --hostname codespace-pixi -v $(pwd):/home/vscode codespace-pixi:test
pixi shell
```
