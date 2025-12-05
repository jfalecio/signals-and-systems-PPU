# Compilation Guide for MATLAB Applications

This document provides instructions for compiling the interactive MATLAB applications to standalone executables using MATLAB Compiler.

## Prerequisites

### Required Software

1. **MATLAB** (R2023b or later)
   - Must be installed and licensed
   - Required for compilation only (not needed to run executables)

2. **MATLAB Compiler Toolbox**
   - Must be installed as part of MATLAB
   - Check installation: `ver` command in MATLAB should list "MATLAB Compiler"

3. **Required MATLAB Toolboxes**
   - Signal Processing Toolbox
   - Audio System Toolbox (for audio-related applications)
   - These toolboxes are included in the compiled executables

### System Requirements

- Windows 10 or later (64-bit) for compiling Windows executables
- Sufficient disk space for compilation outputs (~500 MB per app)
- Administrator privileges may be required

## Quick Start

### Automated Compilation

A master compilation script is provided: `compile_all_apps.m`

1. Open MATLAB
2. Navigate to the repository root directory
3. Run the compilation script:
   ```matlab
   compile_all_apps
   ```

This script will:
- Compile all 18 applications
- Create the `Executables/` directory structure
- Place executables in the correct locations
- Generate `readme.txt` files for each executable

**Note**: The compilation script (`compile_all_apps.m`) is excluded from the repository (in `.gitignore`) as it's an internal build tool.

## Manual Compilation

### Basic Compilation Command

For a simple function-based application:

```matlab
mcc -m -v -R -nosplash -R -nodisplay -o app_name app_file.m
```

### Parameters Explained

- `-m`: Create a standalone executable
- `-v`: Verbose output (shows compilation progress)
- `-R -nosplash`: Suppress MATLAB splash screen
- `-R -nodisplay`: Suppress display output
- `-o app_name`: Specify output executable name
- `app_file.m`: Input MATLAB file to compile

### Adding Dependencies

If the application uses files from other directories:

```matlab
mcc -m -v -R -nosplash -R -nodisplay -a "path/to/dependencies" -o app_name app_file.m
```

- `-a "path"`: Add directory to CTF (Component Technology File) archive

## Compiling Specific Application Types

### Function-Based Applications

Most applications are simple functions. Example:

```matlab
% Compile interactive_pure_tone_generator.m
cd 'Interactive Matlab Apps/lec01'
mcc -m -v -R -nosplash -R -nodisplay -o interactive_pure_tone_generator interactive_pure_tone_generator.m
```

### Class-Based Applications

Class-based applications (DT_main, CT_main) require wrapper functions:

1. **Create a wrapper function** that instantiates the class:
   ```matlab
   function DT_main_wrapper()
       app = DT_main();
   end
   ```

2. **Compile the wrapper**:
   ```matlab
   cd 'Interactive Matlab Apps/lec04/Discrete Time Convolution'
   mcc -m -v -R -nosplash -R -nodisplay -a "." -o DT_main DT_main_wrapper.m
   ```

The `compile_all_apps.m` script automatically creates and uses wrapper functions for class-based apps.

### Multi-File Applications

Applications with multiple supporting files (like FourierSeriesApp):

```matlab
cd 'Interactive Matlab Apps/lec07/FourierSeriesApp'
mcc -m -v -R -nosplash -R -nodisplay -a "." -o CT_Fourier_Series_App CT_Fourier_Series_App.m
```

The `-a "."` flag includes all files in the current directory.

## Application-Specific Notes

### Lecture 1 Apps

**Files**: `interactive_pure_tone_generator.m`, `interactive_audio_manipulation.m`, `Time_transformation_examples.m`

- Simple function-based apps
- No special dependencies
- Standard compilation

### Lecture 2 Apps

**Files**: 5 interactive apps

- All function-based
- Some require Audio System Toolbox
- Standard compilation

### Lecture 4 Apps

**DT_main** (Class-based):
- Requires wrapper function
- Multiple supporting class files (DT_convolution_engine, DT_signal_parser, etc.)
- Use `-a "."` to include all files

**Other apps**: Standard function-based compilation

### Lecture 5 Apps

**CT_main** (Class-based):
- Requires wrapper function
- Multiple supporting class files
- Use `-a "."` to include all files

### Lecture 7 Apps

**FourierSeriesApp**:
- Main file: `CT_Fourier_Series_App.m`
- Supporting files: `CT_FS_Math.m`, `CT_FS_PlotManager.m`, etc.
- Use `-a "."` to include directory

**DTFourierSeriesApp**:
- Main file: `DT_Fourier_Series_App.m`
- Supporting files: `DT_FS_Math.m`, `DT_FS_PlotManager.m`, etc.
- Use `-a "."` to include directory

**BuildABeatSynthesizer**:
- Main file: `BuildABeatSynthesizer.m`
- Supporting file: `SynthesizerMath.m`
- Use `-a "."` to include directory

