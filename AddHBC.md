
# Add a new HBC version

Add a new Hermes Bytecode to the tool. Steps below are mainly for iOS, but a similar concept applies for Android

## Steps

### Clone / Fork the repository and create a new branch

1. Download or clone this repository to your local machine
2. If creating a new branch, run `git checkout -b feat/new-hbc`

### Identify the React Native version

1. Download the .ipa for the application using your preferred tool / site. This may be [armconverter](https://armconverter.com/decryptedappstore), [decrypt.day](https://decrypt.day/), [AnyIPA](https://anyipa.me/), or something else
2. Unzip the .ipa file and find the `{something}.jsbundle` file
5. In the unzipped .ipa file, find `Frameworks/hermes.framework` and copy out the `hermes` file
6. Load that file in your favourite decompiler or hex editor and search for the string `for RN`

At the end of this, you should have the React native version in the format of `for RN 0.79.1`

### Find the hermes bytecode version reference

1. Navigate to https://github.com/facebook/react-native/tags and head to the tag identified above
    - This will be https://github.com/facebook/react-native/tree/v0.79.1
2. Using the `Go to file` search box on Github, search for `sdks/.hermesversion`

Now you'll have something like `hermes-2025-03-03-RNv0.79.0-bc17d964d03743424823d7dd1a9f37633459c5c5`

### Get the bytecode

1. Navigate to https://github.com/facebook/hermes, and head to the tag identified above
    - This will be https://github.com/facebook/hermes/tree/hermes-2025-03-03-RNv0.79.0-bc17d964d03743424823d7dd1a9f37633459c5c5
2. Now download the following files from the folder `include/hermes/BCGen/HBC` into your local repository under `utils/data`
    - `BytecodeList.def`
    - `BytecodeFileFormat.h`
    - `SerializedLiteralGenerator.h`
    - `BytecodeVersion.h`

### Generate new code

1. Navigate to `utils/tool`
2. Run `python opcode_generator.py` which will create the `data/opcode.json` file
3. Follow the instructions from that script for the next steps