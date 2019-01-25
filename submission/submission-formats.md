# Initial proposal for the submission of LDC results

Michele, 3/24/2018

## Submission forum

If the participants are willing to share their code, I suggest they post it on github.com (or on our gitlab if they are consortium members). As for results (estimates, chains, technical notes), these can go on figshare.com, which can host up-to-5GB entries including an abstract and a heterogeneous fileset. figshare is free for public repos, and it provides a DOI. I would suggest one figshare entry per participating researcher/group. We'll suggest a naming scheme to identify datasets within a challenge.

## How to submit point estimates, plus errors

Use a simple format motivated by the LDC internal text format and using LDC standard units and parameter definitions. This can be YAML: 

    author:                 Michele
    e-mail:                 vallis@vallis.org
    date:                   2018/03/20

    challenge:              LDC1
    dataset:                LDC1-1-MBHB

    estimates:
        - SourceType:             MBHB
          Approximant:            IMRPhenomD
          ObservationDuration:    7864320.0
          Cadence:                10.0
          Mass1:                  1869759.731
          Mass2:                  565846.141
          Distance:               42.98096306767939
          InitialPolarAngleL:     1.9528
          InitialAzimuthalAngleL: 1.1555959752434493
          AzimuthalAngleOfSpin1:  5.840950175706398
          AzimuthalAngleOfSpin2:  1.9878462360990703
          Spin1:                  0.7764685576250351
          Spin2:                  0.9532320445857974
          PolarAngleOfSpin1:      0.0
          PolarAngleOfSpin2:      0.0
          PhaseAtCoalescence:     1.2852901366370226
          CoalescenceTime:        6951400.0
          EclipticLongitude:      4.5844
          EclipticLatitude:       0.8967163267948965
          Redshift:               4.5699
        - SourceType:             MBHB
          Approximant:            IMRPhenomD
          ...

This format could allow for the specification of normal errors, e.g.,

          Mass1:                  1869759.731 +/- 4.31

    or asymmetric, suitable also for a confidence range

          Mass1:                  1869759.731 + 4.31 - 2.34

JSON is also possible:

    {
        author:    'Michele',
        e-mail:    'vallis@vallis.org',
        date:      '2018/03/20',
        challenge: 'LDC1',
        datasets:  'LDC1-1-MBHB',
        sources:   [{
                        SourceType:  'MBHB',
                        Approximant: 'IMRPhenomD',
                        Mass1:       '1869759.731 +/- 4.31',
                        ...
                    },
                    {
                        SourceType:  'MBHB',
                        ...
                    },
                    ...]
    }

For both we can provide simple code to write files from various languages.

## How to submit posteriors

For these, I would suggest simple CSV/TSV tables, one for each source, e.g.,

    Mass1,Mass2,Distance,InitialPolarAngleL,InitialAzimuthalAngleL,[...]
    1869759.731,565846.141,42.98096306767939,1.9528,1.1555959752434493,[...]
    [...]

Although these are ASCII files, they compare well to binaries once gzipped.
We should ask for ~10,000 quasi-independent samples. 
The tables should probably be accompanied by a YAML/JSON with provenance 

    author:     Michele
    e-mail:     vallis@vallis.org
    date:       2018/03/20

    challenge:  LDC1
    dataset:    LDC1-1-MBHB

    posteriors: - ldc1-1-mbhb-1.csv
                - ldc1-1-mbhb-2.csv
                - ldc1-1-mbhb-3.csv
                [...]

