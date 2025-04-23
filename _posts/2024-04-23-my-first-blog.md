---

layout: post
title: "how to install scitools understand in linux and using its api"
date: 2025-04-23

tags: [Debug]

---

# Abstract

The blog share some debug experience of install scitools understand in linux.

# Details

The following link basically tell you what to do.

https://support.scitools.com/support/solutions/articles/70000583180-running-understand-on-a-headless-linux-server

However, you may encounter some other problems.

For me, I struggled to set the environment and can only run the understand api in shell files.

I present the shell code that works for me here.

```bash
# SET THE LICENSE
#!/bin/bash

# Remove CUDA paths from library path
export LD_LIBRARY_PATH=$(echo $LD_LIBRARY_PATH | tr ':' '\n' | grep -v "cuda-12.2" | tr '\n' ':')

# Add Python and Perl lib paths explicitly
export PYTHON_LIB_PATH="/home/caesar/.local/share/understand/bin/linux64/Python/lib"
export PERL_LIB_PATH="/home/caesar/.local/share/understand/bin/linux64/Perl"

# Prioritize Understand's libraries (including Python and Perl lib paths)
export LD_LIBRARY_PATH="${PYTHON_LIB_PATH}:${PERL_LIB_PATH}:/home/caesar/.local/share/understand/bin/linux64:/home/caesar/.local/share/understand/bin/linux64/lib:${LD_LIBRARY_PATH}"

# Set Qt-specific environment variables
export QT_PLUGIN_PATH="/home/caesar/.local/share/understand/bin/linux64/plugins" 
export QT_QPA_PLATFORM_PLUGIN_PATH="/home/caesar/.local/share/understand/bin/linux64/plugins/platforms"
export QT_QPA_PLATFORM=offscreen

# Preload Understand's Qt DBus library and Perl library to ensure symbols are found
export LD_PRELOAD="/home/caesar/.local/share/understand/bin/linux64/Perl/libperl.so:/home/caesar/.local/share/understand/bin/linux64/libQt6DBus.so.6"

# Set the license code
/home/caesar/.local/share/understand/bin/linux64/und -setlicensecode [your license code]

```

```bash
# RUN THE MAIN FUNC
# Remove CUDA paths from library path
export LD_LIBRARY_PATH=$(echo $LD_LIBRARY_PATH | tr ':' '\n' | grep -v "cuda-12.2" | tr '\n' ':')

# Add Python and Perl lib paths explicitly
export PYTHON_LIB_PATH="/home/caesar/.local/share/understand/bin/linux64/Python/lib"
export PERL_LIB_PATH="/home/caesar/.local/share/understand/bin/linux64/Perl"

# Prioritize Understand's libraries (including Python and Perl lib paths)
export LD_LIBRARY_PATH="${PYTHON_LIB_PATH}:${PERL_LIB_PATH}:/home/caesar/.local/share/understand/bin/linux64:/home/caesar/.local/share/understand/bin/linux64/lib:${LD_LIBRARY_PATH}"

# Set Qt-specific environment variables
export QT_PLUGIN_PATH="/home/caesar/.local/share/understand/bin/linux64/plugins" 
export QT_QPA_PLATFORM_PLUGIN_PATH="/home/caesar/.local/share/understand/bin/linux64/plugins/platforms"
export QT_QPA_PLATFORM=offscreen

# Preload Understand's Qt DBus library and Perl library to ensure symbols are found
export LD_PRELOAD="/home/caesar/.local/share/understand/bin/linux64/Perl/libperl.so:/home/caesar/.local/share/understand/bin/linux64/libQt6DBus.so.6"

# Modify your script to avoid loading the Qt GUI components entirely
export UNDERSTAND_NO_GUI=1

# Print paths to verify
echo "Python library path: ${PYTHON_LIB_PATH}"
ls -la ${PYTHON_LIB_PATH}/libpython3.13.so* 2>/dev/null || echo "Python library not found in expected location"
echo "Perl library path: ${PERL_LIB_PATH}"
ls -la ${PERL_LIB_PATH}/libperl.so 2>/dev/null || echo "Perl library not found in expected location"

# Run your Python script directly with the API, avoiding the GUI initialization
/home/caesar/.local/share/understand/bin/linux64/Python/bin/python3.13 /home/caesar/caesar/Diasplus/dataset_construction/use_understand_to_analyze_call_graph/repo_analyze_python_version/main_py_version.py
```
