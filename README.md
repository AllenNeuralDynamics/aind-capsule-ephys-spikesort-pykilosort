# Spike sort with pyKilosort for AIND ephys pipeline
## aind-capsule-ephys-spikesort-pykilosort


### Description

This capsule is designed to spike sort ephys data using [pyKilosort](https://github.com/int-brain-lab/pykilosort) for the AIND pipeline.

This capsule spike sorts preprocessed ephys stream and applies a minimal curation to:

- remove empty units
- remove excess spikes (falling beyond the end of the recording)

**NOTE**: the capsule runs `pyKilosort==1.4.3`, with a slight modification to get rid of some print statements (see [PR](https://github.com/int-brain-lab/pykilosort/pull/16)).


### Inputs

The `data/` folder must include the output of the [aind-capsule-ephys-preprocessing](https://github.com/AllenNeuralDynamics/aind-capsule-ephys-preprocessing), containing 
the `data/preprocessed_{recording_name}` folder.

### Parameters

The `code/run` script takes 4 arguments:

- `preprocessing_strategy`: `cmr` (default) | `destripe`. The preprocessing strategy to use. `cmr` is the common median reference, `destripe` is the high-pass spatial filtering.
- `debug`: `false` (default) | `true`. If `true`, the capsule will run in debug mode, processing only a small subset of the data.
- `debug_duration_s`: `60` (default). The duration of the debug subset, in seconds.
- `drift`: `estimate` (default) | `apply` | `skip`. The drift correction strategy to use. `estimate` will estimate the drift and save it to the output folder. `apply` will estimate the drift and interpolate the traces using the estimated motion. `skip` will skip the drift correction.

A full list of parameters can be found at the top of the `code/run_capsule.py` script and is reported here:

```python
preprocessing_params = dict(
        preprocessing_strategy="cmr", # 'destripe' or 'cmr'
        highpass_filter=dict(freq_min=300.0,
                             margin_ms=5.0),
        phase_shift=dict(margin_ms=100.),
        detect_bad_channels=dict(method="coherence+psd",
                                 dead_channel_threshold=-0.5,
                                 noisy_channel_threshold=1.,
                                 outside_channel_threshold=-0.3,
                                 n_neighbors=11,
                                 seed=0),
        remove_out_channels=True,
        remove_bad_channels=True,
        max_bad_channel_fraction_to_remove=0.5,
        common_reference=dict(reference='global',
                              operator='median'),
        highpass_spatial_filter=dict(n_channel_pad=60,
                                     n_channel_taper=None,
                                     direction="y",
                                     apply_agc=True,
                                     agc_window_length_s=0.01,
                                     highpass_butter_order=3,
                                     highpass_butter_wn=0.01),
        motion_correction=dict(compute=True,
                               apply=False,
                               preset="nonrigid_accurate",)
    )
```

### Output

The output of this capsule is the following:

- `results/spikesorted_{recording_name}` folder, containing the spike sorted data saved by SpikeInterface and the spike sorting log
- `results/data_procress_spikesorting_{recording_name}.json` file, a JSON file containing a `DataProcess` object from the [aind-data-schema](https://aind-data-schema.readthedocs.io/en/stable/) package.

