# L-MSP Measured Transition-Pair Dataset

This supplementary dataset is constructed from continuous real-robot execution logs collected on the L-MSP benchtop continuum-robot platform.

## Dataset Type

The dataset contains measured real-world command-conditioned transition pairs. These pairs are not simulation-generated.

## Pair Definition

Each pair is formed from two valid samples within the same executed command segment (`PointID`). The before sample is denoted `t`, and the after sample is denoted `t+1`.

The pair row contains:
- nominal structured instruction and planner reference;
- measured ground-truth displacement description from `Act_5`, `Act_6`, and `Act_7`;
- measured state vector before and after the transition (`S_t_*`, `S_t1_*`);
- measured 48-channel magnetic map before and after the transition (`M_t_*`, `M_t1_*`).

## Ground-Truth Annotation

The movement description is computed from measured before/after states:
- `GT_dX_tip_mm = Act_5(t+1) - Act_5(t)`
- `GT_dY_tip_mm = Act_6(t+1) - Act_6(t)`
- `GT_dZ_tip_mm = Act_7(t+1) - Act_7(t)`
- `GT_step_3D_mm = sqrt(dx^2 + dy^2 + dz^2)`

The `Instruction_nominal` and `Plan_*` columns describe the nominal command/reference issued by the planner/controller. They should not be treated as measured ground-truth displacement labels.

## Important Note

The dataset does not impose a fixed 2 mm displacement. The selected pairs cover measured 3D displacement bins from approximately 0.5 mm to 8 mm. Differences between nominal commands and measured transitions are expected because tendon friction, mechanical hysteresis, and closed-loop tracking error are naturally included in real-robot execution.

## Workbook Sheets

- `README`: short overview and recommended wording.
- `Column_Description`: explanation of each column group.
- `Pair_Stats`: summary statistics for the selected 10,000 pairs.
- `Pair_Dataset_10000`: one row per measured transition pair, including pair annotation, before/after states, and before/after magnetic maps.
