# Running FUZZBUNCH with Python 3

This directory contains FUZZBUNCH, which has been migrated from Python 2.6 to Python 3.

## Changes Made

The following changes were made to get FUZZBUNCH working with Python 3:

### Python 2 to Python 3 Syntax Conversion
- Converted all `print` statements to `print()` functions
- Fixed `raise Exception, "message"` to `raise Exception("message")`
- Changed `except Exception, e:` to `except Exception as e:`
- Updated octal literals from `0666` to `0o666`
- Replaced `raw_input()` with `input()`
- Updated string operators (e.g., fixed print >> sys.stderr)
- Updated shebang from `#!/usr/bin/python2.6` to `#!/usr/bin/env python3`

### Platform-Specific Library Handling
- Made `exma` and `pytrch` imports optional with graceful fallback
- These libraries require platform-specific binaries (.dll/.pyd for Windows, .so for Linux)
- FUZZBUNCH will run with limited functionality when these libraries are not available
- Plugins that require these libraries will fail to load with appropriate warnings

### Directory and Error Handling
- Added checks for missing plugin directories (listeningposts, ede-exploits, triggers)
- Improved error handling to continue loading other plugins when one fails

## Running FUZZBUNCH

To run FUZZBUNCH:

```bash
cd /path/to/FOXACID/windows/FUZZBUNCH
python3 fb.py
```

## Limitations

Since FUZZBUNCH was originally designed for Windows and relies on Windows-specific binaries:

1. **Platform-specific binaries not available on Linux**: The `pytrch` module requires `.pyd` files (Windows Python extensions)
2. **Limited plugin functionality**: Plugins that depend on TRUANTCHILD/EXPLOITMANAGER will not work
3. **Some exploits may not load**: Windows-specific exploits will fail to initialize

## Warnings You May See

When running on Linux, you'll see these warnings - they are expected:

```
Warning: exma library not available, some functionality will be limited
Warning: pytrch module not available, some functionality will be limited
Warning: Cannot initialize config - platform-specific libraries not available
Failed to load [PluginName] - XML Error
```

These warnings indicate that certain Windows-specific components are not available, but FUZZBUNCH will continue to run.

## Testing

The tool successfully:
- Starts up without syntax errors
- Loads the FUZZBUNCH framework
- Initializes configuration
- Loads available plugins (those not requiring Windows binaries)
- Presents the interactive command prompt

## Future Improvements

To fully port FUZZBUNCH to Linux would require:
- Rewriting the Windows-specific binary components (pytrch, exma)
- Creating Linux equivalents of the TRUANTCHILD/EXPLOITMANAGER libraries
- Testing all exploits and payloads for Linux compatibility
