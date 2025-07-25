---
type: docs
url: "hub/docs/folder/Installation"
---

# Introduction

Artbox has an [AppImage](../AppImage/) made for a Debian based system, that is available to download. If you are interested in building your own version from the source code then read on. Artbox is a modified version of GIMP, if you can build GIMP, you can build Artbox. The program relies on many parts to function and many apps are used to construct it. You need to create a _build environment_ for it first, like an aquarium for a fish. The following is a guide, for a Debian system. It will be a unique process for your system, and may require further research. Good luck!

## Content

* [Git](#git)
* [Dependencies](#dependencies)
* [Install Location](#install-location)
* [Clone the Source Code Repositories](#clone-the-source-code-repositories)
* [Environment Variables](#environment-variables)
* [Build Environment Optimizations](#build-environment-optimizations)
* [Build Artbox, BABL and GEGL](#build-artbox-babl-and-gegl)
* [Desktop Launcher (System Specific)](#desktop-launcher-system-specific)
* [Automatically Updating](#automatically-updating-to-the-latest-development-version)
* [Manual Updating](#steps-to-manually-update)
* [Troubleshooting](#troubleshooting)
* [Conclusion](#conclusion)

## Git

Before we dive into building Artbox, you'll need to install and learn the basics of Git, a version control system that helps you manage and share source code. Git is an essential tool for any developer, and understanding how to use it will make the rest of the build process much easier. If you're new to Git, take a few minutes to read through [Using Git on Linux](../../../guides/folder/Using-Git-on-Linux/) to get up to speed.

## Dependencies

Here is the [official guide](https://developer.gimp.org/core/setup/build/linux/). The suggestion to look at [this](https://gitlab.gnome.org/GNOME/gimp/-/blob/master/.gitlab-ci.yml) file, that builds GIMP in the GitLab CI environment, is worth following. That file lists all the dependencies the GIMP Dev build process needs. By using that information we can make a bash script to install those packages on our system. Save the following code block to a file called `install-GIMP-dep.sh` and execute it by following the instructions below.

To execute the script:

* Open a terminal in the script folder.
* Run the command `bash install-GIMP-dep.sh` to execute the script.

## Important

Be wary about executing shell scripts from the internet, have a look at the contents and try and understand roughly what it is doing. Alternatively copy it into an AI chatbot and ask _that_ what the script is doing.

```bash
#!/bin/bash

# Define the list of packages to install
PACKAGES=(
  ccache
  clang
  cmake
  lld
  valac
  desktop-file-utils
  gobject-introspection
  libgtk-3-bin
  xvfb
  pkg-config
  build-essential
  xauth
  xsltproc
  appstream
  at-spi2-core
  bison
  ffmpeg
  flex
  gettext
  gjs
  glib-networking
  graphviz
  graphviz-dev
  iso-codes
  libaa1-dev
  libappstream-glib-dev
  libarchive-dev
  libbz2-dev
  libcfitsio-dev
  libgexiv2-dev
  libgirepository1.0-dev
  libgs-dev
  libgtk-3-dev
  libgudev-1.0-dev
  libheif-dev
  libjson-glib-dev
  libjxl-dev
  liblcms2-dev
  liblzma-dev
  libmaxflow-dev
  libmng-dev
  libmypaint-dev
  libomp-dev
  libopenexr-dev
  libopenjp2-7-dev
  libpoppler-glib-dev
  libqoi-dev
  librsvg2-dev
  libsuitesparse-dev
  libtiff-dev
  libumfpack5
  libunwind-dev
  libwebp-dev
  libwmf-dev
  libxmu-dev
  libxpm-dev
  mypaint-brushes
  poppler-data
  python3
  python3-gi
  python3-gi-cairo
  hicolor-icon-theme
  shared-mime-info
  libgl1-mesa-dev
  libgl1-mesa-dri
  libegl1-mesa-dev
  git
  meson
  gi-docgen
  ghostscript
  libdbus-glib-1-dev
  libexif-dev
  libraw20
  libtiff5-dev
  libtool
  luajit
  xz-utils
  yelp-tools
)

# Define a function to install a package and report failure
install_package() {
  local package="$1"
  if sudo apt-get install -y "$package"; then
    echo "Installed $package"
  else
    FAILED_PACKAGES+=("$package")
  fi
}

# Initialize the list of failed packages
FAILED_PACKAGES=()

# Loop through the packages and install them
for package in "${PACKAGES[@]}"; do
  install_package "$package"
done

# Print a summary of the installation
echo ""
echo "Installation Summary:"
echo "---------------------"
echo "Installed packages: ${#PACKAGES[@]}"
echo "Failed packages: ${#FAILED_PACKAGES[@]}"
if [ ${#FAILED_PACKAGES[@]} -gt 0 ]; then
  echo "Failed packages:"
  for package in "${FAILED_PACKAGES[@]}"; do
    echo "  $package"
  done
fi

read -n 1 -r -s -p "Press any key to exit"
```

## Install Location

After the Git challenge and package installation, we can proceed with the task. We'll keep the files we need in repository folders on the hard-drive, it's good to call the root folder `code`, then put in a sub-folder, like `gnome`, then another sub-folder `build` and one called `bash`

* Home
  * code
    * bash
    * gnome
      * build

These shell commands will create that little structure when run in a terminal, or you can do it using the File Manager.

```shell
mkdir $HOME/code
mkdir $HOME/code/bash
mkdir $HOME/code/gnome
mkdir $HOME/code/gnome/build
```

We are now ready to download from the internet, the source code files we need for our build environment. These files will be _cloned_ from existing repositories using Git and GitLab addresses.

## Clone the Source Code Repositories

In a terminal we can download the sources to our build directory using the `git clone` command:

```shell
cd $HOME/code/gnome/build
git clone https://gitlab.gnome.org/GNOME/babl
git clone https://gitlab.gnome.org/GNOME/gegl
git clone https://gitlab.gnome.org/GNOME/gimp
git clone https://gitlab.gnome.org/pixelmixer/artbox.git
```

The simple folder structure is now populated with thousands of files, and there's more to be made automatically by the build process.

* Home
  * code
    * bash
    * gnome
      * build
        * babl
        * gegl
        * gimp
        * artbox

## Environment Variables

The software that is about to be built, needs to know a few things about its environment. We do this by exporting some environmental variables. Copy the following into a file, call it **build_env.sh** and save it in the `bash` folder.

```bash
#!/usr/bin/env bash
export GIMP_PREFIX="${HOME}/code/gnome"
export PATH="$GIMP_PREFIX/bin:$PATH"

# Capture the multi-os-directory
multi_os_directory=$(gcc -print-multi-os-directory 2>/dev/null)
if echo "$multi_os_directory" | grep ./ > /dev/null; then
  LIB_DIR=$(echo "$multi_os_directory" | sed 's/\.\.\///g')
else
  LIB_DIR="lib"
fi

# Capture the multiarch
multiarch=$(gcc -print-multiarch 2>/dev/null)
if echo "$multiarch" | grep . > /dev/null; then
  LIB_SUBDIR="${multiarch}/"
else
  LIB_SUBDIR=""
fi

# Export environment variables
export PKG_CONFIG_PATH="${GIMP_PREFIX}/${LIB_DIR}/${LIB_SUBDIR}pkgconfig${PKG_CONFIG_PATH:+:$PKG_CONFIG_PATH}"
export LD_LIBRARY_PATH="${GIMP_PREFIX}/${LIB_DIR}/${LIB_SUBDIR}${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}"
export XDG_DATA_DIRS="${GIMP_PREFIX}/share:/usr/share${XDG_DATA_DIRS:+:$XDG_DATA_DIRS}"
export GI_TYPELIB_PATH="${GIMP_PREFIX}/${LIB_DIR}/${LIB_SUBDIR}girepository-1.0${GI_TYPELIB_PATH:+:$GI_TYPELIB_PATH}"

# Hardware acceleration support
if [ -d "/usr/lib/${LIB_SUBDIR}dri" ]; then
    export LIBGL_DRIVERS_PATH="/usr/lib/${LIB_SUBDIR}dri"
fi

# Enable Mesa threaded rendering for better performance
export mesa_glthread=true

# Ensure proper graphics context
export DISPLAY=${DISPLAY:-:0}

# Compiler configuration (use clang for better performance)
export CC="ccache clang"
export CXX="ccache clang++"
export CC_LD="lld"
export CXX_LD="lld"

# Add ccache to PATH for faster rebuilds
export PATH="/usr/lib/ccache:$PATH"
```

## Build Environment Optimizations

The updated environment configuration includes several optimizations that improve build performance and align with the CI environment. **Note**: Artbox will work fine without these optimizations, but they provide better development experience and consistency.

**Build Optimizations:**
- **Clang compiler with LLD linker**: Faster compilation and linking compared to GCC
- **ccache optimization**: Speeds up rebuilds by caching compiled objects
- **Mesa threading**: Enables multi-threaded OpenGL rendering (performance enhancement)
- **Graphics driver paths**: Explicit configuration for consistency with CI builds

**Why These Matter:**
- Faster development iteration with quicker builds
- Better graphics performance during development testing
- Consistent behavior between local builds and distributed AppImage
- Alignment with official build environment

**Compatibility Note:** These settings match the official Artbox AppImage build environment, ensuring your local build behaves identically to the distributed version.

### OpenCL Acceleration (Experimental)

Artbox includes optional OpenCL acceleration for certain graphics operations, accessible through **Edit → Preferences → Experimental Playground → Use OpenCL**.

**Important Warnings:**
- **Experimental status**: OpenCL support is unfinished and may cause crashes
- **Performance**: May actually slow down operations rather than accelerate them
- **Stability**: Expect potential application instability when enabled

**Technical Details:**
- OpenCL acceleration operates through GEGL (the graphics processing library)
- Only affects "some operations" rather than comprehensive acceleration
- Requires compatible OpenCL drivers (Intel, AMD, or NVIDIA)

**Recommendation:** Leave OpenCL disabled unless you're specifically testing experimental features. The Mesa DRI hardware acceleration configured in the environment provides better stability and performance for most users.

## Build Artbox, BABL and GEGL

To build the software, we can use another shell script, that uses this file to build or compile the software. Copy the following and save it as `artbox.sh` in the bash folder. Then in your File Manager, right click the artbox.sh file, properties, permissions, `Allow executing file as program`.

Notice that BABL and GEGL are also being built, these two additional packages don't have to be built every time. When
COMPILE_ONLY is set to "true", after a full build perhaps, they are skipped.

```shell
#!/usr/bin/env bash
# This script automates the build process for either Artbox (a GIMP fork) or
# GIMP itself. It includes optional steps to build libraries like BABL and GEGL
# It DEPENDS on "build_env.sh" being available in the same script directory

# Default configuration
COMPILE_ONLY="false"    # Set to "true" to compile without a full build

BUILD_BABL="true"       # Set to "false" to skip building BABL
BUILD_GEGL="true"       # Set to "false" to skip building GEGL
BUILD_FORK="artbox"     # Set to "gimp"  to build GIMP instead

# This automatically finds the directory where this script is located
SCRIPT_DIR="$(dirname "$(realpath "$0")")"

# This saves the initial directory to return to it later
INITIAL_DIR="$(pwd)"

# Load the environment variables
source "$SCRIPT_DIR/build_env.sh"

# Start in the build directory
cd "${GIMP_PREFIX}/build/"

# A fast compile if requested, skip other the other builds
if [ "$COMPILE_ONLY" == "true" ]; then
  echo -e "\n*** Compiling $BUILD_FORK ***\n"

  # Update the git submodule for the chosen fork
  cd "${GIMP_PREFIX}/build/$BUILD_FORK"
  git submodule update --init

  # Create and navigate to the build directory
  mkdir -p "${GIMP_PREFIX}/build/$BUILD_FORK/_build"
  cd "${GIMP_PREFIX}/build/$BUILD_FORK/_build"

  # Run Ninja to compile
  ninja
  ninja install

  echo -e "\n*** Finished compiling $BUILD_FORK ***\n"

  # Return to the initial directory and pause before the exit
  cd "$INITIAL_DIR"
  sleep 3

  exit 0 # Early exit after compiling
fi

# Build BABL if enabled
if [ "$BUILD_BABL" == "true" ]; then
  echo -e "\n*** Building BABL ***\n"

  # Create and navigate to the build directory for BABL
  mkdir -p babl/_build
  cd babl/_build

  # Run Meson setup and build commands
  meson setup .. -Dprefix="${GIMP_PREFIX}"  --buildtype="release"
  ninja
  ninja install

  echo -e "\n*** Finished building BABL ***\n"
  cd "${GIMP_PREFIX}/build/"
fi

# Build GEGL if enabled
if [ "$BUILD_GEGL" == "true" ]; then
  echo -e "\n*** Building GEGL ***\n"

  # Create and navigate to the build directory for GEGL
  mkdir -p gegl/_build
  cd gegl/_build

  # Run Meson setup and build commands
  meson setup .. -Dprefix="${GIMP_PREFIX}" --buildtype="release"
  ninja
  ninja install

  echo -e "\n*** Finished building GEGL ***\n"
  cd "${GIMP_PREFIX}/build/"
fi

# Build the chosen version of GIMP (Artbox or GIMP)
echo -e "\n*** Building $BUILD_FORK ***\n"

# Update the git submodule for the chosen fork
cd "${GIMP_PREFIX}/build/$BUILD_FORK"
git submodule update --init

# Create and navigate to the build directory
mkdir -p "${GIMP_PREFIX}/build/$BUILD_FORK/_build"
cd "${GIMP_PREFIX}/build/$BUILD_FORK/_build"

# Run Meson setup and build commands with modern options
meson setup .. -Dprefix="${GIMP_PREFIX}" --buildtype="debugoptimized" -Dvector-icons=true -Dcheck-update=yes
ninja
ninja install

echo -e "\n*** Finished building $BUILD_FORK ***\n"

# Return to the initial directory and pause before the exit
cd "$INITIAL_DIR"
sleep 3
```

To run the build script you can open a terminal in the bash folder and enter: `bash artbox.sh`

## Run Artbox

To run the software, we use a shell script. Copy the following and save it as `artbox-run.sh` in the bash folder. Then in your File Manager right click the artbox-run.sh file, properties, permissions, `Allow executing file as program`.

```bash
#!/usr/bin/env bash
# Launches Artbox

# This automatically finds the directory where this script is located
SCRIPT_DIR="$(dirname "$(realpath "$0")")"

# Load the environment variables
source "$SCRIPT_DIR/build_env.sh"

# The current version of the exe we built that can be found in ${GIMP_PREFIX}/bin/
export GIMP_VERSION="3.1"

# Launch command based on the build version
"${GIMP_PREFIX}/bin/gimp-${GIMP_VERSION}"
```

## Desktop Launcher (System Specific)

You can launch Artbox using a desktop launcher. Save the following as a file to your desktop, then right click it, go to Properties, Permissions, and check "Allow executing file as program".

```ini
[Desktop Entry]
Exec=gnome-terminal -- /home/your-home/code/bash/artbox-run.sh
Terminal=True
Icon=/home/your-home/code/gnome/build/artbox/gimp-data/images/logo/artbox-logo.svg
Type=Application
Name=Artbox
```

Change `your-home` to your actual username or home directory. For example:

```ini
Exec=gnome-terminal -- /home/mark/code/bash/artbox-run.sh
Icon=/home/mark/code/gnome/build/artbox/gimp-data/images/logo/artbox-logo.svg
```

### Using the Artbox Logo and Desktop Integration Files

When you build and install Artbox, the build process provides files for desktop integration:

- Logo: `${GIMP_PREFIX}/share/artbox/logos/artbox-logo.svg`
- Desktop launcher template and instructions: `${GIMP_PREFIX}/share/artbox/desktop-integration/README.md` and `artbox.desktop`

For development builds, you can use the logo directly from the source tree:
```
Icon=/home/your-home/code/gnome/build/artbox/gimp-data/images/logo/artbox-logo.svg
```

You can also use a generic system icon:
```
Icon=applications-graphics
```

To set up a launcher:
1. Copy the template:
   ```bash
   cp ${GIMP_PREFIX}/share/artbox/desktop-integration/artbox.desktop ~/.local/share/applications/artbox.desktop
   ```
2. Edit the file to set the correct executable path and icon location.
3. Save it to both your desktop (for quick access) and to `~/.local/share/applications/artbox.desktop` (so your Linux desktop environment can recognize and list Artbox in your application menu or search).
4. Make the file executable:
   - Terminal:
     ```bash
     chmod +x ~/Desktop/artbox.desktop
     chmod +x ~/.local/share/applications/artbox.desktop
     ```
   - GUI: Right-click the file, Properties, Permissions, check "Allow executing file as program"

For more details or troubleshooting, see the README.md file in the desktop-integration directory.

## Automatically Updating to the Latest Development Version

To update Artbox or GIMP to the latest development version, you can perform a 'hard' reset of the local repository to match the remote repository. **Warning:** This process will overwrite any local changes you have made to the code.

Here is a script that will get the latest versions of GIMP, Artbox, BABL and GEGL. Copy the following and save it as `reset-all-repos.sh` in the bash folder. Then in your File Manager, right click the `reset-all-repos.sh` file, properties, permissions, `Allow executing file as program`.

```bash
#!/usr/bin/env bash
# This script resets all the specified repositories (babl, gegl, artbox, and gimp)
# to their original states using 'git reset --hard', 'git clean -df', and ensures
# they are reset to the latest changes from their respective branches ('master' or 'artbox').
# If it's the gimp or artbox repo, a submodule update will be performed.
# It DEPENDS on "build_env.sh" being available in the same script directory.

# Flags to control whether to reset each repository
RESET_BABL="true"
RESET_GEGL="true"
RESET_GIMP="true"
RESET_ARTBOX="true"

# This automatically finds the directory where this script is located
SCRIPT_DIR="$(dirname "$(realpath "$0")")"

# This saves the initial directory to return to it later
INITIAL_DIR="$(pwd)"

# Load the environment variables
source "$SCRIPT_DIR/build_env.sh"

# Start in the build directory
cd "${GIMP_PREFIX}/build/"

# Positive warning message
echo "This script will reset selected repositories (babl, gegl, artbox, gimp) to their latest versions."
echo "Programmers! All uncommitted changes and untracked files will be lost."
echo -e "\nAre you sure you want to continue? (y)"

# User prompt
read -r CONFIRM

# Only proceed if the user confirms
if [ "$CONFIRM" != "y" ]; then
  echo "Operation canceled by the user."
  cd "$INITIAL_DIR"
  exit 1
fi

# Define the paths to the repositories and their respective branches
REPOS=()

if [ "$RESET_BABL" == "true" ]; then
  REPOS+=("${GIMP_PREFIX}/build/babl master")
fi
if [ "$RESET_GEGL" == "true" ]; then
  REPOS+=("${GIMP_PREFIX}/build/gegl master")
fi
if [ "$RESET_GIMP" == "true" ]; then
  REPOS+=("${GIMP_PREFIX}/build/gimp master")
fi
if [ "$RESET_ARTBOX" == "true" ]; then
  REPOS+=("${GIMP_PREFIX}/build/artbox artbox")
fi

# Loop through each repository, reset, clean, checkout branch, and fetch the latest changes
for REPO_INFO in "${REPOS[@]}"; do
  REPO=$(echo "$REPO_INFO" | awk '{print $1}')
  BRANCH=$(echo "$REPO_INFO" | awk '{print $2}')

  # Check if the repository exists
  if [ ! -d "$REPO" ]; then
    echo -e "Repository $REPO does not exist, skipping"
    continue
  fi

  # Navigate to the repository
  if cd "$REPO"; then
    # Checkout the correct branch
    git checkout -q "$BRANCH"
    # Fetch the latest changes from origin
    git fetch origin -q
    # Perform git reset and clean
    git reset --hard -q origin/"$BRANCH"
    git clean -df -q
    echo -e "Repository $REPO has been reset to the latest state on branch $BRANCH\n"

    # If the repository is gimp or artbox, perform a submodule update
    if [[ "$REPO" == *"gimp"* || "$REPO" == *"artbox"* ]]; then
      git submodule update --init --recursive -q
    fi
  else
    echo -e "Failed to navigate to $REPO"
  fi
done

# Return to the initial directory
cd "$INITIAL_DIR"
echo -e "Remember to rebuild all the repos to get the latest versions of the app!\n"
```

### Post Update

After running this script the next thing to do would be run the `artbox.sh` script with the control flags set as:

```plaintext
COMPILE_ONLY="false"
BUILD_BABL="true"
BUILD_GEGL="true"
BUILD_FORK="artbox"
```

Then the version of Artbox will be the latest one to play with, and it'll be using the latest BABL and GEGL.

## Steps to Manually Update

1. **Navigate to the Local Repository:** First, go to the directory of the repository you want to update.
2. **Checkout the Desired Branch:** Switch to the branch you want to update. Make sure this is the branch you intend to reset.
3. **Fetch the Latest Data:** Retrieve the latest changes from the remote repository (origin).
4. **Reset to the Remote Branch:** Perform a hard reset to align your local branch with the remote branch. This will discard any local changes.
5. **Rebuild:** Repeat the [building](#build-artbox-babl-and-gegl) process by running the 'artbox.sh' script.

**Example commands to reset the artbox branch of the Artbox repo:**

```bash
cd ${HOME}/code/gnome/build/artbox/
git checkout artbox
git fetch origin
git reset --hard origin/artbox
```

### Explanation of Commands

* `git checkout artbox`: Switches to the 'artbox' branch. Replace 'artbox' with the name of the branch you want to update if different.

* `git fetch origin`: Downloads the latest changes from the remote repository (`origin`) but does not merge them into your local branch.

* `git reset --hard origin/artbox`: Resets your current branch to match the state of the `origin/artbox` branch. This is a 'hard' reset, meaning any local changes will be lost.

## Troubleshooting

### Graphics Performance Issues

If Artbox feels slow or unresponsive during canvas operations:

1. **Check hardware acceleration status:**
   ```bash
   glxinfo | grep -E "(OpenGL vendor|OpenGL renderer|direct rendering)"
   ```
   You should see "direct rendering: Yes" and your GPU listed as the renderer.

2. **Verify DRI drivers are installed:**
   ```bash
   ls /usr/lib/x86_64-linux-gnu/dri/
   ```
   This should show driver files like `i965_dri.so` (Intel) or `radeonsi_dri.so` (AMD).

3. **Check environment variables are set:**
   ```bash
   echo $LIBGL_DRIVERS_PATH
   echo $mesa_glthread
   ```

### OpenCL Issues

**If you enabled OpenCL acceleration and experience problems:**

- **Application crashes**: Disable OpenCL in **Edit → Preferences → Experimental Playground**
- **Slower performance**: OpenCL may not be beneficial for your hardware/workload combination
- **Check OpenCL support**: Verify your graphics drivers support OpenCL:
  ```bash
  clinfo
  ```
  Install `clinfo` if needed: `sudo apt install clinfo`

**OpenCL compatibility:**
- **Intel GPUs**: Requires `intel-opencl-icd` package
- **AMD GPUs**: Requires `mesa-opencl-icd` or `rocm-opencl-runtime`
- **NVIDIA GPUs**: Requires proprietary drivers with OpenCL support

**Recommendation**: Keep OpenCL disabled unless specifically needed for testing.

### Build Issues

**Common problems and solutions:**

- **Missing dependencies**: Re-run the dependency installation script if meson setup fails
- **ccache issues**: Clear ccache with `ccache -C` if you get strange compilation errors
- **Linker errors with clang**: Ensure `lld` package is installed: `sudo apt install lld`
- **Submodule problems**: Run `git submodule update --init --recursive` in the artbox directory

### Performance Optimization

For the best development experience:

- Use an SSD for source code storage
- Allocate sufficient RAM (8GB+ recommended)
- Consider using `--buildtype=release` for final testing builds
- Monitor ccache hit rates with `ccache -s`

## Conclusion

At this point you will have the source code for Artbox, a build script and a desktop launcher. Double clicking the launcher should see a terminal and Artbox will open. There are many ways to make a build script, this is a starting point. If you got this far, congratulations!
