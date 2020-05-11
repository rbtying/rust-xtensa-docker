Use Dockerized rustc for crossbuild:

```
docker run --rm --mount type=bind,source="$(pwd)",target=/project rbtying/esp-crossbuild-env cargo +xtensa xbuild --target xtensa-esp32-none-elf --release
```
