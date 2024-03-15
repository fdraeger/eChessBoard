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
| support free chess starting positions | must |
| indexing/coding of new pieces to add/replace pieces. | must |

## LC Resonance
LC oscillators inside the pieces are forced into oscillating at their specific resonance frequency.
The resonance is measured for each square and the piece type is recognized.
![LC-Chess Concept_v2](https://github.com/fdraeger/eChessBoard/assets/19647221/73da6a58-e1e4-49db-af92-f5e03dd56589)


## Development Steps

1.  Build a POC: signal generation, amplifier, sending coil.
    >Generate a clean signal at the coil in the frequency range of 90kHZ - 300kHZ
    >
    >  [AD9833](https://www.analog.com/media/en/technical-documentation/data-sheets/AD9833.pdf) ==> [LM384](https://www.ti.com/lit/ds/symlink/lm384.pdf)  ==> Send Coil
    >
    >? Will the LM384 amp schematic be sufficient

1.  Make various LC Element configurations    
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

1.  POC: Reading Coil, Detection & ADC
    >? do we need an amp after the coil?
    >  RECV COIL ==> AMP ==> ENV DETECTION ==> ADC
    >
    >? What are otions to detect the LC resonance frequency? Are there Freq detection chips?
    >

## Alternate Concept
### RFID
An RFID tag is placed into the piece.
For each square, an RFID read operation is performed and pieces are recognized by their specific ID.


