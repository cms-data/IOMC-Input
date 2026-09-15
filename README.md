# IOMC-Input
Data files for IOMC/Input

## Files

### `TTbar_13TeV_TuneCUETP8M1_HepMC3.hepmc3`

HepMC3 `Asciiv3` input for the `MCFileSource3` unit test
(`IOMC/Input/test/testReader3_cfg.py`).

* 50 events, inclusive `t{\bar t}` at 13 TeV
* `Configuration/Generator/python/TTbar_13TeV_TuneCUETP8M1_cfi.py`,
  generated with `Pythia8HepMC3GeneratorFilter` so the record is native
  HepMC3 rather than converted from HepMC2
* beamspot `Realistic25ns13TeVEarly2018Collision`, conditions
  `auto:phase1_2018_realistic` (150X_mc2018_realistic_v1), CMSSW_20_1_0_pre3
* ~1500 particles and ~870 vertices per event, 13 MB

Produced after cms-sw/cmssw#51857. Before that fix,
`HepMC3Product::applyVtxGen` appended to an un-cleared `GenEventData`, so every
vertex-smeared HepMC3 record was stored twice with the duplicates unlinked. A
file made from an unpatched release has exactly twice the particles of its
`generator:unsmeared` counterpart and roughly half of them carrying no
production vertex; this one has the same counts as the unsmeared record and two
beam particles per event, as it should.
