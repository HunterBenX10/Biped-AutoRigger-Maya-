# Biped Rig Builder

A Maya auto-rigger for biped game characters. Place guides on any mesh and get a
game-ready skeleton with UE5 joint names, automatic skinning, corrective joints and a full
IK/FK control rig, in a few clicks.

Made by Ben. Pre-rigged character: [Gumroad](https://9842329043591.gumroad.com/l/lmwzr)

<!-- add a screenshot / GIF here: ![Biped Rig Builder](docs/preview.gif) -->

## Features

**Guides and skeleton**
- Fit to Mesh places the guides on any proportions; they can be adjusted, mirrored and
  started in A-pose or T-pose
- Skeleton uses Unreal Engine 5 mannequin names and orientation, ready to export
- Twist joints on the arms and legs

**Skinning**
- One click skins the body with an adaptive weight solve, on any mesh
- Clothes, shoes and hair get their weights from the body
- Stray vertices in extreme poses are found and repaired automatically
- Legs and pelvis use dual quaternion blending to keep their volume
- Non-manifold meshes fall back to a safe bind instead of crashing Maya

**Correctives**
- Joints for chest, elbow, wrist, hip, knee, ankle, waist and back
- Added after skinning, one at a time, with **Show Weights** to see what each one moves
- Edited live with sliders in the UI
- Automatic corrective and breathing blendshapes

**Control rig**
- IK/FK arms, legs and spine with switch controls
- Stretchy IK limbs and a spline-IK spine
- Reverse foot: heel, toe, ball, toe tap and bank
- Space switching for head, hands, arms and pole vectors
- Finger curl, fist and spread attributes; breathing on the chest controls
- Global scale; Remove Rig keeps the skin so you can repaint and rebuild

## Install

1. Download or clone the repo.
2. Drag `drag_drop_install.py` into the Maya viewport.
3. A **BipedRig** button appears on your current shelf and the tool opens. Drop the file
   again to update.

For development, paste `launch_biped_rig_builder.py` into the Script Editor and run it.
It runs straight from the folder and reloads the code on every run.

**Requirements:** Maya 2022 or newer, which ships with numpy. The tool also avoids newer-only
nodes so it runs on older versions.

## Workflow

1. **Guides:** select the character, press Create Guides, then Fit to Mesh and adjust.
   The character should face +Z.
2. **Skeleton:** Build Skeleton.
3. **Skin:** Skin Mesh. Paint touch-ups if you like, then Mirror L>R.
4. **Correctives** (optional): add only the ones you need from the Correctives tab.
5. **Rig:** Build Rig. Remove Rig takes you back without losing the skin.

## How it works

- Positions and axes are computed from your guides, not copied from a template, so the
  rig adapts to any proportions.
- Skin weights are solved in pure numpy (`rig/weightmath.py`). The heat-map bind only
  decides which bone owns which area; the solve then builds every joint blend from the
  mesh's own thickness.
- Rig behaviour lives in JSON (`data/`): control layout, locks, switches, spaces and
  correctives can be changed without touching code.

| Folder | Contents |
|---|---|
| `core/` | naming, maths, node helpers, mesh queries |
| `rig/` | guides, skeleton, skinning, correctives, controls, IK/FK systems |
| `data/` | skeleton template, control layout, rig rules |
| `ui/` | the tool window |

## Contact

Feedback and bug reports: eeb78120@gmail.com
