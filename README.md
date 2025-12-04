# UBT (Unity Bundle Tool)

A powerful, user-friendly command-line tool to extract and repack Unity asset bundles. Built with Python and UnityPy.

**Developer:** [minhmc2007](https://github.com/minhmc2007)

---

## Installation

Install the tool directly from PyPI:

```bash
pip install unity-bundle-tool
```

## Usage

Once installed, you can use the `ubt` command from your terminal.

### Extract a Bundle

```bash
ubt extract path/to/your/asset.bundle path/to/output_folder/
```

This will create:
```
output_folder/
├── manifest.json           # Asset tracking manifest
├── Textures/              # PNG files from Texture2D/Sprite assets
├── TextAssets/            # TXT/bytes files from TextAsset objects
├── MonoBehaviours_JSON/   # JSON files from MonoBehaviour typetrees
├── MonoBehaviours_DAT/    # Raw binary data from MonoBehaviours
├── AudioClips/            # WAV or raw audio files
└── OtherAssets/           # Generic binary data from other asset types
```

### Repack a Bundle

After modifying files, repack them into a new bundle:

```bash
ubt repack path/to/output_folder/ path/to/new_repacked.bundle
```

**Important**: The input directory must contain the `manifest.json` file created during extraction. The original bundle file referenced in the manifest must still exist and be accessible.

## Features

- Extract Unity bundle files to organized directory structure
- Support for multiple asset types:
  - **Textures** (Texture2D, Sprite) → PNG files
  - **Text Assets** → TXT/bytes files
  - **MonoBehaviours** → JSON (typetree) or DAT (raw binary)
  - **Audio Clips** → WAV or raw audio data
  - **Generic Assets** → Raw binary data
- Repack modified assets back into Unity bundle format
- Automatic file sanitization and organization
- Detailed manifest tracking for reliable repacking

## Asset Type Support

| Asset Type | Extraction Format | Repacking Support |
|------------|------------------|-------------------|
| Texture2D/Sprite | PNG | ✅ Yes |
| TextAsset | TXT/bytes | ✅ Yes |
| MonoBehaviour (with typetree) | JSON | ✅ Yes |
| MonoBehaviour (raw) | DAT binary | ⚠️ Limited |
| AudioClip | WAV/raw audio | ⚠️ Limited |
| Other types | Raw binary | ⚠️ Limited |

## Workflow

1. **Extract** a bundle to examine and modify assets
2. **Modify** the extracted files as needed:
   - Edit PNG images in image editors
   - Modify text files
   - Edit JSON files for MonoBehaviour data
3. **Repack** the modified assets into a new bundle

## Important Notes

- **Keep the original bundle file**: Repacking requires the original bundle as a template
- **Preserve file structure**: Don't move files between the organized subdirectories
- **Manifest dependency**: The `manifest.json` file is essential for repacking
- **Binary compatibility**: Some asset modifications may not work depending on Unity version and asset complexity
- **Backup your files**: Always keep backups of original bundles before modification

## Error Handling

The script includes comprehensive error handling for:
- Corrupted or protected bundle files
- Missing dependencies
- Invalid file paths
- Asset processing failures
- Repacking inconsistencies

## Limitations

- MonoBehaviour repacking from raw DAT files has limited reliability
- AudioClip repacking may not preserve original compression formats
- Some Unity-specific asset formats may not be fully supported
- Protected or encrypted bundles cannot be processed

## Command Line Help

```bash
ubt --help
ubt extract --help
ubt repack --help
```

## License

This project is licensed under the GPL 3 License.
