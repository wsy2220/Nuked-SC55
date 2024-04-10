# Nuked SC-55
Roland SC-55 emulator, by nukeykt.

Supported models:
- SC-55mk2 (v1.01 firmware is confirmed to work)
- SC-55mk1 (v1.21/v2.0 firmwares are confirmed to work)
- CM-300/SCC-1 (v1.10/v1.20 firmwares are confirmed to work)
- SC-55st (v1.01)

Special thanks:
- John McMaster: SC-55 PCM chip decap.
- org/ogamespec: deroute tool.
- SDL team.
- Wohlstand: linux/macos port.
- mattw.
- HardWareMan.

## Status

3 ICs are needed to be emulated:
- Roland PCM chip
- Hitachi H8/532 MCU
- Mitsubishi M37450M2 MCU

MCUs are emulated using info from their datasheets. PCM chip info is derived from analyzing decapped chip.

### PCM chip tracing progress

![pcm_tracing.jpg](pcm_tracing.jpg)

### MCU emulation progress

![mcu1.png](mcu1.png)

![mcu2.png](mcu2.png)


## Install

Put firmware image into the same folder as Nuked SC-55. Files should be names as such:

```
SC-55mk2 (v1.01):
R15199858 (H8/532 mcu) -> rom1.bin
R00233567 (H8/532 extra code) -> rom2.bin
R15199880 (M37450M2 mcu) -> rom_sm.bin
R15209359 (WAVE 16M) -> waverom1.bin
R15279813 (WAVE 8M) -> waverom2.bin

SC-55st (v1.01):
R15199858 (H8/532 mcu) -> rom1.bin
R00561413 (H8/532 extra code) -> rom2_st.bin
R15199880 (M37450M2 mcu) -> rom_sm.bin
R15209359 (WAVE 16M) -> waverom1.bin
R15279813 (WAVE 8M) -> waverom2.bin

SC-55 (v1.21):
R15199778 (H8/532 mcu) -> sc55_rom1.bin
R15209363 (H8/532 extra code) -> sc55_rom2.bin
R15209276 (WAVE A) -> sc55_waverom1.bin
R15209277 (WAVE B) -> sc55_waverom2.bin
R15209281 (WAVE C) -> sc55_waverom3.bin

SC-55 (v2.0):
R15199799 (H8/532 mcu) -> sc55_rom1.bin
R15209387 (H8/532 extra code) -> sc55_rom2.bin
R15209276 (WAVE A) -> sc55_waverom1.bin
R15209277 (WAVE B) -> sc55_waverom2.bin
R15209281 (WAVE C) -> sc55_waverom3.bin

CM-300/SCC-1 (v1.10):
R15199774 (H8/532 mcu) -> cm300_rom1.bin
R15279809 (H8/532 extra code) -> cm300_rom2.bin
R15279806 (WAVE A) -> cm300_waverom1.bin
R15279807 (WAVE B) -> cm300_waverom2.bin
R15279808 (WAVE C) -> cm300_waverom3.bin

CM-300/SCC-1 (v1.20):
R15199774 (H8/532 mcu) -> cm300_rom1.bin
R15279812 (H8/532 extra code) -> cm300_rom2.bin
R15279806 (WAVE A) -> cm300_waverom1.bin
R15279807 (WAVE B) -> cm300_waverom2.bin
R15279808 (WAVE C) -> cm300_waverom3.bin

```

## License

Nuked SC-55 can be distributed and used under the original MAME license (see LICENSE file).
Non-commercial license was chosen to prevent making and selling SC-55 emulation boxes using (or around) this code, as well as preventing from using it in the commercial music production.

## Additional info

- Nuked SC-55 will listen to the specified MIDI IN port (default is port 0). Use `-p:<port_number>` command line argument to specify port number. To use it with the other applications use external MIDI pipe software (e.g. loopMIDI).

- SC-55mk2/SC-55mk1 buttons are mapped as such (currently hardcoded):

```
Q -> POWER
W -> INST ALL
E -> INST MUTE
R -> PART L
T -> PART R
Y -> INST L
U -> INST R
I -> KEY SHIFT L
O -> KEY SHIFT R
P -> LEVEL L
LEFTBRACKET  -> LEVEL R
A -> MIDI CH L
S -> MIDI CH R
D -> PAN L
F -> PAN R
G -> REVERB L
H -> REVERB R
J -> CHORUS L
K -> CHORUS R
LEFT -> PART L
RIGHT -> PART R
```

- `-mk2`, `-st`, `mk1` and `-cm300` command line arguments can be used to specify rom set. If no model is specified emulator will try to autodetect rom set (based on file names). 

- Due to a bug in the SC-55mk2's firmware, some parameters don't reset properly on startup. Do GM, GS or MT-32 reset using buttons to fix this issue.
