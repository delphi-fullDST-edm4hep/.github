# Bringing DELPHI data into the EDM4hep ecosystem

This organization connects the DELPHI experiment's legacy data formats to a
modern, reproducible HEP analysis stack. Its three public repositories cover
different parts of this work. One produces fully simulated DELPHI events with
modern generators. One converts reconstructed DELPHI events to EDM4hep. The
third draws those events, in a browser.

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
                     │
                     ▼
              event display
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
or visit the repository for its build, production and validation guides.

## DELPHI event display

[**delphi-edm4hep-eventdisplay**](https://github.com/delphi-fullDST-edm4hep/delphi-edm4hep-eventdisplay)
draws a single DELPHI event straight from an EDM4hep file, with no DELGRA, no
X11 and no ROOT. It reads the file with uproot and discovers the collections
from podio metadata rather than assuming their names, so each part of the
picture can be drawn from whichever `Track`, `Vertex`, `Cluster`, hit or
`ParticleID` collection you choose.

It draws four panels — the r-φ and r-z views of the whole event, the vertex
detector with its layers and hits, and the RICH Cherenkov angle against
momentum with the expected π/K/p curves — or a three-dimensional detector
scene. Only measured quantities are drawn: tracks are helices from their own
perigee parameters, started at the vertex they belong to, with the
back-extrapolation to the interaction point dotted so the picture never claims
a path the particle did not travel.

The display runs in the browser. Drop an EDM4hep file onto the page and uproot
reads it locally under Pyodide; nothing is uploaded and no server is involved.
Beside the figure, every collection in the event is listed with its type,
domain, provenance, relations and per-event object count — the same vocabulary
as the converter's collection map — and selecting one dims everything in the
figure drawn from anywhere else.

**Use it when:** you want to look at a single converted event, see what a
collection actually holds for that event, or produce a figure for a talk.

[Open the event display](https://delphi-fulldst-edm4hep.github.io/delphi-edm4hep-eventdisplay/)
or [read its documentation](https://delphi-fulldst-edm4hep.github.io/delphi-edm4hep-eventdisplay/manual/).

## Get involved

Start with the README and documentation in each repository. You can submit bug
reports, focused feature requests, documentation improvements, and reproducible
validation results through GitHub issues and pull requests. Please read our
[contribution guide](https://github.com/delphi-fullDST-edm4hep/.github/blob/main/CONTRIBUTING.md)
before opening a pull request.

> [!NOTE]
> Each repository documents its own licensing. Do not assume that code or legacy
> DELPHI material without an explicit licence can be reused without limits.
