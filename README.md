[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.nm000249-blue)](https://doi.org/10.82901/nemar.nm000249)

# BNCI 2022-001 EEG Correlates of Difficulty Level dataset

BNCI 2022-001 EEG Correlates of Difficulty Level dataset.

## Dataset Overview

- **Code**: BNCI2022-001
- **Paradigm**: imagery
- **DOI**: 10.1109/THMS.2020.3038339
- **Subjects**: 13
- **Sessions per subject**: 1
- **Events**: trajectory_start=1, waypoint_miss=16, waypoint_hit=48, trajectory_end=255
- **Trial interval**: [0, 90] s
- **Session IDs**: offline, online_session_2, online_session_3
- **File format**: gdf
- **Data preprocessed**: True

## Acquisition

- **Sampling rate**: 256.0 Hz
- **Number of channels**: 64
- **Channel types**: eeg=64, eog=3
- **Channel names**: AF3, AF4, AF7, AF8, AFz, C1, C2, C3, C4, C5, C6, CP1, CP2, CP3, CP4, CP5, CP6, CPz, Cz, EOG1, EOG2, EOG3, F1, F2, F3, F4, F5, F6, F7, F8, FC1, FC2, FC3, FC4, FC5, FC6, FCz, FT7, FT8, Fp1, Fp2, Fpz, Fz, Iz, O1, O2, Oz, P1, P10, P2, P3, P4, P5, P6, P7, P8, P9, PO3, PO4, PO7, PO8, POz, Pz, T7, T8, TP7, TP8
- **Montage**: 10-10
- **Hardware**: Biosemi ActiveTwo
- **Software**: EEGLAB
- **Reference**: car
- **Sensor type**: active
- **Line frequency**: 50.0 Hz
- **Auxiliary channels**: EOG (3 ch, horizontal, vertical), ppg

## Participants

- **Number of subjects**: 13
- **Health status**: patients
- **Clinical population**: normal or corrected-to-normal vision, no history of motor or neurological disease (one subject with history of vasovagal syncope)
- **Age**: mean=22.6, std=1.04
- **Gender distribution**: female=8, male=5
- **Handedness**: {'right': 12, 'left': 1}

## Experimental Protocol

- **Paradigm**: imagery
- **Number of classes**: 4
- **Class labels**: trajectory_start, waypoint_miss, waypoint_hit, trajectory_end
- **Trial duration**: 90.0 s
- **Study design**: Subjects piloted a simulated drone through circular waypoints using a flight joystick, controlling roll and pitch while the drone maintained constant velocity. In offline session: 32 trajectories each with constant difficulty level (v-shape design from level 16 to 1 and back to 16), each trajectory had 32 waypoints and lasted ~90 seconds. In online sessions: each condition consisted of 12 trajectories with 33 waypoints and 8 decision points per trajectory.
- **Feedback type**: visual
- **Stimulus type**: visual
- **Stimulus modalities**: visual
- **Primary modality**: visual
- **Synchronicity**: cue-based
- **Mode**: both
- **Instructions**: Subjects piloted a simulated drone through a series of circular waypoints. Subjects controlled the roll and pitch while the drone had a constant velocity of 11.8 arbitrary units per second when flying straight. They were instructed to press a button when the current level was easy as a way to collect ground truth for decoding or to proceed with self-paced learning.
- **Stimulus presentation**: screen_size=twenty-inch screen, screen_resolution=1680x1050, input_device=Logitech Extreme 3D Pro joystick, waypoint_colors=green (current), blue (next), yellow (decision point), waypoint_distance_pitch=32 A.U. (at least 2.7 seconds), waypoint_distance_roll=24 A.U. (at least 2.0 seconds)

## HED Event Annotations

Schema: HED 8.4.0 | Browse: https://www.hedtags.org/hed-schema-browser

```
  trajectory_start
    ├─ Experiment-structure
    └─ Label/trajectory_start

  waypoint_miss
    ├─ Experiment-structure
    └─ Label/waypoint_miss

  waypoint_hit
    ├─ Experiment-structure
    └─ Label/waypoint_hit

  trajectory_end
    ├─ Experiment-structure
    └─ Label/trajectory_end

```
## Paradigm-Specific Parameters

- **Detected paradigm**: motor_imagery
- **Imagery tasks**: right_hand, left_hand, feet

## Data Structure

- **Trials**: {'offline_session': '32 trajectories of 32 waypoints each (~90 seconds per trajectory)', 'online_session_per_condition': '12 trajectories of 33 waypoints each with 8 decision points'}
- **Blocks per session**: 2
- **Trials context**: Offline session: v-shape difficulty design (level 16→1→16). Online sessions: each condition had 12 trajectories, starting at level 1 for 1st trajectory, then 4 levels lower than final level of previous trajectory. Average 10.3 seconds per decision group (4 waypoints).

## Preprocessing

- **Data state**: preprocessed
- **Preprocessing applied**: True
- **Steps**: downsampling from 2048 Hz to 256 Hz, casual bandpass filtering between 1 and 40 Hz, SPHARA 20th order spatial low-pass filter for interpolation and artifact reduction, common-average re-referencing, ICA for EOG artifact removal, peripheral electrodes removed (25 central channels kept), artifact rejection: windows with peak value > 50 µV rejected
- **Highpass filter**: 1.0 Hz
- **Lowpass filter**: 40.0 Hz
- **Bandpass filter**: [1.0, 40.0]
- **Filter type**: Butterworth
- **Filter order**: 14
- **Artifact methods**: ICA, SPHARA, amplitude thresholding
- **Re-reference**: car
- **Downsampled to**: 256.0 Hz
- **Notes**: Out of 39 recordings, P2 was removed twice from offline or online sessions due to short-circuit with the CMS or DRL electrode. On average, 15.8 ICA components were returned and 1.07 components were removed during construction of online decoders (correlation > 0.7 with EOG).

## Signal Processing

- **Classifiers**: LDA, Generalized Linear Model with elastic net regularization
- **Feature extraction**: PSD, ICA, log-PSD
- **Frequency bands**: analyzed=[2.0, 28.0] Hz; theta=[4.0, 8.0] Hz; alpha=[10.5, 13.0] Hz
- **Spatial filters**: SPHARA, common-average reference

## Cross-Validation

- **Method**: leave-one-pair-out cross-validation (4x or 64x depending on class balance)
- **Folds**: 4
- **Evaluation type**: within_subject, cross_session

## Performance (Original Study)

- **Accuracy**: 76.7%
- **Offline Validation Accuracy Mean**: 76.7
- **Offline Validation Accuracy Std**: 5.1
- **Online Session 2 Accuracy Mean**: 56.2
- **Online Session 2 Accuracy Std**: 8.6
- **Online Session 3 Accuracy Mean**: 54.7
- **Online Session 3 Accuracy Std**: 11.0
- **Online Above Chance Recordings**: 16 out of 26 (~62%)

## BCI Application

- **Applications**: drone control, adaptive learning, difficulty regulation, visuomotor learning
- **Environment**: indoor laboratory
- **Online feedback**: True

## Tags

- **Pathology**: Healthy
- **Modality**: EEG
- **Type**: Experimental/Research

## Documentation

- **DOI**: 10.1109/TAFFC.2021.3059688
- **Associated paper DOI**: 10.1109/THMS.2020.3038339
- **License**: CC-BY-4.0
- **Investigators**: Ping-Keng Jao, Ricardo Chavarriaga, Jose del R. Millan
- **Senior author**: Jose del R. Millan
- **Contact**: ping-keng.jao@alumni.epfl.ch; ricardo.chavarriaga@zhaw.ch; jose.millan@austin.utexas.edu
- **Institution**: Ecole Polytechnique Federale de Lausanne
- **Address**: 1015 Geneva, Switzerland
- **Country**: Switzerland
- **Repository**: BNCI Horizon
- **Publication year**: 2021
- **Funding**: Swiss National Centres of Competence in Research (NCCR) Robotics
- **Acknowledgements**: The authors would like to thank Alexander Cherpillod for his help in the implementation of the simulator and Ruslan Aydarkhanov for his suggestions in designing the protocol. Some figures were drawn with the Gramm MATLAB toolbox.
- **Keywords**: EEG, real-time decoding of difficulty, closed-loop adaptation, (simulated) flying, workload, challenge point, brain-machine interface

## Abstract

Adaptively increasing the difficulty level in learning was shown to be beneficial than increasing the level after some fixed time intervals. To efficiently adapt the level, we aimed at decoding the subjective difficulty level based on Electroencephalography (EEG) signals. We designed a visuomotor learning task that one needed to pilot a simulated drone through a series of waypoints of different sizes, to investigate the effectiveness of the EEG decoder. The EEG decoder was compared with another condition that the subjects decided when to increase the difficulty level. We examined the decoding performance together with behavioral outcomes. The online accuracies were higher than the chance level for 16 out of 26 cases, and the behavioral results, such as task scores, skill curves, and learning patterns, of EEG condition were similar to the condition based on manual regulation of difficulty.

## Methodology

The study compared two conditions for difficulty regulation during a simulated drone piloting task: (1) EEG-based automatic difficulty adjustment using real-time decoding of perceived difficulty, and (2) Manual self-paced adjustment where subjects pressed a button when they found the level easy. Each subject participated in one offline session (for building subject-specific decoders) and two online sessions (each containing both EEG and Manual conditions in counterbalanced order). The task involved piloting a drone through circular waypoints with 16 difficulty levels defined by waypoint radius. Features were extracted using Thomson's multitaper algorithm with 2-second sliding windows, and classification used generalized linear models with elastic net regularization followed by LDA. The study evaluated both decoding accuracy and behavioral outcomes (task scores, skill curves, learning patterns).

## References

Jao, P.-K., Chavarriaga, R., & Millan, J. d. R. (2021). EEG Correlates of Difficulty Levels in Dynamical Transitions of Simulated Flying and Mapping Tasks. IEEE Transactions on Human-Machine Systems, 51(2), 99-108. https://doi.org/10.1109/THMS.2020.3038339

Notes

.. versionadded:: 1.3.0

This dataset is designed for cognitive workload assessment and difficulty level detection. Unlike motor imagery datasets, the task involves actual motor control while the cognitive state (perceived difficulty) varies.

The public release contains only the first session (offline) data. Additional behavioral data and online sessions with closed-loop difficulty adaptation are not included. The paradigm "imagery" is used for compatibility, though the actual task involves motor execution with cognitive load variations.

See Also

BNCI2015_004 : Multi-class mental task dataset with imagery and cognitive tasks BNCI2014_001 : 4-class motor imagery dataset

Examples

>>> from moabb.datasets import BNCI2022_001 >>> dataset = BNCI2022_001() >>> dataset.subject_list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
Appelhoff, S., Sanderson, M., Brooks, T., Vliet, M., Quentin, R., Holdgraf, C., Chaumon, M., Mikulan, E., Tavabi, K., Hochenberger, R., Welke, D., Brunner, C., Rockhill, A., Larson, E., Gramfort, A. and Jas, M. (2019). MNE-BIDS: Organizing electrophysiological data into the BIDS format and facilitating their analysis. Journal of Open Source Software 4: (1896). https://doi.org/10.21105/joss.01896

Pernet, C. R., Appelhoff, S., Gorgolewski, K. J., Flandin, G., Phillips, C., Delorme, A., Oostenveld, R. (2019). EEG-BIDS, an extension to the brain imaging data structure for electroencephalography. Scientific Data, 6, 103. https://doi.org/10.1038/s41597-019-0104-8

---
Generated by MOABB 1.5.0 (Mother of All BCI Benchmarks)
https://github.com/NeuroTechX/moabb
