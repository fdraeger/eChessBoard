# eChessBoard
Chess board which recognizes pieces

## Requirements
| Requirement | Importance |
|-----------------------|-------|
| piece recognition by type and color. 12 unique types. | must |
| no delays while playing | must |
| realtime piece move recording. moving (short board read cycles) | nice |
| Look&Feel like high quality wooden chessboard. max board height 30mm | must |
| hidden RGB led per square | nice |
| support and recognize all chess moves (takes, castling, promotion) | must |
| support custom chess starting positions | must |
| indexing/coding of new pieces to add/replace pieces. | must |
| chess board web interface & live game streaming | nice |
| DGT chess clock interface compatibility | nice |
| online chess engine interface - play against engine (requires LED) | nice | 
| play checkers, too | nice |

## LC Resonance
LC oscillators inside the pieces are forced into oscillating at their specific resonance frequency.

Their resonance is measured for each square and the piece type is recognized.

![LC-Chess Concept_v2](https://github.com/fdraeger/eChessBoard/assets/19647221/30177d53-11b4-4d84-bec9-5f01f5fe459e)

### Questions
First stage:
*  Will the LM384 5W Amp setup be sufficient to start ? Frequency issues when dealing with 300kHz ? Coil will be around 2 Ohms, is that an issue?
*  What coil inductance aspects should be considered to stimulate the LC element? Inductance? Ideally it is a PCB coil.

Stage two (reading LC signal):
*  do we need an amplifier? Specs? Reference Schematic?
*  Converting RecvCOil signal into square wave pulses for easy frequency detection. IC for this? reference schematic?
*  are there ICs for freq measurements (in our frequancy range)?
*  reference cases for measuring frequencies with an ESP32 (or other, separate µCTRLR)


## Development Steps

### Phase One: Build stimulating part
Build a POC: signal generation, amplifier, sending coil.
    >Generate a clean signal at the coil in the frequency range of 90kHZ - 300kHZ
    >
    >  [AD9833](https://www.analog.com/media/en/technical-documentation/data-sheets/AD9833.pdf) ==> [LM384](https://www.ti.com/lit/ds/symlink/lm384.pdf)  ==> Send Coil
    >
    >? Will the LM384 amp schematic be sufficient

Make various LC Element configurations for evaluation
    >Experiment with different coil sizes and LC parameters
    >
    >? what would a "good" inductance range be? 1mH, 10mH, ...?
    >
    >? LC Element: what is a good frequency range?
    >
    >? LC Element: how small can you get?
    >
    >? LC Element: ferrit core? Y/N?
    >
    >How clearly can we separate/distinct resonance frequencies? We need 12 frequencies clearly distinguishable.
    >Ideally we work with fixed resonance frequencies (no freq sweep).

### Phase Two: Measure LC element frequency
POC: Reading Coil, Detection & ADC
    >? do we need an amp after the coil?
    >  RECV COIL ==> AMP ==> ENV DETECTION ==> ADC
    >
    >? What are otions to detect the LC resonance frequency? Are there Freq detection chips?
    >How can the signal be transformed into rectangular shape?
    >
    >? Can we use hall sensors and count their trigger signals on the LC magnetic field changing polarity?
    >eg. [A1101](https://www.allegromicro.com/~/media/Files/Datasheets/A110x-Datasheet.ashx)


## Alternate Concepts
### RFID
An RFID tag is placed into the piece.
For each square, an RFID read operation is performed and pieces are recognized by their specific ID.


