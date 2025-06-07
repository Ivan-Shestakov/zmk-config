### Building keymap locally

in ~/zmk run devcontainer by
```
podman run -it --rm \                                                                                                                                                     main~/code/zmk
  --security-opt label=disable \
  --workdir /workspaces/zmk \
  -v ~/code/zmk:/workspaces/zmk \
  -v ~/code/zmk-config:/workspaces/zmk-config -p 3000:3000 zmk /bin/bash
```

This starts local dev container with all build dependencies and the custom config mounted under /workspaces/zmk-config

Once inside repeat these commands to build the firmware and rename the result 
`west build -s app -d /workspaces/zmk/build/ -b nice_nano_v2 -- -DZMK_CONFIG=/workspaces/zmk-config/config -DSHIELD=dm_4x5_left`
`mv build/zephyr/zmk.uf2 build/zephyr/dm_4x5_left.uf2`
`west build -s app -d /workspaces/zmk/build/ -b nice_nano_v2 -- -DZMK_CONFIG=/workspaces/zmk-config/config -DSHIELD=dm_4x5_right`
`mv build/zephyr/zmk.uf2 build/zephyr/dm_4x5_right.uf2`

To flash, connect the nrfmicro via USB-C cable, and quickly short RST and GND pins twice, a USB drive should be detected, copy the .uf2 file there. 
