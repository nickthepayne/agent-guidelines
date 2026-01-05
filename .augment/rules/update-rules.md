---
type: "always"
---

# Global Rules Sync

> ⛔ **STOP — ACTION REQUIRED AFTER EDITING `.augment-global/`**
>
> If you have just edited ANY file in the `.augment-global` folder:
>
> **ASK THIS EXACT QUESTION:**
> "Would you like me to apply these changes to your global augment configuration?"
>
> - If confirmed → Run the sync command below
> - If declined → Continue without syncing
>
> **DO NOT proceed to other tasks until you have asked this question.**

If confirmed, run this command to copy the rules to the global augment configuration:

```bash
mkdir -p ~/.augment/rules && cp -r .augment-global/rules ~/.augment
```