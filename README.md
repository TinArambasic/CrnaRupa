# Crna rupa u Blenderu

3D vizualizacija crne rupe izrađena u **Blenderu**, korištenjem shader node sustava i **Cycles** render enginea. Projekt je nastao kao rekreacija crne rupe *Gargantua* iz filma *Interstellar* (2014.), uz pojednostavljene fizikalne efekte radi brže izrade i renderiranja.

> Seminarski rad — Fakultet primijenjene matematike i informatike, Sveučilište J. J. Strossmayera u Osijeku, 2026.

![status](https://img.shields.io/badge/status-completed-brightgreen) ![Blender](https://img.shields.io/badge/Blender-Cycles-orange) ![license](https://img.shields.io/badge/license-MIT-blue)

## Sadržaj

- [O projektu](#o-projektu)
- [Kako to izgleda](#kako-to-izgleda)
- [Korištene tehnike](#korištene-tehnike)
- [Struktura scene](#struktura-scene)
- [Preduvjeti](#preduvjeti)
- [Pokretanje](#pokretanje)
- [Renderiranje](#renderiranje)
- [Struktura repozitorija](#struktura-repozitorija)
- [Reference](#reference)
- [Napomena o korištenju AI alata](#napomena-o-korištenju-ai-alata)
- [Licenca](#licenca)

## O projektu

Cilj projekta je izraditi vizualno vjeran 3D model crne rupe koji simulira ključne fizikalne pojave:

- **horizont događaja** — granicu iza koje ništa, pa ni svjetlost, ne može pobjeći,
- **akrecijski disk** — vrući plin i prašinu koji kruže oko crne rupe i emitiraju snažno zračenje,
- **gravitacijsko lećenje** — savijanje svjetlosti oko crne rupe zbog kojeg disk izgleda kao da omotava jezgru odozgo i odozdo.

Umjesto post-produkcijskih trikova, savijanje svjetlosti ostvareno je **stvarnom optičkom refrakcijom** kroz Glass BSDF shader, na način na koji staklena kugla izobličuje sve iza sebe.

## Kako to izgleda

Video renderirane animacije nalazi se u korijenu repozitorija: 0001-0180.mkv
Video demonstracija je dostupna na linku https://www.youtube.com/watch?v=VOWv3d9-U8Q

## Korištene tehnike

| Element | Pristup |
|---|---|
| Jezgra (horizont događaja) | Emission node, crna boja, Strength 1000 — potpuno neosvijetljena sfera |
| Beauty ring | Emission node, narančasta boja, Strength 10 000 |
| Akrecijski disk | Slikovna tekstura + HSV korekcije + RGB Curves + maska preko Color Rampa i Mix Shadera |
| Gravitacijsko lećenje | Glass BSDF + Transparent BSDF, kombinirano preko Mix Shadera i Layer Weight node-a |
| Pozadina | HDRI (.exr) fotografija Mliječne staze — Environment Texture → Emission |
| Animacija | Driver izraz `#frame/10` na Z rotaciji, bez keyframeova |
| Render engine | Cycles (ray/path tracing), 1080p, 30 fps |

## Struktura scene

Scena je organizirana kroz tri glavna materijala, svaki primijenjen na zaseban objekt:

1. **Kružnica** — jezgra crne rupe + beauty ring
2. **Akrecijski disk**
3. **Gravitacija** — sfera s refrakcijskim shaderom koja simulira lećenje

## Preduvjeti

- [Blender](https://www.blender.org/download/) 3.x ili noviji
- GPU s podrškom za Cycles (preporučeno, radi brzine renderiranja)

## Pokretanje

```bash
git clone https://github.com/TinArambasic/CrnaRupa.git
cd CrnaRupa
```

Otvori `.blend` datoteku direktno u Blenderu:

```bash
blender crna_rupa.blend
```

## Renderiranje

Render engine je postavljen na **Cycles**. Za render animacije:

`Render → Render Animation` (`Ctrl+F12`)

Prosječno vrijeme renderiranja u ovom projektu iznosilo je ~5–6 min po frameu (ukupno ~8h za video od 3 sekunde, 1080p/30fps).

## Struktura repozitorija

```
.
├── crna_rupa.blend        # glavna Blender datoteka
├── 0001-0180.mkv          # gotovi render outputi
├── Seminarski-Rad-Tin_Arambasic          # seminarski rad i proces pravljenja 3d modela
└── README.md
```

## Reference

1. Luminet, J.-P. (1979). *Image of a spherical black hole with thin accretion disk.* Astronomy and Astrophysics.
2. James, O., von Tunzelmann, E., Franklin, P., Thorne, K. S. (2015). *Gravitational lensing by spinning black holes in astrophysics, and in the movie Interstellar.* Classical and Quantum Gravity.
3. Hubelbauer, T. — [blender-gargantua](https://github.com/TomasHubelbauer/blender-gargantua)
4. Maisuradze, N. — Behind the scenes: Gargantua black hole tutorial (BlenderNation / Blender Artists forum)
5. [Freepik](https://www.freepik.com) — Milky Way HDRI fotografija
6. [Blender Manual](https://docs.blender.org) — Cycles Render Engine, Shader Nodes, World Properties, Glass BSDF

## Napomena o korištenju AI alata

Autor je koristio Claude (Anthropic) kao pomoć pri pisanju popratnog seminarskog rada — za pojašnjenje teorije crne rupe i pomoć pri preprekama u 3D modeliranju. Nijedan generirani sadržaj činjenične prirode ili vezan uz temu rada nije predstavljen kao izvorno autorovo djelo.

## Licenca

Ovaj projekt je dostupan pod [MIT licencom](LICENSE) (po želji promijeni prema stvarnoj licenci repozitorija).


