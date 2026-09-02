# Bringing DELPHI data into the EDM4hep ecosystem

This organization connects the DELPHI experiment's legacy data formats to a
modern, reproducible HEP analysis stack. Its two public repositories cover
different parts of this work. One produces fully simulated DELPHI events with
modern generators. The other converts reconstructed DELPHI events to EDM4hep.

```text
modern event generators
          │
          ▼
      HepMC3 / LUJETS
          │
          ▼
   DELSIM + DELANA ────── preserved DELPHI data
          │                         │
          └──────────┬──────────────┘
                     ▼
              shortDST + fullDST
                     │
                     ▼
                   EDM4hep
```

## DELPHI simulation pipeline

[**delphi-sim-pipeline**](https://github.com/delphi-fullDST-edm4hep/delphi-sim-pipeline)
connects modern event generators to the original DELPHI detector simulation and
reconstruction chain. Its generator-independent `hepmc2fadgen` converter changes
HepMC3 event records into the Fortran-unformatted LUJETS input that DELSIM
expects. DELSIM and DELANA then produce the standard DELPHI shortDST and fullDST
outputs.

The repository supports Pythia 8, Sherpa, Herwig 7, Whizard, external HepMC3
input, and legacy-generator paths. It also includes container and HTCondor tools,
event-record checks, reproducible seeding rules, and a controlled 1994/94C2
validation path. A clear environment boundary keeps the modern Key4hep generator
stack separate from the legacy DELPHI runtime. The `fort.26` event record is the
only artifact passed between them.

**Use it when:** you want to generate new Monte Carlo events, process them with
the DELPHI detector simulation and reconstruction, or compare generator models
with a controlled detector setup.

## DELPHI to EDM4hep converter

[**delphi-edm4hep**](https://github.com/delphi-fullDST-edm4hep/delphi-edm4hep)
converts DELPHI ZEBRA reconstruction data into podio/EDM4hep files. Its two-pass
C++ pipeline first converts shortDST content into `sDST_*` collections. It then
matches the corresponding fullDST events and adds detailed `fDST_*` collections.
The result keeps both the compact reconstructed event view and the extra tracking
and detector information found only in fullDST.

The conversion includes reconstructed particles, track states and covariance,
vertices and beamspot information, calorimeter content, particle identification,
generator truth, and reco-to-truth links. Dedicated tools support beamspot
extraction and AABTAG flavour-tag validation or recalculation. The repository
also includes data-reconstruction drivers, schema documentation, CI across
Key4hep release channels, and alignment and content checks for converted files.

**Use it when:** you have matching DELPHI shortDST/fullDST data or simulation
and want an analysis-ready EDM4hep representation with documented collection
meanings and units.

[Read the converter documentation](https://delphi-fulldst-edm4hep.github.io/delphi-edm4hep/)
or visit either repository for its build, production and validation guides.

## Get involved

Start with the README and documentation in each repository. You can submit bug
reports, focused feature requests, documentation improvements, and reproducible
validation results through GitHub issues and pull requests. Please read our
[contribution guide](https://github.com/delphi-fullDST-edm4hep/.github/blob/main/CONTRIBUTING.md)
before opening a pull request.

> [!NOTE]
> Each repository documents its own licensing. Do not assume that code or legacy
> DELPHI material without an explicit licence can be reused without limits.
