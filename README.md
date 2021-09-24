# PVC Relocator

Move Kubernetes Persistent Volume Claims (PVCs) from one Namespace to another

## Requirements

* **You must take backups first, otherwise you might lose all your data if something goes wrong**
* **You always run the risk of data loss when messing with PVCs, so take backups before beginning**
* The source and destination Namespaces must already exist
* Your shell must already have `kubectl` set up without needing any additional args (e.g. don't need `--kubeconfig=whatever`)

## Usage

Edit the script and set the `SRCNS`, `DESTNS` and `PVC` variables how you want.

Then just `./pvc-relocator.sh`.

Output should look similar to this:

```
Plan Summary

PVC to move: "tautulli"
         PV: "pvc-bf411943-088e-4c88-97af-d73a67ad92b4"
    from NS: "default"
      to NS: "media"

Are you sure? [y/N] y
persistentvolume/pvc-bf411943-088e-4c88-97af-d73a67ad92b4 patched (no change)
Changed reclaim policy on pvc-bf411943-088e-4c88-97af-d73a67ad92b4 to Retain
Deleting original PVC from "default" (don't panic)...
persistentvolumeclaim "tautulli" deleted
Disconnecting PV from PVC...
persistentvolume/pvc-bf411943-088e-4c88-97af-d73a67ad92b4 patched
Creating new PVC...
persistentvolumeclaim/tautulli created
Linking PV to new PVC...
persistentvolume/pvc-bf411943-088e-4c88-97af-d73a67ad92b4 patched
```

The script gives you one chance to change your mind.

Good luck!

# DISCLAIMER

Use at your own risk. You took backups first, right?
