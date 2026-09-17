# pico_bayblade_speedomeeter



cmake -S . -B build-make -DPICO_NO_PICOTOOL=ON; cmake --build build-make --target pico_bayblade_speedomeeter -j 4; & 'C:\Program Files\Raspberry Pi\Pico SDK v1.5.1\pico-sdk-tools\elf2uf2.exe' build-make\pico_bayblade_speedomeeter.elf build-make\pico_bayblade_speedomeeter.uf2;