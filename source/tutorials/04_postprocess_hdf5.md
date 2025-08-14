# Tutorial 4 — Post‑processing HDF5 outputs

Many cases write **HDF5**. Here’s a minimal Python snippet to inspect datasets.

```python
import h5py, sys
fn = sys.argv[1] if len(sys.argv)>1 else "output.h5"
with h5py.File(fn, "r") as f:
    def walk(g, indent=0):
        for k, v in g.items():
            print("  "*indent + k, type(v))
            if isinstance(v, h5py.Group):
                walk(v, indent+1)
    walk(f)
```

For visualisation, convert to your preferred format (e.g. XDMF) or load directly in ParaView with the HDF5 or XDMF readers if provided.
