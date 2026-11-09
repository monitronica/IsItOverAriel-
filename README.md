# *Is It Over?*

> Robotic puppetry, interactive theatre, and an archive of a handmade control system

*Je že konec? / Is It Over?* is an experimental performance set in the final moments before an imagined apocalypse. Presented as the planet's last safe space, it brings performers and audience together around last wishes, private fears, trust, vulnerability, and the question of what kind of world might remain possible.

The work combines devised performance, object theatre, audience interaction, and a deliberately DIY technological language. This repository preserves the two Arduino sketches used to translate a performer's joystick gestures into the pan-and-tilt motion of robotic stage objects.

> **Production photograph**
>
> [View the eye photograph in Moment's official gallery](https://moment.si/wp-content/uploads/2022/11/195A3900.jpg) · Photograph by **Boštjan Lah** · [Production page and full gallery](https://moment.si/en/performance/is-it-over/)
>
> The photograph remains linked to its publisher because the official sources credit the photographer but do not state a licence authorising redistribution.

| Production | Details |
| --- | --- |
| Original title | *Je že konec?* |
| English title | *Is It Over?* |
| Premiere | 25 November 2022 |
| Venue | Intimni oder GT22, Maribor, Slovenia |
| Co-producers | Moment and Maribor Puppet Theatre |
| Format | Experimental theatre / object theatre / robotic puppetry |
| Running time | 45 minutes |
| Recognition | ZIZ Award for Performance, 2023 |

## The performance

The production turns the apocalypse away from spectacle and towards relationships. Under the pressure of a countdown, the performers and audience encounter questions of survival, honesty, fear, and collective imagination. Everyday objects, puppet forms, visible electronics, and handmade mechanisms share the stage; technology is not presented as a seamless effect, but as part of the work's material and emotional vocabulary.

The concept was developed by Ariel Doron, Maša Radi Buh, and Nika Bezeljak. Nika Bezeljak directed; Maša Radi Buh was dramaturge; and Miha Bezeljak, Uroš Kaurin, and Gregor Prah devised and performed the work. Monika Pocrnjić created its visual design and technology.

The performance received the ZIZ Award for Performance at the 5th ZIZ Festival in 2023 and was recommended by the Zlata paličica expert platform for young audiences.

## Robotic puppetry system

The archived controller is intentionally simple: a two-axis analog joystick drives two hobby-servo channels. On each pass through the Arduino loop, the sketch:

1. reads the joystick's horizontal and vertical axes on `A0` and `A1`;
2. maps each 10-bit reading (`0–1023`) to a servo command (`0–180` degrees);
3. writes the resulting positions to the two servo objects; and
4. reports the raw readings and mapped angles over serial at `9600` baud.

This is a direct pan-and-tilt interface, not an autonomous robot. Timing and intention remain with the puppeteer; the electronics enlarge small hand movements into the movement of a stage object. The mechanism therefore sits between traditional puppet control and robotic actuation.

### Connections recorded in the sketches

| Function | [`ptservojoy.ino`](ptservojoy.ino) | [`ptservojoy2.ino`](ptservojoy2.ino) |
| --- | ---: | ---: |
| Joystick X (`VRX`) | `A0` | `A0` |
| Joystick Y (`VRY`) | `A1` | `A1` |
| X-axis servo signal | Digital pin `10` | Digital pin `5` |
| Y-axis servo signal | Digital pin `9` | Digital pin `6` |
| Pin assigned to `led` | Digital pin `5` | Digital pin `5` |
| Serial monitor | `9600` baud | `9600` baud |

Both versions include Arduino's standard [`Servo`](https://docs.arduino.cc/libraries/servo/) library. They also call `analogWrite(led, 255)` during every loop iteration.

> [!CAUTION]
> **Pin 5 conflict in `ptservojoy2.ino`:** digital pin `5` is assigned both to `SERVO_X_PIN` and to the variable `led`. The sketch consequently asks one physical output to carry servo-control pulses and an `analogWrite()` command. Those are not independent signals and may interfere, depending on the board and timer implementation. Treat this as an archival production sketch, verify the original hardware before reconstruction, and assign separate pins in any new adaptation. The working source is preserved unchanged here.

### Sketch variants

- [`ptservojoy.ino`](ptservojoy.ino) attaches the two servo objects to digital pins `10` and `9`. Its `led` output is on pin `5`, separate from both servo signals.
- [`ptservojoy2.ino`](ptservojoy2.ino) attaches the servo objects to pins `5` and `6`. In this variant, pin `5` is also assigned to `led`, producing the conflict documented above.

Neither sketch includes a dead zone, smoothing, calibration, movement easing, or mechanical travel limits. The repository does not include a schematic, bill of materials, Arduino board model, servo model, or power specification; this documentation therefore makes no assumptions about the original wiring beyond what the source code records.

### Reconstructing the controller

1. Open one `.ino` file in the Arduino IDE.
2. Confirm every signal assignment against the intended board and physical build.
3. Power the servos appropriately for their load; do not infer a power arrangement from the absence of a schematic.
4. Select the matching board and port, then compile and upload.
5. Open the serial monitor at `9600` baud to inspect joystick readings and commanded angles.
6. Test with linkages disconnected or safely constrained before allowing the full `0–180` command range.

## Movement as artistic research

In live puppetry, movement is more than an engineering output. A pause, tremor, overshoot, or sudden turn can become character, attention, or emotion. These sketches expose a small translation layer between the performer's hand and two mechanical axes, leaving expressive decisions with the operator.

That simplicity is artistically productive: the mechanism is legible, movement can be discovered through rehearsal, and wires, joints, electronics, and handmade objects can remain visible within the theatrical language. The code is best understood as a technical score embedded in a larger performance-making process.

## Artistic and production credits

| Role | Credit |
| --- | --- |
| Concept | Ariel Doron, Maša Radi Buh, Nika Bezeljak |
| Authors and performers | Miha Bezeljak, Uroš Kaurin, Gregor Prah |
| Director | Nika Bezeljak |
| Dramaturge | Maša Radi Buh |
| Visual design and technology | Monika Pocrnjić |
| Lighting and space design | Andrej Firm |
| Sound design | Gašper Torkar |
| Lighting design | Gašper Bohinec |
| Language editor | Metka Damjan |
| Executive production | Lana Bauman, Nika Bezeljak |
| Public relations | Anamarija Nađ (Moment), Špela Hren Juhart (Maribor Puppet Theatre) |
| Photography | Boštjan Lah |
| Co-production | Moment and Maribor Puppet Theatre |
| Support | Ministry of Culture of the Republic of Slovenia; Municipality of Maribor |

Credits have been checked against the official production records linked below.

## Documentation and press

- [Moment — official production page, gallery, credits, and trailer](https://moment.si/en/performance/is-it-over/)
- [Maribor Puppet Theatre — current production record](https://www.lg-mb.si/predstave/je-ze-konec/)
- [SiGledal — production archive](https://veza.sigledal.org/uprizoritev/je-ze-konec)
- [Zlata paličica — expert recommendation](https://www.zlatapalicica.si/predstava/je-ze-konec/)
- [“Don't Stop Me Now” — review by Petra Vidali, *Večer*](https://vecer.com/kultura/gledaliska-kritika-dont-stop-me-now-10322413)
- [“Konec sveta” — review by Tjaša Bertoncelj, SiGledal](https://veza.sigledal.org/kritika/konec-sveta-r)
- [Andrej Firm — lighting and space design project page](https://www.andrejfirm.com/is-it-over/)
- [Official trailer — Moment on Vimeo](https://vimeo.com/786279788)

See [Press and References](PRESS_AND_REFERENCES.md) for an annotated bibliography, educational material, festival records, and the image-rights note.

## Licensing

- Original project documentation, artistic descriptions, and README content
  owned by the repository author or used with permission are licensed under
  [Creative Commons Attribution 4.0 International](LICENSE-CC-BY-4.0.md)
  ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
- The Arduino source files [`ptservojoy.ino`](ptservojoy.ino) and
  [`ptservojoy2.ino`](ptservojoy2.ino) are licensed under the
  [MIT License](LICENSE-MIT). Their shared controller logic derives from an
  [ArduinoGetStarted.com example](https://arduinogetstarted.com/tutorials/arduino-joystick-servo-motor)
  expressly released into the public domain; the repository history records
  the production-specific versions as uploaded by Mon in 2023.
- Third-party materials, photographs, press articles, linked websites, and
  external media are excluded from these licences unless their rights holders
  explicitly grant permission.
- The linked production photograph `195A3900.jpg`, credited to Boštjan Lah,
  is **not** covered by either licence without appropriate authorisation from
  its rights holder.

These licences grant rights only to material the relevant licensor is
authorised to license. They do not alter copyright notices, credits, or terms
attached to third-party material.
