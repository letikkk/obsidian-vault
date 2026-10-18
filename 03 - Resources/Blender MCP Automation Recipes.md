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
created: 2026-10-18
status: active
---

# 🧊 Resource: Blender MCP Automation Recipes

> **Production Python automation recipes for Blender MCP. Generates tactile beveled chunky voxel geometry, multi-part color separation, skinned armature rigs, and clean `.glb` exports.**

---

## 1. Chunky Voxel Prop with Tactile Edge Bevels

```python
import bpy
import bmesh
import math

def create_beveled_voxel_block(name, size, location, bevel_width=0.08, segments=2):
    mesh = bpy.data.meshes.new(name)
    obj = bpy.data.objects.new(name, mesh)
    bpy.context.collection.objects.link(obj)
    
    bm = bmesh.new()
    bmesh.ops.create_cube(bm, size=1.0)
    
    # Scale cube to desired dimensions
    bmesh.ops.scale(bm, vec=size, verts=bm.verts)
    
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
    
    # Apply 35 degree auto-smooth shading
    bpy.context.view_layer.objects.active = obj
    obj.select_set(True)
    bpy.ops.object.shade_smooth_by_angle(angle=math.radians(35))
    
    return obj
```

---

## 2. Multi-Part Color Split & Studio Material Assignment

```python
import bpy

def assign_roblox_part_metadata(obj, part_color_name, material_variant="Studs"):
    """
    Tags a Blender object for Roblox MeshPart BrickColor and MaterialVariant mapping.
    """
    mat = bpy.data.materials.new(name=f"MAT_{part_color_name}_{material_variant}")
    mat.use_nodes = True
    
    # Set custom properties consumed during Roblox Studio import script
    obj["RobloxBrickColor"] = part_color_name
    obj["RobloxMaterialVariant"] = material_variant
    
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
    # Parent with Armature Modifier
    mesh_obj.parent = armature_obj
    mod = mesh_obj.modifiers.new(name="Armature", type='ARMATURE')
    mod.object = armature_obj
    
    # Create matching vertex group and assign all vertices
    vg = mesh_obj.vertex_groups.new(name=bone_name)
    all_vert_indices = [v.index for v in mesh_obj.data.vertices]
    vg.add(all_vert_indices, 1.0, 'REPLACE')
```

---

## 4. Production `.glb` Export Routine (Preserving Armatures)

```python
import bpy

def export_roblox_glb(filepath):
    """
    Exports scene models to .glb with export_apply=False to preserve Armature hierarchies.
    """
    bpy.ops.export_scene.gltf(
        filepath=filepath,
        export_format='GLB',
        use_selection=False,
        export_apply=False, # Mandatory: Keep Armature modifier and bones alive
        export_yup=True,
        export_skins=True,
        export_morph=False
    )
```

---

## 🔗 Related Vault Links
- 3D Art Area: [[02 - Areas/Blender Modeler & 3D Art|Blender Modeler & 3D Art]]
- Level Assembly: [[02 - Areas/World Building & Level Design|World Building & Level Design]]
- Spatial Math: [[03 - Resources/Spatial Math & Anti-Intersection Guide|Spatial Math & Anti-Intersection Guide]]
