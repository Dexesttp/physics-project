# Physics Project

## Main objective

This project aims to study the internals of Havok Cloth physics system, in order to adapt it
manually to other needed shapes.

## Files

The files included here are fragments used for simulating all effects on Sturges' clothing
(`Fallout4 - Meshes.ba2\Meshes\Clothes\Sturgess\SturgesFTorso.nif`).

In particular, the "googles physics" are used.

The original files themselves aren't included, but can be extracted from the game files using both
[ba2extract](http://f4se.silverlock.org/) to get the .nif file from the .ba2 archive and
[Outfit Studio by Ousnius](https://github.com/ousnius/BodySlide-and-Outfit-Studio) to extract the
physics from the nif file.

## Working with the files

It is recommended to use [Visual Studio Code](https://code.visualstudio.com/).

You'll need HKXPack, which you can get from [its GitHub repository](https://github.com/Dexesttp/hkxpack).

The default path search for the HKXPack jar is `%git%/af4/hkxpack/cli/target/hkxpack-cli.jar`,
so you'll need to change it in the `.vscode/tasks.json` file if you want to use another path.

If you want to studychnage the binary files, you can use the
[Hexdump for VSCode](https://marketplace.visualstudio.com/items?itemName=slevesque.vscode-hexdump) VSCode extension.

Then, each time you modify the xml files, you can recompile them using the `Ctrl`+`Shift`+`B` shortcut
or the `run buld task` Visual Studio code command.

## Documentation

All documentation found about the cloth files is available in the `doc/` subfolder.

This includes a rundown of the structure of a typical `hclClothData` item, under `cloth_data_notes`.

The other files are specific to the current item.

The `osd_notes` file describes the object skin definition, used to link vertices to bones.

The `vss_slc_notes` file describes the hard constraints between vertices and particles (done through vertec/particle pairs and standard link constraints).

The `constraints_notes` file describes the actual constraints between items and attempt to link them to a side of the body.

## License

All the original files are Bethesda products made from Havok tools, however they have been so heavily modified that the original license shouldn't apply.
So here's my approach on this.

```text
Copyright © 2016 DexesTTP <dexes.ttp at gmail.com>
This work is free. You can redistribute it and/or modify it under the
terms of the Do What The Fuck You Want To Public License, Version 2,
as published by Sam Hocevar. See the LICENSE.txt file for more details.
```

If you're a Bethesda, Havok or Microsoft representative, and you believe this repository shouldn't exist (with relevant arguments), feel free to drop me an email/issue.

## Credits

Dexesttp

## Special thanks

Bethesda, for the awesome Fallout 4 game that we haven't even scratched the surface of compared to Skyrim.

Havok, for their engine that really can do miracles.

Microsoft, for pulling out the HCT and forcing me to study and learn a lot about the Havok internals :P (also VS Code is pretty cool I guess)

Ousnius, for the BodySlide/Outfit Studio tool as well as his _really convincing arguments_ that kept me going.

The NifTools team, for their thourough documentation of the Nif files that helpoed us a lot in determinign what to search.

The SKSE team, for their awesome work on ba2extract and general analysis stuff.
