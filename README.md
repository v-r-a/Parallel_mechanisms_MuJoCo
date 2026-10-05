# A collection of XML models of parallel mechanisms in MuJoCo

This is envisioned to be a resource of curated parallel mechanisms for MuJoCo, supporting the study of their kinematics, dynamics, and control. **Contributions of models, improvements, and examples are welcome!** Submit contributions through a pull request with a short description of the change and the checks performed. For substantial additions, opening an issue first is encouraged.

There are already a huge number of URDF files of parallel mechanisms on the internet. Adapting them to MuJoCo's format via [simulate](https://mujoco.readthedocs.io/en/latest/programming/samples.html#sasimulate) utility is pretty easy. One could define [constaints](https://mujoco.readthedocs.io/en/latest/XMLreference.html#equality) from that point. 

Contributors may follow model organization and documentation conventions similar to [MuJoCo Menagerie](https://github.com/google-deepmind/mujoco_menagerie). Someday, we could merge this repository in to MuJoCo Menagerie!

MuJoCo's [soft constraint model](https://mujoco.readthedocs.io/en/latest/computation/index.html#constraint-model) may not be the best to analyse parallel mechanisms at the moment, but could be useful some day. 

## Mechanisms

| Manipulator | Basic model | Refined model |
| --- | :---: | :---: |
| Planar_4bar | — | — |
| Planar_5bar | ✓ | — |
| Planar_3RRR | — | — |
| 3RPS | — | — |
| 3RRR | — | — |
| 6SPU | — | — |
| 6RSS | — | — |
| Spherical_3RRR | — | — |

✓ = available; — = not yet available.

## Model categories

- **Basic model:** A minimal, runnable model using simple geometric shapes, with the intended joint topology, actuation, and loop-closure constraints. Assumed dimensions and physical parameters should be documented.
- **Refined model:** A model with better-supported geometry and physical parameters, documented actuator properties, and validation results. Detailed visual meshes alone do not establish dynamic accuracy.

The table records model availability, not independent certification of accuracy. Each model's README should describe its validation status and limitations.

## Recommended model organization

Keep each mechanism in its corresponding directory. When both categories are provided, use `basic/` and `refined/` subdirectories, each following the layout below.

| File or directory | Purpose |
| --- | --- |
| `model.xml` | Mechanism definition, including joints, inertial properties, actuators, and loop-closure constraints. |
| `scene.xml` | Includes `model.xml` and adds the floor, lighting, camera, and other scene elements. |
| `README.md` | Model description, parameter sources, usage instructions, and limitations. |
| `preview.png` | Image of the mechanism; joint labels are encouraged. |
| `assets/` | Optional meshes and textures. |
| `LICENSE` | Model-specific licensing terms where applicable; preserve licenses for third-party assets. |

Keep the mechanism reusable by placing environmental objects in `scene.xml`.

## Modeling and contribution guidelines

Contributions of new mechanisms, corrections, refined models, and documentation are welcome. Please follow these guidelines:

1. **Describe the mechanism.** State its topology, mechanism DOF, actuated and passive joints, dimensions, joint limits, and coordinate conventions.
2. **Explain loop closure.** Identify where the kinematic tree is cut and which equality constraints close each loop. Document the intended assembly mode.
3. **Provide a valid starting configuration.** Include a usable initial pose and, where appropriate, a named keyframe.
4. **Document physical assumptions.** Use SI units wherever possible and identify the sources of masses, inertias, geometry, and actuator parameters. Clearly label assumed values and any damping or armature introduced for numerical stability.
5. **Keep XML readable.** Use descriptive names, two-space indentation, default classes for repeated properties, and relative asset paths. Separate visual and collision geometry where useful.
6. **Check behavior before contributing.** Verify that the scene loads and runs without numerical warnings. Exercise a representative motion and report loop-closure error, timestep, solver settings, and any observed limitations.
7. **Make results reproducible.** Include the commands or scripts needed to reproduce the demonstration or validation, together with the tested MuJoCo version. Add a preview image when possible.
8. **Credit sources.** Cite relevant papers, CAD sources, and original authors. Preserve third-party license notices and document any model-specific licensing terms.

