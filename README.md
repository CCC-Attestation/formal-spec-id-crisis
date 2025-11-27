# Identity Crisis

This repo contains the artifacts for formal specification and analysis of the following two candidates for standardization for attested TLS protocols:
- [Interoperable RA-TLS protocol](https://github.com/ccc-attestation/interoperable-ra-tls)
- TLS-attest protocol: [spec](https://datatracker.ietf.org/doc/draft-fossati-tls-attestation/09/) and [CCC project implementation](https://github.com/ccc-attestation/attested-tls-poc)

## Artifacts author
Muhammad Usama Sardar (contact: muhammad_usama.sardar at tu-dresden.de)

## Paper authors
Muhammad Usama Sardar, Mariam Moustafa, and Tuomas Aura

## Acknowledgments
Ionut Mihalcea contributed significantly to the discussions for the formalization. We also gratefully acknowledge insightful discussions with the following on this work:
- Jean-Marie Jacquet
- Thomas Fossati
- Eric Rescorla
- Hannes Tschofenig
- Yaron Sheffer
- Laurence Lundblade
- Giridhar Mandyam
- Christopher Patton
- Richard Barnes

Several others at the IETF and IRTF have contributed by providing feedback.

## Tool 
We use state-of-the-art symbolic security analysis tool [ProVerif](https://ieeexplore.ieee.org/document/9833653) for the specification of the protocols. 
### Installing ProVerif
Install the latest version (2.05 at the moment) of ProVerif: see https://bblanche.gitlabpages.inria.fr/proverif/ for details.
See Section 1.4 of [manual](https://bblanche.gitlabpages.inria.fr/proverif/manual.pdf) for installation options:
- via OPAM: Section 1.4.1
- from sources: Section 1.4.2
- from binaries: Section 1.4.3 

## Artifacts organization
- Folder `IRA-TLS` contains code for original Interoperable RA-TLS protocol.
- Folder `IRA-TLS/fix` contains code for our proposed fix for Interoperable RA-TLS protocol.
- Folder `TLS-a` contains code for original TLS-attest standard candidate.
- Folder `TLS-a/fix` contains code for our proposed fix for TLS-attest standard candidate.

The name of files within each folder are the same. So the following commands can be used to run any of those.

## Running automatic proofs 

### Basic Execution
Run as follows: 

```bash 
proverif -lib tls-lib-simple.pvl tls13-multiagent.pv
```

### Generation of traces for failing properties
In order to additionally generate a trace for each property which results in "false", create a subfolder (e.g., `traces` in the following command) for results before executing.

```bash 
mkdir traces
```

Then to execute: run as follows:
```bash 
proverif -lib tls-lib-simple.pvl -graph traces tls13-multiagent.pv
```

OR 
```bash 
proverif -lib tls-lib-simple.pvl -html traces tls13-multiagent.pv
```

Subfolder `traces` will contain the traces in .dot as well as .PDF.

### Saving log
To additionally save in log file together with display:
```bash
proverif -lib tls-lib-simple.pvl -html traces tls13-multiagent.pv 2>&1 | tee log.txt
```

### Horn clauses
To additionally see the Horn clauses generated in ProVerif: 

a. use command-line option `-test` as follows: 
```bash
proverif -lib tls-lib-simple.pvl tls13-multiagent.pv -test
```

OR 

b. add one of the following two settings inside the input (*.pv) file:

- `set verboseClauses = short.` to display the Horn clauses

- `set verboseClauses = explained.` to additionally display a sentence after each clause it generates to explain where this clause comes from.

### Interactive mode
To run in interactive mode:
```bash
proverif_interact -lib tls-lib-simple.pvl tls13-multiagent.pv
```


