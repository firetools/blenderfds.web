---
layout: default
title: Release notes
nav_order: 3
---

# Release notes
{: .no_toc }

This page describes BlenderFDS evolution.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Current versions

### DEV: [BlenderFDS main development repository](https://github.com/firetools/blenderfds)

The current development version is verified to work with **Blender 2.93.0**,
and supports import/export to **FDS 6 and 7** (unreleased).
This version is not intended for production environments.

### 2021-02-16: [BlenderFDS 5.1.0](https://github.com/firetools/blenderfds/releases/tag/v5.1.0)

This new **minor** release is verified to work with **Blender 2.91.2**,
and supports import/export to **FDS 6 and 7** (unreleased).


#### New features for users:
{: .no_toc }

* As requested by the users, BlenderFDS now takes into account the Blender [View Layers](https://docs.blender.org/manual/en/latest/render/layers/layers.html) settings.
Blender collections that are not enabled in the current view layer, and all the contained objects, are excluded from exporting.
The user can set and export different geometric configurations from several `View layer` instances of the same `Scene`.

## Older versions

### 2020-11-12: [BlenderFDS 5.0.1](https://github.com/firetools/blenderfds/releases/tag/v5.0.1)
{: .no_toc }

A new **maintenance** release is out. Just bugfixing.

### 2020-11-05: [BlenderFDS 5.0.0](https://github.com/firetools/blenderfds/releases/tag/v5.0.0)
{: .no_toc }

A new **major** BlenderFDS release is out, ported to the Blender 2.9x series:

* Exporting target is **FDS version 7 (unreleased)**, but the exported file is compatible with the current released FDS solver (`File > Export > FDS case`).
* This BlenderFDS version shall be installed as an addon of **Blender 2.90.1**. It does **not** work with older versions and it **is not guaranteed** to work with newer ones.
* The new file format is not fully backward compatible, so double check your old input files.

#### New features for users:
{: .no_toc }

* All the new Blender 2.9x features for 3d modelling, see its [release notes](https://wiki.blender.org/wiki/Reference/Release_Notes)
* New managed namelists: `GEOM`, `PRES`, `CATF`, `MOVE`.
* The `GEOM` namelist offers tools for:
  * automatic improvement of Blender Mesh quality and detection of defects that render it not manifold;
  * checking for intersections with other Blender Objects;
  * exporting and importing the new binary `bingeom` format (`BINARY_FILE`);
  * exporting and importing terrains (`IS_TERRAIN`);
* New operator for setting geolocation of any element into the FDS case, after georeferencing your case by setting the origin geolocation.
  For example, you can put a `DEVC` at a specific coordinate without effort, and check the position on an online map.
* New `Align selected` operator for `MESH`, that correctly aligns MESH cells.
* New management tool for *other parameters*, in addition to those that are directly managed.

#### New features for developers:
{: .no_toc }

* The new verification suite automatically checks the code by performing full import and export of all the official FDS V&V cases.
* The Blender Object, Material, Collection, and Scene are extended with `from_fds()` and `to_fds()` methods.
* The code is fully documented with Doxygen. 
* Cleaner Python code structure, fully object-oriented.
* The code is now linted with `pylint` and formatted with `black`.

### 2018-09-23: BlenderFDS 4.3.0
{: .no_toc }

A new **minor** release is out. Even if `minor`, this release is **packed with new features**, developed during my six months visit at NIST as a guest researcher. A great *thank you* to all the friends there, it was an amazing stay both from a professional and personal point of view! And a lot of work is now laying ahead.

This release was badly delayed by the [Morandi bridge collapse](https://www.nytimes.com/interactive/2018/09/06/world/europe/genoa-italy-bridge.html) in Genoa, Italy. The collapse caused 43 casualties, around 630  people evacuated from their homes, the disruption of the economic and transportation systems of the city. [We](http://www.vigilfuoco.it) are still very busy working on the recovery.

Now back to BlenderFDS.

#### New features for users:
{: .no_toc }

* New `FDS Case config` panel for each Blender Scene. 
* Vastly improved support for `GEOM` namelist:
  * New triangulation algorithm, now much more stable.
  * New full fledged automatic geometry quality checks for all defects:
    * non manifold edges and vertices,
    * non contiguous or inverted normals,
    * open geometry,
    * degenerate or duplicate faces and edges,
    * loose geometry,
    * self-intersecting geometry.
  * Added `Get intersection with` operator to check for intersections between selected objects.
  * When a geometry quality error condition is detected, the offending vertices, faces, edges are now _selected_, to assist the user debugging the geometry.
  * Setup of geometry _epsilon_ for edge length and face area is now possible on a per-case basis, in the new `Case config` panel.
  * Added the possibility to exclude the geometry quality checks from specific objects.
  * `Show geometry` operator now shows the exported geometry for `GEOMs` as well.
* Added support for `RADI` and `CATF` namelists.
* Improved support for Blender units (eg. imperial units), some issues still ongoing.
* Renewed voxelization and pixelization algorithms for `OBSTs` and `VENTs`, on average 3x speed up.
* Voxels and pixels can now be centered to the object bounding box, this allows the creation of truly symmetrical voxelized spheres.
* Added `CELL_CENTERED` parameter to `SLCF` namelist.
* While waiting for a proper configurability of the number of exported float digits of geometric coordinates, 6 decimal digits are now exported.
* New FDS default values treatment: default values are not exported to the FDS case. The default value is shown in the help message when hovering over the property field.

#### New features for developers:
{: .no_toc }

* Improved Python code structure towards the large transformations towards Blender 2.8 support
* Code clean-up for Python PEP8

### 2018-06-12: BlenderFDS 4.2.2
{: .no_toc }

A new **maintenance** release is out.

#### New features for users:
{: .no_toc }

* Bug fixing: UI, FDS file formatting.

### 2018-05-18: BlenderFDS 4.2.1
{: .no_toc }

A new **maintenance** release is out.

#### New features for users:
{: .no_toc }

* Bug fixing. Some Blender 2.79 packages have an older Python interpreter embedded, this was breaking BlenderFDS. Fixed!
* Pushing forward some minor simplified UI enhancements.

### 2018-05-14: BlenderFDS 4.2.0
{: .no_toc }

A new **minor** release is out.

#### New features for users:
{: .no_toc }

* Improvement of the voxelization algorithm, better continuity between close objects
* Experimental support for importing and exporting the future `GEOM` namelist
* New search tool for `MATL_ID` names
* Added `MPI_PROCESS` parameter to `MESH` namelist
* Exported FDS files have now a more compact format, as suggested by FDS developers
* Some bugfix and slight refactor

### 2016-11-24: BlenderFDS 4.1.1
{: .no_toc }

A new **maintenance** release is out.

While working on a new project I discovered that voxelization failed in some not infrequent cases.
It is now fixed.

### 2016-09-21: BlenderFDS 4.1.0
{: .no_toc }

A new **minor** release is out.

#### New features for users
{: .no_toc }

* The calculated FDS geometry is now cached inside Blender Objects. Exporting of unmodified objects to FDS is now lightning fast!
* Improved management of displayed FDS geometries
* Some bugfix and slight refactor

### 2016-04-06: BlenderFDS 4.0.6
{: .no_toc }

A new **maintenance** release is out.

The paths to predefined files were incorrectly determined in corner cases.
The bug is now fixed.

### 2016-03-15: BlenderFDS 4.0.5
{: .no_toc }

A new **maintenance** release is out.

Bojan Csoti spotted a little bug with oversized objects, thank you!
The bug is now fixed.

### 2016-03-04: BlenderFDS 4.0.4
{: .no_toc }

A new **maintenance** release is out.

Again bug fixing:

* Fixed link to wiki in Blender menu;
* Temporary object should never be exported, fixed!

and a little new nifty feature:

* new tool for selecting DEVC QUANTITY.

### 2016-02-11: BlenderFDS 4.0.3
{: .no_toc }

A new **maintenance** release is out.

While developing **automated testing procedure**, I am finding and fixing many bugs:

* Importing function was creating fake XB parameters in several objects. Solved!
* Wrong naming of input/output operators, fixed!
  * bpy.ops.export.fds_case() -> bpy.ops.export_scene.fds_case()
  * bpy.ops.import.fds_case() -> bpy.ops.import_scene.fds_case() or fds_snippet()

### 2016-02-11: BlenderFDS 4.0.2
{: .no_toc }

A new **maintenance** release is out:

* Added SP_DUMP_STATUS_FILES to DUMP namelist for automatic monitoring of case file running.
* New automated testing procedure before releasing (see `/dev/autotest`): all example cases are exported and run.
* Small bug fixing.

### 2016-02-04: BlenderFDS 4.0.1
{: .no_toc }

A new **maintenance** release is out. No new features, just bug fixing:

* Improved defaults and feedback to users for Operators.
* Facilitated addition of a new SURF related to a specific Blender Object (eg. OBST)
* Bug fixing. 

I :heart: GitHub.

### 2016-01-25: BlenderFDS 4.0.0
{: .no_toc }

A new **major** BlenderFDS release is out:

* Exporting target is **FDS version 6** (`File > Export > FDS case`).
* This BlenderFDS version shall be installed as an addon of **Blender 2.76b**. It does **not** work with older versions and it **is not guaranteed** to work with newer ones.
* The new file format is not backward compatible.

This is the first version after the huge migration to GitHub. This release was delayed by at least one year, because  I was very taken by the working-groups on the new Italian Fire Code.

#### Thank you!
{: .no_toc }

First of all, I would like to **sincerely thank** all the contributors that financially supported BlenderFDS development during the last crowdfunding campaign.

A particular thank goes to our sponsors:
* Sergei Maximov;
* backbone;
* Kristopher Overholt;
* Combustion Science & Engineering, Inc. (Stephen Olenick).

This version of BlenderFDS is the result of a huge effort: the codebase was complitely reviewed and restructured to make place for new features and guarantee future maintainability. The source code is now fully object oriented, fully commented, and much more readable.

#### New features for users
{: .no_toc }

* Simplified user interface.
* BlenderFDS can **import existing FDS case files** to BlenderFDS scenes (`File > Import > FDS case`).
* Creation of `GE1` **cad description file** (`Scene Panel > DUMP Panel`), that allows realistic visualization in Smokeview.
* New geometric description `PIXELS` for flat faces (`Object Panel > OBST Panel > XB`, for namelists that support faces). Faces of any shape, normal to any axis, can be exported to FDS (eg. round `VENTs`!).
* Namelist grouping and sorting by Blender empties (`Add Blender Menu > Empty`). Parent your namelists under a Blender Empty, and discover them **properly sorted and grouped** in the FDS case file.
* New tool for FDS MESH creation (`Object Panel > MESH Panel > IJK`): **set cell sizes and align** them to the global reference system, for easier mutual alignment of `MESHes`.
* New tool for calculating FDS `SURF` `HRRPUA` and `TAU_Q` according to EU and US standards (`Material Panel > SURF Panel > TAU_Q`).
* Improved user interface and tools:
  * geometry and code visualization buttons are now readily available in the user interface;
  * easier parameters copying between selected namelists.
* Faster and **more precise** voxelization algorithm.
* Free FDS text file is now fully integrated into Blender interface.
* `Show geometry` button visualizes the geometry as it is going to be exported to FDS. This allows the user to check it visually.
* Multiple geometries can now have a **suffix added to their** `IDs` (`Object Panel > Any namelist panel > ID`), eg. add z coordinate to thermocouples `ID` values: `tc+1.20, tc+1.30, tc+1.40, ...`
* Set default appearance and allowed geometry parameters on namelist change.
* File versioning, check and manage future transitions to new BlenderFDS file formats.
* Custom snippets path preference in `Blender User Preferences > Add-Ons` panel.

#### New features for developers
{: .no_toc }

* New *programming API*: `context.scene.to_fds()`, `context.object.to_fds()`, `context.material.to_fds()`, `context.scene.from_fds()`. Build or modify your geometry using Python programming language!
* New debug mode and timing.
* Detailed description of FDS language in `lang.py`.
