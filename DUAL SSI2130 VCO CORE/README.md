# DUAL SSI2130 VCO SUBMODULE

Dual analog VCO submodule built around two Sound Semiconductor SSI2130 oscillator cores, intended as a reusable building block for larger synth designs and digitally-assisted analog voice architectures.

> **Status:** Revision 3.0 schematic dated 2026-07-07.

## Overview

This submodule implements **two complete SSI2130 VCO packages** with supporting analog circuitry for:

- Exponential pitch control inputs
- Fine tune input
- Scale trim
- HF trim / high-frequency compensation
- PWM control
- Through-zero FM and PM support
- Hard and soft sync
- Auxiliary waveform and mixer inputs
- Buffered waveform outputs
- Per-oscillator measurement outputs for calibration, tuning, or digital supervision
- Edge-connector integration to a carrier board

The design is well suited for:

- Polyphonic analog synth voice cards
- Eurorack or desktop oscillator platforms
- Digitally-assisted analog oscillators
- Research and experimentation around SSI2130-based oscillator circuits

## What this submodule offers

### Two full SSI2130 voices

Each voice contains one SSI2130 with its own surrounding support circuitry, giving you two matched oscillator cores in one reusable schematic block.

### Buffered outputs

Each oscillator provides dedicated buffered outputs for:

- Triangle
- Saw
- Sine
- Pulse
- Mix
- Square / measurement path

This makes the submodule easier to integrate into a larger system without placing all buffering responsibility on the carrier board.

### Multiple pitch-control paths

The schematic exposes several pitch-related inputs per oscillator, including multiple V/oct inputs, fine tune, scale trim, and trim/control injection nodes. That makes the design suitable both for classic analog CV routing and for MCU-assisted correction or calibration schemes.

The scale is set to accept a 1V/OCT standard, but it needs to be trimmed by feeding voltae into the SCALE_TRIM input. This can be done with a DAC or manually using a trimmer resistor and a voltage source. An example setup is included in the original schematic.

There are three V/OCT inputs and one FINE_TUNE input which, when combined with a 0-5V variable voltage source, will span exactly one octave. In addition to that, there is a TUNE_TRIM input designed to precisely set the root note of the oscillator. This can be done with a DAC or manually using a trimmer resistor and a voltage source. An example setup is included in the original schematic.

## Functional blocks

The schematic is organized into repeated left/right oscillator sections and a shared support area:

- **Exponential converter CVs** — multiple V/oct and tuning injection inputs
- **HF trim** — high-frequency tracking trim network
- **Scale trim** — external scaling correction input
- **Sine shaper** — external circuitry required to produce a sine wave with the SSI2130
- **Mixer** — auxiliary input buffers and gain CV inputs for the SSI2130 internal mixer
- **Outputs** — buffered/raw outputs for each waveform
- **Through-zero FM and PM** — external support circuitry for TZFM/PM
- **VCO kickstart** — startup/help circuitry for oscillator initialization
- **Power section** — local +5 V and ±2.5 V reference generation / conditioning for the submodule

### Digital control and calibration

This submodule is especially suitable for digitally-assisted analog control schemes. The exposed trim/control and measurement nodes make it practical to:

- Measure oscillator frequency from a square or measure output
- Apply pitch correction by current injection into the TUNE_TRIM or SCALE_TRIM input
- Store calibration tables in an MCU on the carrier board
- Implement startup or continuous tuning compensation

### Analog routing flexibility

Because the design exposes both standard outputs and several internal/raw nodes, it can serve as either:

- a clean finished oscillator front end, or
- a lower-level VCO core for more experimental carrier designs

### Repository contents

- `DUAL-SSI2130-VCO-CORE.pdf` — exported schematic
- `DUAL SSI2130 VCO CORE.kicad_sch` — KiCad source schematic

### Licensing

```text
Hardware license: CERN-OHL-S v2
Documentation license: CC BY-NC-SA 4.0
```

### Attribution

```text
Designed by b:art instruments
```