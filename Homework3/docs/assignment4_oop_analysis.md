# Assignment 4: OOP Analysis - Pymatgen Sites Module

**Author:** Ardavan Mehdizadeh  
**Course:** ML4MSD - Homework 3  
**Date:** October 14, 2025

---

## What Does This Module Do?

The sites.py module defines two classes for representing atoms in materials: `Site` and `PeriodicSite`. Site is for non-periodic systems (molecules) with Cartesian coordinates. PeriodicSite extends Site for crystals, adding a lattice and fractional coordinates to handle periodic boundary conditions.

---

## OOP Concepts from Class

**Classes and Instances** - Site and PeriodicSite are classes, you create instances like `site1 = Site(...)`

**`__init__` method** - Initializer that sets up species, coordinates, properties

**Inheritance** - `PeriodicSite(Site)` inherits from Site, like `Metal(Material)` in class

**Properties** - Uses `@property` for managed attributes like `species`, `x`, `y`, `z`, plus `a`, `b`, `c` for PeriodicSite. Setting coords automatically updates between Cartesian and fractional

**Methods** - Regular methods like `distance(other)`, `to_unit_cell()`

**Class methods** - `from_dict(cls, dct)` creates instances from dictionaries

---

## Dunder Methods

### Covered in Class:
- `__init__` - constructor
- `__repr__` - detailed string for debugging
- `__str__` - user-friendly string  
- `__eq__` - equality comparison

### NOT Covered in Class:
- `__hash__` - makes sites hashable for sets/dicts
- `__lt__` - less-than for sorting
- `__getattr__` - attribute access fallback
- `__getitem__` - subscript notation like `site[element]`
- `__contains__` - `in` operator

### Mentioned in Exercise 8.1 (not in sites.py):
- `__add__`, `__sub__`, `__mul__`, `__truediv__` - arithmetic operators

---

## Site vs PeriodicSite

Site is for non-periodic systems like molecules and clusters. It only has Cartesian coordinates (x, y, z) and no concept of a lattice.

PeriodicSite extends Site for crystalline systems. It has both Cartesian (x, y, z) and fractional (a, b, c) coordinates, plus a Lattice object. The key feature is that when you change fractional coordinates, it automatically calculates the Cartesian coordinates using the lattice, and vice versa. This is essential for working with crystal structures because PeriodicSite understands periodic boundaries - it knows that an atom at fractional position [0.9, 0, 0] is equivalent to [-0.1, 0, 0] across the periodic boundary.