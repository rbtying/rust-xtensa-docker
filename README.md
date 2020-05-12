Use Dockerized rustc for crossbuild:

Set up a user-specific container:
```
docker build -t rbtying/esp-crossbuild-env-user --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) esp-crossbuild-env
```

Then run the compile from inside of the new container:
```
docker run --rm --mount type=bind,source="$(pwd)",target=/project rbtying/esp-crossbuild-env-user cargo +xtensa xbuild --target xtensa-esp32-none-elf --release
```

Binding a different directory and using `-w` to set the working directory is also useful:
```
docker run --rm --mount type=bind,source="$WORKSPACE_DIR",target=/project -w "/project/$PATH_RELATIVE_TO_WORKSPACE_DIR" rbtying/esp-crossbuild-env-user cargo +xtensa xbuild --target xtensa-esp32-none-elf --release
```
