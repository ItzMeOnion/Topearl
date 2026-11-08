# TP's Anchor Optimiser

A client-side Fabric mod for **Minecraft Java 1.21.11**. Disguise any item or block as another one:

- Pick what the item/block **looks like** from a searchable list of every item.
- Give it a **custom name** and choose the **name colour** (16 chat colours or any hex colour).
- Placed blocks really take the look-alike's model, and use its **render layer**, so a disguised
  spawner is properly **see-through in the cage gaps**.
- Hides the real item id shown by F3+H advanced tooltips (switchable per disguise).

Only you see the changes. Servers and other players are unaffected.

## Using it

Press **K** in game to open the menu (rebind it in Controls, under Miscellaneous).

- **+ Add disguise** -> choose the item to disguise (or click "Held item"), choose what it looks like,
  type a name, pick a colour, Save.
- **Waxed/oxidised too** applies the rule to the exposed / weathered / oxidised / waxed versions of
  copper items, so the disguise does not break when copper ages.
- Rules are saved in `config/tps_anchor_optimiser.json`.

First run comes with:
- copper block -> Netherite Block
- cut copper stairs -> purple "Skeleton Spawner" (see-through cage gaps)
- copper bulb -> Gilded Blackstone
- golden chestplate -> pink "Elytra"
- copper nugget -> Netherite Ingot

If you already used an older version, your saved rules in `config/tps_anchor_optimiser.json` are kept.
Delete that file to get the defaults back.

## Known limits

- Looks only: hitbox, sounds, breaking speed and what the item actually does are unchanged.
  Disguised stairs still have a stair-shaped hitbox.
- A worn disguised chestplate still shows the real armour on your body.
- Made for the vanilla renderer. Sodium / Iris and similar rendering mods may ignore the block changes.
- Next to a see-through disguised block, a neighbouring block can hide a face you would expect to see
  through the gaps. This is a vanilla culling quirk of looking like a non-solid block.

## Building it on GitHub (no installs needed)

1. Make a free account at github.com, click **+** -> **New repository**, name it, click **Create repository**.
2. Unzip the project. **Before uploading**, if you have your own mod picture, put it in
   `src/main/resources/assets/tps_anchor_optimiser/` and name it `icon.png` (replace the one there).
   It must be a real PNG, not a WebP renamed.
3. On the new repo page click **uploading an existing file** and drag in **everything inside the
   unzipped folder** (the `src` folder, `build.gradle`, `.github`, etc.). Click **Commit changes**.
   - If the `.github` folder did not upload: **Add file -> Create new file**, type the name
     `.github/workflows/build.yml`, paste in the contents of that file, commit.
4. Open the **Actions** tab. A run called **build** starts by itself. Wait for the green tick
   (about 3-6 minutes). If Actions is disabled, click the green button to enable it.
5. Click the finished run, scroll to **Artifacts**, download **TPs-Anchor-Optimiser**, unzip it.
   The `.jar` inside is the mod.
6. Re-run any time with **Actions -> build -> Run workflow**.

The build file finds the project folder by itself, so it still works if the files end up inside an
extra folder.

## Installing

1. Install Fabric for 1.21.11: https://fabricmc.net/use/installer/
2. Download **Fabric API** for 1.21.11 (version 0.141.5+1.21.11) from https://modrinth.com/mod/fabric-api
3. Put the Fabric API jar and `tps-anchor-optimiser-1.1.0.jar` in `.minecraft/mods`.
   Remove any older TP's Anchor Optimiser jar first.
4. Start the "fabric-loader-1.21.11" profile. The mod icon shows in the Mods list if you also
   install Mod Menu (https://modrinth.com/mod/modmenu).

## Changing the description or picture

- Description: `src/main/resources/fabric.mod.json`, the `"description"` line.
- Picture: `src/main/resources/assets/tps_anchor_optimiser/icon.png` (square PNG, 128x128 or bigger).

## Where the code is

- `Rules.java` - the rules, saving, and the lookups everything else uses
- `RulesScreen.java`, `EditRuleScreen.java`, `ItemPickerScreen.java` - the menu
- `mixin/ItemModelResolverMixin.java` - swaps item models (inventory, hand, ground)
- `mixin/BlockModelShaperMixin.java` - swaps placed-block models
- `mixin/ItemBlockRenderTypesMixin.java` - swaps the render layer (spawner transparency)
- `mixin/ItemStackMixin.java` - names and name colours, hides the item id tooltip line

## Licence

MIT. Minecraft is a trademark of Mojang / Microsoft. This mod contains no Minecraft assets; look-alikes
are drawn from your own game files.
