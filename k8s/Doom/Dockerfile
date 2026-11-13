FROM ghcr.io/trisnol/doom-wasm@sha256:175bfa92348516d9939258f7dd23c1709e54a80b6806ce0a09ee72eb39090d64

COPY doom1.wad /home/doom/doom-wasm/src/user-addon.wad

RUN curl -fsSL -o /tmp/freedoom.zip \
      https://github.com/freedoom/freedoom/releases/download/v0.13.0/freedoom-0.13.0.zip \
    && echo '3f9b264f3e3ce503b4fb7f6bdcb1f419d93c7b546f4df3e874dd878db9688f59  /tmp/freedoom.zip' \
      | sha256sum -c - \
    && python3 -c 'from zipfile import ZipFile; ZipFile("/tmp/freedoom.zip").extract("freedoom-0.13.0/freedoom1.wad", "/tmp")' \
    && cp /tmp/freedoom-0.13.0/freedoom1.wad /home/doom/doom-wasm/src/freedoom1.wad \
    && rm -rf /tmp/freedoom.zip /tmp/freedoom-0.13.0 \
    && sed -i 's/"-iwad", "doom1.wad"/"-iwad", "freedoom1.wad"/' \
      /home/doom/doom-wasm/src/index.html \
    && sed -i 's/("", "doom1.wad", "doom1.wad"/("", "freedoom1.wad", "freedoom1.wad"/' \
      /home/doom/doom-wasm/src/index.html \
    && sed -i 's/"-config", "default.cfg",/"-config", "default.cfg", "-file", "user-addon.wad",/' \
      /home/doom/doom-wasm/src/index.html \
    && sed -i '/Module.FS.createPreloadedFile("", "default.cfg",/a\                    Module.FS.createPreloadedFile("", "user-addon.wad", "user-addon.wad", true, true);' \
      /home/doom/doom-wasm/src/index.html
