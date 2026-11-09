# Is It Over? — Robotic Puppetry & Interactive Theatre

> **Featured photograph:** [view the first eye image from the official Moment gallery](https://moment.si/wp-content/uploads/2022/11/195A3900.jpg) — photograph by **Boštjan Lah**; [production page and source gallery](https://moment.si/en/performance/is-it-over/).
>
> The image is linked rather than stored in this repository because the official pages identify the photographer but do not publish a licence authorising redistribution. This preserves a clear path to the original and its context.

*Je že konec? / Is It Over?* is an experimental theatre performance about the final moments before an imagined apocalypse. Framed as the planet's last safe space, it invites an audience to encounter last wishes, private fears, unspoken words and the difficult question of how people might remain together when time runs out.

Premiered on 25 November 2022 at Intimni oder GT22 in Maribor, the work was co-produced by [Moment](https://moment.si/en/performance/is-it-over/) and [Maribor Puppet Theatre](https://www.lg-mb.si/en/past-seasons/is-it-over-yet/). It combines devised performance, object theatre, audience interaction and a deliberately handmade technological language. The repository preserves two Arduino sketches developed for its joystick-controlled, pan/tilt puppet mechanisms.

## Artistic concept and production

The performance shifts the apocalypse away from spectacle and towards human relationships. Under the pressure of a countdown, its performers and audience move through questions of survival, trust, vulnerability and the possibility of imagining a different world. The production's DIY visual vocabulary brings everyday objects, puppet forms and technology into the same theatrical space.

The concept was created by Ariel Doron, Maša Radi Buh and Nika Bezeljak. Nika Bezeljak directed, Maša Radi Buh served as dramaturge, and Miha Bezeljak, Uroš Kaurin and Gregor Prah devised and performed the work. Monika Pocrnjić created the visual design and technology. The performance was recognised with the ZIZ award for performance at the 2023 ZIZ Festival.

## Robotic puppetry

The two sketches implement the same compact control idea: a two-axis analog joystick becomes a direct movement interface for two hobby-servo channels. The Arduino reads the joystick's horizontal and vertical signals, maps each 10-bit reading (`0–1023`) to a servo command (`0–180` degrees), and continuously sends the resulting positions to the two servos.

This is a pan/tilt control pattern rather than an autonomous robot. Movement comes from the performer through the joystick; the microcontroller translates that gesture into paired servo positions. The mechanism therefore sits between puppet control and robotic actuation: human timing and intention remain central, while the electronics convert small hand movements into the motion of a stage object.

### Connections visible in the code

| Function | `ptservojoy.ino` | `ptservojoy2.ino` |
|---|---:|---:|
| Joystick X / `VRX` | `A0` | `A0` |
| Joystick Y / `VRY` | `A1` | `A1` |
| X-axis servo signal | Digital pin `10` | Digital pin `5` |
| Y-axis servo signal | Digital pin `9` | Digital pin `6` |
| `led` variable | Digital pin `5` | Digital pin `5` |
| Serial monitor | `9600` baud | `9600` baud |

Both sketches use Arduino's standard [`Servo`](https://docs.arduino.cc/libraries/servo/) library. Each loop also writes a full PWM value (`255`) to the pin named `led` and prints raw joystick readings and mapped servo angles to the serial monitor.

> **Archival note:** in `ptservojoy2.ino`, digital pin `5` is assigned to both `SERVO_X_PIN` and `led`. The sketch is preserved unchanged, but this pin conflict should be reviewed before recreating the circuit. The repository does not contain a schematic, bill of materials or servo model, so no further electrical assumptions are made here.

## Arduino sketches

### `ptservojoy.ino`

The first variant attaches the two servo objects to pins 10 and 9. It reads the joystick on A0 and A1, maps both axes across the full nominal servo-command range, and reports the input and output values over serial.

### `ptservojoy2.ino`

The second variant performs the same mapping and serial reporting but attaches the servo objects to pins 5 and 6. As noted above, pin 5 is also used by the `led` variable in this version.

### Running a sketch

1. Open one `.ino` file in the Arduino IDE.
2. Confirm the signal-pin assignments against the physical build before connecting hardware.
3. Select the appropriate Arduino board and port.
4. Compile and upload the sketch.
5. Open the serial monitor at `9600` baud to inspect joystick readings and commanded angles.

The sketches contain no calibration, dead zone, easing or mechanical-limit settings. Before using them with a reconstructed mechanism, check that the full commanded range is safe for the actual linkage and servos.

## Movement as artistic experimentation

In live puppetry, movement is never merely an engineering output. A pause, tremor, overshoot or sudden turn can become character, attention or emotion. These sketches expose a simple translation layer between the performer's hand and the puppet's two axes, leaving the expressive decisions with the operator.

That simplicity is artistically productive. It makes the mechanism legible, allows movement to be discovered through rehearsal, and supports a DIY aesthetic in which wires, joints, electronics and handmade objects can remain part of the theatrical language. The code is consequently best read as production material: a small technical score embedded in a larger process of performance and experimentation.

## Credits

- **Concept:** Ariel Doron, Maša Radi Buh, Nika Bezeljak
- **Authors and performers:** Miha Bezeljak, Uroš Kaurin, Gregor Prah
- **Director:** Nika Bezeljak
- **Dramaturge:** Maša Radi Buh
- **Visual design and technology:** Monika Pocrnjić
- **Lighting and space design:** Andrej Firm
- **Sound design:** Gašper Torkar
- **Lighting design:** Gašper Bohinec
- **Language editor:** Metka Damjan
- **Executive production:** Lana Bauman, Nika Bezeljak
- **Public relations:** Anamarija Nađ (Moment), Špela Hren Juhart (Maribor Puppet Theatre)
- **Photography:** Boštjan Lah
- **Co-production:** Moment and Maribor Puppet Theatre
- **Support:** Ministry of Culture of the Republic of Slovenia and Municipality of Maribor

Credits and production details are drawn from the official Moment, Maribor Puppet Theatre and SiGledal records linked below.

## Production, reviews and documentation

- [Moment — official English production page](https://moment.si/en/performance/is-it-over/)
- [Maribor Puppet Theatre — official English archive page](https://www.lg-mb.si/en/past-seasons/is-it-over-yet/)
- [SiGledal — production record](https://veza.sigledal.org/uprizoritev/je-ze-konec)
- [Andrej Firm — project page](https://www.andrejfirm.com/is-it-over/)
- [Zlata paličica — expert recommendation and production record](https://www.zlatapalicica.si/predstava/je-ze-konec/)
- [“Don't Stop Me Now” — review by Petra Vidali, *Večer*](https://vecer.com/kultura/gledaliska-kritika-dont-stop-me-now-10322413)
- [“Konec sveta” — review by Tjaša Bertoncelj, SiGledal](https://veza.sigledal.org/kritika/konec-sveta-r)
- [Trailer — Moment on Vimeo](https://vimeo.com/786279788)

For annotated sources, press coverage, festival records and educational material, see [PRESS_AND_REFERENCES.md](PRESS_AND_REFERENCES.md).

## Repository scope

This repository is an archive of the Arduino control sketches and their production context. The original `.ino` files are intentionally preserved as created. No licence is currently stated for the code or production imagery; absence of a licence should not be interpreted as permission to reuse either.