**DutyCycleSpectrumAnalyzer**:
- Main file: `DutyCycleSpectrumAnalyzer.m`
- Supporting file: `DutyCycleMath.m`
- Use `-a "."` to include directory

**Other apps**: Standard function-based compilation

## Output Files

After compilation, MATLAB Compiler generates several files:

### Executable Files

- `app_name.exe`: The standalone executable (this is what users run)
- `app_name.ctf`: Component Technology File (archive of MATLAB code and dependencies)
  - **Note**: `.ctf` files are excluded from the repository (in `.gitignore`)

### Documentation Files

- `readme.txt`: Automatically generated documentation
  - Contains MATLAB Runtime version requirements
  - System requirements
  - Installation instructions
  - **Note**: `readme.txt` files ARE included in the repository

### Other Generated Files (Excluded from Repo)

- `run_app_name.bat`: Batch script for running (intermediate file)
- `mccExcludedFiles.log`: Log of excluded files
- `for_testing/`: Testing directory
- `*.log`: Compilation logs

## Directory Structure for Executables

Executables should be placed in `Executables/Interactive Matlab Apps/` mirroring the source structure:

```
Executables/Interactive Matlab Apps/
├── lec01/
│   ├── interactive_pure_tone_generator.exe
│   ├── interactive_audio_manipulation.exe
│   ├── Time_transformation_examples.exe
│   └── readme.txt (for each app)
├── lec02/
│   └── ...
├── lec04/
│   ├── Discrete Time Convolution/
│   │   ├── DT_main.exe
│   │   └── readme.txt
│   └── ...
└── ...
```

## Troubleshooting Compilation

### Common Issues

#### 1. "mcc is not recognized"

**Problem**: MATLAB Compiler Toolbox not installed.

**Solution**: Install MATLAB Compiler Toolbox through MATLAB Add-Ons.

#### 2. "Cannot find function or variable"

**Problem**: Missing dependencies or files not in path.

**Solutions**:
- Use `-a` flag to add directories to CTF archive
- Ensure all required files are in the same directory or explicitly added
- Check that supporting files are accessible

#### 3. "Toolbox not found"

**Problem**: Required toolbox not available or not included.

**Solutions**:
- Verify toolbox is installed: `ver` command
- MATLAB Compiler should automatically detect and include toolboxes
- Check toolbox license is valid

#### 4. Large Executable Size

**Problem**: Executables are very large (>100 MB).

**Explanation**: This is normal. Executables include:
- MATLAB Runtime components
- Required toolboxes
- All dependencies
- Application code

**Note**: Users only need to install MATLAB Runtime once (shared across all apps).

#### 5. Class Compilation Errors

**Problem**: Errors when compiling class-based apps.

**Solutions**:
- Use wrapper function approach (see Class-Based Applications section)
- Ensure all class files are in the same directory
- Use `-a "."` to include current directory

### Verification

After compilation, verify the executable:

1. **Check file exists**: Verify `.exe` file was created
2. **Check readme.txt**: Verify `readme.txt` was generated
3. **Test run**: Try running the executable (requires MATLAB Runtime)
4. **Check size**: Executable should be substantial (>10 MB typically)

## Best Practices

1. **Test Before Compiling**: Ensure the application runs correctly in MATLAB first
2. **Clean Directory**: Remove old compilation artifacts before recompiling
3. **Version Control**: Don't commit intermediate files (`.ctf`, `.bat`, etc.)
4. **Documentation**: Keep `readme.txt` files with executables
5. **Consistent Naming**: Use consistent naming for executables
6. **Directory Structure**: Maintain the same structure as source code

## MATLAB Runtime Version

The MATLAB Runtime version required by executables matches the MATLAB version used for compilation:

- **MATLAB R2023b** → **MATLAB Runtime R2023b**
- **MATLAB R2024a** → **MATLAB Runtime R2024a**

**Important**: Document the MATLAB version used for compilation. Users need to install the matching MATLAB Runtime version.

## Automation

The `compile_all_apps.m` script automates:
- Creating directory structure
- Compiling all applications
- Handling class-based apps (wrapper creation)
- Organizing output files
- Moving files to correct locations

For manual compilation or customization, refer to the sections above.

## Additional Resources

- [MATLAB Compiler Documentation](https://www.mathworks.com/help/compiler/)
- [MATLAB Compiler User's Guide](https://www.mathworks.com/help/compiler/compiler-applications.html)
- [MATLAB Runtime Documentation](https://www.mathworks.com/help/compiler/matlab-runtime.html)

## Notes

- Compilation must be done on Windows to create Windows executables
- Cross-platform compilation requires the target platform's MATLAB installation
- Executables are platform-specific (Windows executables won't run on Mac/Linux)
- The compilation script is excluded from the repository (internal build tool)

---

**For Users**: If you just want to run the applications, see [Executables/README.md](Executables/README.md) instead of this document.

**For Developers**: Use this guide to compile applications or modify the compilation process.

