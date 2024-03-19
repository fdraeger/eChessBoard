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
![LC-Chess Concept_v2](https://github.com/fdraeger/eChessBoard/assets/19647221/f4ed7cbb-b8b4-464f-8bc2-8b8abed7b2ed)

### Questions
Stimulating part:
*  Will the LM384 5W Amp setup be sufficient to start? Fmax ~300kHz? Coil ~2 Ohms.
*  What coil inductance aspects should be considered to stimulate the LC element? 1mH? 10mH? Does it matter? Ideally it is a PCB coil.
*  How long will a resonace last? If it last long enough, we could scan an entire row (8 readings) in one go.

Reading LC signal:
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
>Can we use the [ESP32 pulse counter feature](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/pcnt.html)? 
>
>? Can we use hall sensors and count their trigger signals on the LC magnetic field changing polarity?
>eg. [A1101](https://www.allegromicro.com/~/media/Files/Datasheets/A110x-Datasheet.ashx)
>probably too slow (signal raise & falling times of 400ns)
>


## Alternate Concepts
### RFID
An RFID tag is placed into the piece.
For each square, an RFID read operation is performed and pieces are recognized by their specific ID.

Selection of transponders and readers needs to match supported protocols. Main protocols are MIFRAE, ISO 14443 (low range< 10cm) and 15693 (long range <60cm).
The popular MFRC522 chip does not support the 15693. Bummer, because there is a super small ( 4x4x0.7mm) transponder (thanks Paul Kelly for pointing this out).
14443 transponders get as small as 8x5mm, but cost about 1€ each.

I tried a MFRC522 test setup and must say, the behaviour is quite good.
Alternatives are: NXPs [PN5180](https://www.nxp.com/docs/en/data-sheet/PN5180A0XX_C3_C4.pdf) or [ST25Rxxx](https://www.st.com/en/nfc/st25-nfc-readers.html) series from ST

Even though the RFID concept seems easy, the major challenge will be to desing PCB antenna.





