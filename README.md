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

### `TTbar_14TeV_TuneCP5_2025.h5`

GenHDF5 input for relval 16834.86 (`GeneratorInterface/GenHDF5Interface`,
`customise.simFromHDF5RelVal`), written by https://gitlab.cern.ch/tvami/genhdf5.

* 100 events, the GEN of workflow 16834.0 (`TTbar_14TeV_TuneCP5_cfi`, relval
  seeds, single thread), `auto:phase1_2025_realistic`, beamspot `DBrealistic`,
  CMSSW_20_1_X_2026-09-30-2300
* P2 precision, 633 kB: `/sim` (with the pre-decayed chains of displaced decays,
  `/sim/status`, `/sim/endVtxIdx`), `/event`, and the `/truth` tier (MiniAOD-pruned
  genParticles with status flags and mothers), file attributes `beamspot=applied`,
  `final_state=all`
