---
title: Blender MCP Automation Recipes
categories:
  - "[[Resources]]"
tags:
  - resource
  - roblox
  - blender
  - mcp
  - python
  - 3d-modeling
  - animation
created: 2026-10-18
updated: 2026-10-25
status: active
---

# 🧊 Resource: Blender MCP Automation Recipes

> **Production Python automation recipes for Blender MCP. Generates tactile beveled chunky voxel geometry, multi-part color separation, bottom-aligned crate origins, skinned armature rigs, and clean `.glb` exports.**

---

## 1. Chunky Voxel Prop with Tactile Edge Bevels & Bottom-Aligned Pivot

```python
import bpy
import bmesh
import math

def create_beveled_voxel_block(name, size, location, bevel_width=0.08, segments=2, align_bottom=True):
    """
    Creates a tactile beveled voxel volume with origin resting on the bottom contact face.
    """
    mesh = bpy.data.meshes.new(name)
    obj = bpy.data.objects.new(name, mesh)
    bpy.context.collection.objects.link(obj)
    
    bm = bmesh.new()
    bmesh.ops.create_cube(bm, size=1.0)
    
    # Scale cube to desired dimensions (X, Y, Z)
    bmesh.ops.scale(bm, vec=size, verts=bm.verts)
    
    # Offset vertices so bottom face rests exactly at Z = 0 (Roblox bottom contact plane)
    if align_bottom:
        bmesh.ops.translate(bm, vec=(0, 0, size[2] / 2.0), verts=bm.verts)
    
    # Apply tactile bevel (The Anti-Razor Rule)
    edges = [e for e in bm.edges]
    bmesh.ops.bevel(
        bm,
        geom=edges,
        offset=bevel_width,
        offset_type='OFFSET',
        segments=segments,
        profile=0.5,
        affect='EDGES',
        clamp_overlap=True
    )
    
    bm.to_mesh(mesh)
    bm.free()
    
    obj.location = location
    
    # Apply 35 degree auto-smooth angle preservation
    bpy.context.view_layer.objects.active = obj
    obj.select_set(True)
    bpy.ops.object.shade_smooth_by_angle(angle=math.radians(35))
    
    return obj
```

---

## 2. Multi-Part MaterialVariant & BrickColor Assignment

```python
import bpy

def assign_roblox_part_metadata(obj, part_color_name, material_variant="Studs", is_neon=False):
    """
    Tags a Blender object for Roblox MeshPart BrickColor and MaterialVariant mapping.
    Supported MaterialVariants: 'Studs', 'Weld', 'Universal', 'Glue'.
    Emissive parts set is_neon=True (Material = Enum.Material.Neon).
    """
    mat_name = f"MAT_{part_color_name}_{'Neon' if is_neon else material_variant}"
    mat = bpy.data.materials.new(name=mat_name)
    mat.use_nodes = True
    
    # Set custom properties consumed during Roblox Studio import script
    obj["RobloxBrickColor"] = part_color_name
    obj["RobloxMaterialVariant"] = "" if is_neon else material_variant
    obj["RobloxMaterial"] = "Neon" if is_neon else "Plastic"
    
    if obj.data.materials:
        obj.data.materials[0] = mat
    else:
        obj.data.materials.append(mat)
```

---

## 3. Skinned Armature Rigging & Rigid Bone Weighting (`1.0`)

```python
import bpy

def rig_mesh_to_bone(mesh_obj, armature_obj, bone_name):
    """
    Parents a color-separated mesh to an armature and assigns 100% rigid weight to bone.
    """
    mesh_obj.parent = armature_obj
    mod = mesh_obj.modifiers.new(name="Armature", type='ARMATURE')
    mod.object = armature_obj
    
    # Create matching vertex group and assign all vertices
    vg = mesh_obj.vertex_groups.new(name=bone_name)
    all_vert_indices = [v.index for v in mesh_obj.data.vertices]
    vg.add(all_vert_indices, 1.0, 'REPLACE')
```

---

## 4. Multi-Layer Volumetric 3D Eye Builder

```python
import bpy

def create_3d_beveled_eye(parent_obj, eye_center, eye_radius=0.25, is_left=True):
    """
    Constructs a 100% 3D beveled mesh eye (Sclera + Pupil + Catchlight) with zero 2D decals.
    """
    # 1. White Sclera
    sclera = create_beveled_voxel_block(
        name=f"Eye_Sclera_{'L' if is_left else 'R'}",
        size=(eye_radius * 2, eye_radius * 0.4, eye_radius * 2),
        location=eye_center,
        bevel_width=0.04,
        align_bottom=False
    )
    assign_roblox_part_metadata(sclera, "Institutional white", "Studs")
    
    # 2. Really Black Pupil (offset slightly forward)
    pupil_offset = (eye_center[0], eye_center[1] - (eye_radius * 0.25), eye_center[2])
    pupil = create_beveled_voxel_block(
        name=f"Eye_Pupil_{'L' if is_left else 'R'}",
        size=(eye_radius * 1.2, eye_radius * 0.2, eye_radius * 1.2),
        location=pupil_offset,
        bevel_width=0.03,
        align_bottom=False
    )
    assign_roblox_part_metadata(pupil, "Really black", "Studs")
    
    # 3. White Specular Catchlight (offset top-right)
    catchlight_offset = (pupil_offset[0] + 0.05, pupil_offset[1] - 0.02, pupil_offset[2] + 0.05)
    catchlight = create_beveled_voxel_block(
        name=f"Eye_Highlight_{'L' if is_left else 'R'}",
        size=(eye_radius * 0.35, eye_radius * 0.1, eye_radius * 0.35),
        location=catchlight_offset,
        bevel_width=0.015,
        align_bottom=False
    )
    assign_roblox_part_metadata(catchlight, "Institutional white", "Neon", is_neon=True)
    
    return [sclera, pupil, catchlight]
```

---

## 5. Production `.glb` Export Routine (Preserving Armatures & Bottom Pivots)

```python
import bpy

def export_roblox_glb(filepath):
    """
    Exports scene models to .glb with export_apply=False to preserve Armature hierarchies and animations.
    """
    bpy.ops.export_scene.gltf(
        filepath=filepath,
        export_format='GLB',
        use_selection=False,
        export_apply=False, # Mandatory: Keep Armature modifier, bone weights, and animations intact
        export_yup=True,
        export_skins=True,
        export_morph=False,
        export_animations=True
    )
```

---

## 🔗 Related Vault Links
- 3D Art Area: [[02 - Areas/Blender Modeler & 3D Art|Blender Modeler & 3D Art]]
- Level Assembly: [[02 - Areas/World Building & Level Design|World Building & Level Design]]
- Spatial Math: [[03 - Resources/Spatial Math & Anti-Intersection Guide|Spatial Math & Anti-Intersection Guide]]
