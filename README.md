# 7Hz Elua Ultra EQ

An EQ profile for the **7Hz Elua Ultra**, made with [AutoEq](https://github.com/jaakkopasanen/AutoEq). AutoEq doesn't have the Elua Ultra in its database yet, so apps that use AutoEq's list (such as Wavelet) don't offer it. AutoEq's "7Hz x HBB Elua" is the original Elua, a different IEM.

![7Hz Elua Ultra frequency response and EQ](./7Hz%20Elua%20Ultra.png)

## Files

| File | Use it for |
|------|------------|
| `7Hz Elua Ultra GraphicEQ.txt` | Wavelet (Android), Equalizer APO / Peace (Windows), and other apps that import AutoEq GraphicEQ files |
| `7Hz Elua Ultra ParametricEQ.txt` | Parametric equalizers: apps that take filters with a frequency, gain and Q |
| `7Hz Elua Ultra FixedBandEQ.txt` | Ordinary 10-band equalizers (31 Hz to 16 kHz) |
| `7Hz Elua Ultra.png` | The graph above |

## How to use it

### Wavelet (Android)

1. Download `7Hz Elua Ultra GraphicEQ.txt` to your phone.
2. Import it in Wavelet. Wavelet can import AutoEq GraphicEQ files; where the option sits depends on your version.
3. Use one headphone profile at a time. If Wavelet's AutoEq is still set to another model (the original 7Hz x HBB Elua, say), turn it off or replace it, so the two corrections don't stack.
4. Keep Wavelet's limiter on.

### Parametric EQ

Set the preamp first so the boosts can't clip.

**Preamp: -1.9 dB**

| # | Type | Frequency | Gain | Q |
|---|------|-----------|------|---|
| 1 | Low shelf | 105 Hz | -2.9 dB | 0.70 |
| 2 | Peak | 759 Hz | +1.2 dB | 0.74 |
| 3 | Peak | 5962 Hz | +1.9 dB | 2.75 |
| 4 | Peak | 164 Hz | -1.1 dB | 2.08 |
| 5 | Peak | 1313 Hz | -1.6 dB | 1.93 |
| 6 | High shelf | 10000 Hz | -7.7 dB | 0.70 |
| 7 | Peak | 8486 Hz | +2.2 dB | 1.69 |
| 8 | Peak | 66 Hz | +0.7 dB | 1.90 |
| 9 | Peak | 24 Hz | -0.5 dB | 3.51 |
| 10 | Peak | 32 Hz | -0.4 dB | 2.38 |

If your app has fewer than 10 filters, use 1 to 7. Filters 6 and 7 go together: 6 cuts the treble above 10 kHz, and 7 keeps that cut from reaching down to 8 kHz. Filters 8 to 10 are small tweaks below 70 Hz. With only 5 filters, use 1 to 5; that leaves the treble above 10 kHz as it is.

### 10-band EQ

**Preamp: -1.0 dB**

| 31 Hz | 62 Hz | 125 Hz | 250 Hz | 500 Hz | 1 kHz | 2 kHz | 4 kHz | 8 kHz | 16 kHz |
|-------|-------|--------|--------|--------|-------|-------|-------|-------|--------|
| -3.7 | -1.1 | -1.4 | -0.3 | +1.2 | +0.1 | -0.7 | +1.0 | +1.5 | -12.0 |

## What it changes

- **Bass:** about -3 dB below 40 Hz, easing to about -1.5 dB from 70 to 150 Hz. The Elua Ultra has about 3 dB more sub-bass than AutoEq's target, which already includes an 8 dB bass boost, so the bass stays boosted, just by less.
- **Lower mids:** a little under +1 dB from 400 to 800 Hz, for a touch more body in vocals and instruments.
- **Around 1.3 kHz:** about -1 dB, evening out a slight bump.
- **2 to 5 kHz:** almost untouched. The Elua Ultra already follows the target closely here.
- **Around 6 kHz:** about +2 dB, filling a small dip between the peaks at 3 kHz and 8 kHz.
- **Treble above 10 kHz:** cut progressively, from about -2 dB at 10 kHz to about -7.5 dB at 16 kHz. The Elua Ultra measures with a lot more energy up there than AutoEq's target. This is the biggest change in the profile; AutoEq's own result for the original Elua makes a similar cut.

## How it was made

1. **Measurements.** Elua Ultra measurements from seven squig.link databases: [Aftersound](https://aftersound.squig.link), [Audio Amigo](https://audioamigo.squig.link), [Bass Audio](https://bassaudio.squig.link), [CSI-Zone](https://csi-zone.squig.link), [Jaytiss](https://jaytiss.squig.link), [Paul Wasabi](https://pw.squig.link) and [Vortex Reviews](https://vortexreviews.squig.link). Each one's left and right channels were averaged and set to 0 dB at 1 kHz, then the seven were averaged together. Each is within about 0.2 to 0.7 dB RMS of that average from 20 Hz to 8 kHz, and leaving any one of them out moves the average by about 0.1 dB RMS at most.
   - Three more measurements differed clearly from the rest and were left out: [DucBloke](https://ducbloke.squig.link) (about 2.5 dB more upper bass), [ATechReviews](https://atechreviews.squig.link) (about 3 dB less deep bass, and about 1 dB more from 2 to 8 kHz) and [Soundcheck39](https://soundcheck39.squig.link) (close to the rest below 6 kHz, but with a peak around 8 kHz 4 to 5 dB smaller).
   - [Soundignity](https://soundignity.squig.link) hosts the same file as CSI-Zone, so it was counted once. [Hangout.Audio](https://graph.hangout.audio)'s measurement was made on a B&K 5128 rig, which isn't comparable with the others. Audio Amigo's 15 Ω and 30 Ω measurements weren't used (see Limits).
2. **EQ.** Generated with AutoEq 4.1.2:
   ```
   python -m autoeq --input-file "7Hz Elua Ultra.csv" --output-dir results --target "AutoEq in-ear.csv" --bass-boost 8 --parametric-eq --fixed-band-eq --fs 48000
   ```
   The target is AutoEq's own in-ear target with an 8 dB bass shelf, the same target AutoEq uses for its published in-ear results.
3. **Check.** The same steps run on [Jaytiss's](https://jaytiss.squig.link) measurement of the original 7Hz x HBB Elua reproduce AutoEq's published result for it. The GraphicEQ file comes out identical, and at 44.1 kHz, the sample rate AutoEq's published files use, the parametric and 10-band EQ curves match to within 0.01 dB. This profile is fitted at 48 kHz, the usual rate on Android; the GraphicEQ is the same either way.

The averaged measurement isn't included here, since the data belongs to the people who measured it. It's freely viewable on their sites.

## Limits

- **It's a starting point, not a perfect fit.** Measurement rigs model an average ear. Above about 5 kHz, your own ear canal, the tips you use and how deep they sit can change what you hear by several dB.
- **The treble cut is the least certain part.** Above 10 kHz the measurements disagree most and ears differ most. If the Elua Ultra sounds dull or closed-in with this profile, ease the cut: raise filter 6 part of the way toward 0 dB, raise the 16 kHz slider (it sits at AutoEq's -12 dB limit), or add a little treble on top of the GraphicEQ.
- **If it sounds sharp or tiring,** lower the band around 6 kHz first.
- **Want more bass?** Raise the bass below about 100 Hz to taste, or bring filter 1 back toward 0 dB.
- **Use a low-impedance source.** Audio Amigo's measurements show the Elua Ultra's bass rising by 1 to 2 dB below 100 Hz on a source with 15 to 30 Ω output impedance. The profile assumes a source close to 0 Ω, as most dongles and DACs are.
- **Units vary.** Your pair can differ from the measured ones by a dB or two.

## Credits

- Measurements: **Aftersound**, **Audio Amigo**, **Bass Audio**, **CSI-Zone**, **Jaytiss**, **Paul Wasabi** and **Vortex Reviews**, for publishing their measurements.
- [AutoEq](https://github.com/jaakkopasanen/AutoEq) by Jaakko Pasanen, which did the EQ maths.

Not affiliated with 7Hz.
