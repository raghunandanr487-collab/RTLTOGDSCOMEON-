# 🛣️OPENROAD 

## OpenROAD is the core application and the engine of the flow. It is a unified executable that performs the actual physical design work.


# ⏬INSTALLATION PART 

- To install the openroad you have to follow these commands very carefully,because it is liitle bit tricky.

## 🪜follow the step 

### 1️⃣step1
- Install Necessary Build Tools and GCC-9
  The default compiler version (GCC 11+) often causes internal C++ conflicts with OpenROAD's         dependencies. We force the use of GCC-9.
  
```bash
1. Update repositories and install the build essentials
sudo apt update
sudo apt install build-essential git cmake swig python3-dev -y

# 2. Install the compatible compiler (GCC-9)
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y
sudo apt update
sudo apt install g++-9 -y
```
### 2️⃣step2
- Build and Install OR-Tools (Critical Dependency)
We build and install OR-Tools to /usr/local so OpenROAD's final configuration can find it.

```bash
Clone the repository
git clone [https://github.com/google/or-tools.git](https://github.com/google/or-tools.git)
cd or-tools

# Build and install OR-Tools
mkdir build && cd build
cmake -DBUILD_DEPS=ON -DCMAKE_BUILD_TYPE=Release ..
make -j$(nproc)
sudo make install

# Navigate back to the parent directory to start OpenROAD clone
cd ../..
```
### 👿note- it is end of phase one and in next phase we will clone the openroad and both tools and openroad should built seperatly.


### 3️⃣step3

- These steps ensure a complete and clean repository, resolving initial build issues like missing submodules.
- Clone OpenROAD and Fix Submodule Corruption
- This ensures all required third-party libraries (like spdlog and sta) are fully downloaded.

```bash
# Clone OpenROAD repository (replace <path> with your chosen directory)
cd /home/iamtheking/Desktop/vlsi/vsd
git clone [https://github.com/The-OpenROAD-Project/OpenROAD.git](https://github.com/The-OpenROAD-Project/OpenROAD.git)
cd OpenROAD

# Manually clone the spdlog repository into the third-party folder
cd third-party
git clone [https://github.com/gabime/spdlog.git](https://github.com/gabime/spdlog.git)
cd ../.. 
```

### 4️⃣step4
#### Patch OpenROAD Source Files to Link spdlog

- Because we manually cloned spdlog (and commented out the system find_package), we must patch      two files to tell CMake how to link the internal files directly

- src/CMakeLists.txt (To stop searching for system package)
- Open the file: nano src/CMakeLists.txt
- Find the line find_package(spdlog REQUIRED) (around line 235) and comment it 

#### 🅱️b part

- Patch Root CMakeLists.txt (To build the dependency target)
- Open the file: nano CMakeLists.txt
- Add the line add_subdirectory(third-party/spdlog) immediately after the existing                 add_subdirectory(third-party) line, and before add_subdirectory(src).

```bash
# --- ADD THIS LINE ---
add_subdirectory(third-party/spdlog)
```


## ⚡phase3

### ✋step5
- do this in the openroad file
- Create Build Directory and Run CMake (The Solution Command)
- This command uses the required flags and compiler path to successfully configure the patched source code.

```bash
rm -rf build
mkdir build
cd build

# Run CMake (using g++-9 and pointing to OR-Tools)
cmake .. \
-DCMAKE_BUILD_TYPE=Release \
-DCMAKE_CXX_FLAGS="-Wno-error" \
-DCMAKE_PREFIX_PATH="/usr/local" \
-DCMAKE_CXX_COMPILER=/usr/bin/g++-9
```
## 🕡 step6
 - Compile and Install OpenROAD

```bash
make -j$(nproc)
sudo make install
```




