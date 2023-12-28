![PadoGrid](https://github.com/padogrid/padogrid/raw/develop/images/padogrid-3d-16x16.png) [*PadoGrid*](https://github.com/padogrid) | [*Catalogs*](https://github.com/padogrid/catalog-bundles/blob/master/all-catalog.md) | [*Manual*](https://github.com/padogrid/padogrid/wiki) | [*FAQ*](https://github.com/padogrid/padogrid/wiki/faq) | [*Releases*](https://github.com/padogrid/padogrid/releases) | [*Templates*](https://github.com/padogrid/padogrid/wiki/Using-Bundle-Templates) | [*Pods*](https://github.com/padogrid/padogrid/wiki/Understanding-Padogrid-Pods) | [*Kubernetes*](https://github.com/padogrid/padogrid/wiki/Kubernetes) | [*Docker*](https://github.com/padogrid/padogrid/wiki/Docker) | [*Apps*](https://github.com/padogrid/padogrid/wiki/Apps) | [*Quick Start*](https://github.com/padogrid/padogrid/wiki/Quick-Start)

---

# KB-KITE (Kallisto Indexing and Tag Extraction)

This bundle provides instructions for installing `kb` for running the example notebook titled, *Pre-processing and analysis of feature barcode single-cell RNA-seq data with KITE* [1].

## Installing Bundle

```bash
install_bundle -checkout bundle-none-kb-kite
```

## Use Case

`kallisto` and `bustools` are wrapped in an easy-to-use program called `kb` which is part of the `kb-python` package (developer documentation). This bundle provides instructions for installing `kb` for running the example notebook titled, [*Pre-processing and analysis of feature barcode single-cell RNA-seq data with KITE*](https://www.kallistobus.tools/tutorials/kb_kite/python/kb_kite/) [1].

## Bundle Contents

```console
apps
└── kite
```

## Install Miniconda3 and Restart JupyterLab

First, install Miniconda3 and JupyterLab as follows.

```bash
cd $PADOGRID_ENV_BASE_PATH/downloads
curl -sSL -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh  -b -p $PADOGRID_ENV_BASE_PATH/products/miniconda3

# Initialzie minconda3
$PADOGRID_ENV_BASE_PATH/products/miniconda3/bin/conda init
. ~/.bashrc

# Install JupyterLab
conda init bash
pip install jupyterlab
```

## Restart JupyterLab 

If you are running PadoGrid in Docker/Kubernetes, restart JupyterLab as follows.

```bash
conda create -n myenv -all
conda activate myenv
conda install -y pip
conda update -y --all
pip install jupyterlab
stop_jupyter && start_jupyter -dashboard -default
```

## Install `MulticoreTSNE` from Source

Installing `MulticoreTSNE` using `pip` may throw the following error.

```console
Building wheels for collected packages: MulticoreTSNE
  Building wheel for MulticoreTSNE (setup.py) ... error
  error: subprocess-exited-with-error
  
  × python setup.py bdist_wheel did not run successfully.
  │ exit code: 1
  ╰─> [27 lines of output]
      running bdist_wheel
      running build
      running build_py
      creating build
      creating build/lib.linux-x86_64-cpython-311
      creating build/lib.linux-x86_64-cpython-311/MulticoreTSNE
      copying MulticoreTSNE/__init__.py -> build/lib.linux-x86_64-cpython-311/MulticoreTSNE
      creating build/lib.linux-x86_64-cpython-311/MulticoreTSNE/tests
      copying MulticoreTSNE/tests/__init__.py -> build/lib.linux-x86_64-cpython-311/MulticoreTSNE/tests
      copying MulticoreTSNE/tests/test_base.py -> build/lib.linux-x86_64-cpython-311/MulticoreTSNE/tests
      running egg_info
      writing MulticoreTSNE.egg-info/PKG-INFO
      writing dependency_links to MulticoreTSNE.egg-info/dependency_links.txt
      writing requirements to MulticoreTSNE.egg-info/requires.txt
      writing top-level names to MulticoreTSNE.egg-info/top_level.txt
      reading manifest file 'MulticoreTSNE.egg-info/SOURCES.txt'
      reading manifest template 'MANIFEST.in'
      adding license file 'LICENSE.txt'
      writing manifest file 'MulticoreTSNE.egg-info/SOURCES.txt'
      running build_ext
      cmake version 3.28.1
      
      CMake suite maintained and supported by Kitware (kitware.com/cmake).
      CMake Error: Unknown argument --
      CMake Error: Run 'cmake --help' for all supported options.
      
      ERROR: Cannot generate Makefile. See above errors.
      [end of output]
```

In that case, build it from the source as follows.

```
git clone https://github.com/DmitryUlyanov/Multicore-TSNE.git
cd Multicore-TSNE/
pip install .
```

If you encounter the same error, then edit `setup.py` and remove the following line.

```python
self.cmake_args or "--",
```

`MulticoreTSNE` can also be downloaded as follows.

```bash
curl -O https://files.pythonhosted.org/packages/2d/e8/2afa896fa4eebfa1d0d0ba2673fddac45582ec0f06b2bdda88108ced5425/MulticoreTSNE-0.1.tar.gz

tar xzf MulticoreTSNE-0.1.tar.gz
cd MulticoreTSNE-0.1
less README.md
```

## Startup Sequence

1. From JupyterLab, open the following notebook.

- bundle/none-kb-kite/apps/kite/kite.ipynb

## References

1. *Pre-processing and analysis of feature barcode single-cell RNA-seq data with KITE*, https://www.kallistobus.tools/tutorials/kb_kite/python/kb_kite/

---

![PadoGrid](https://github.com/padogrid/padogrid/raw/develop/images/padogrid-3d-16x16.png) [*PadoGrid*](https://github.com/padogrid) | [*Catalogs*](https://github.com/padogrid/catalog-bundles/blob/master/all-catalog.md) | [*Manual*](https://github.com/padogrid/padogrid/wiki) | [*FAQ*](https://github.com/padogrid/padogrid/wiki/faq) | [*Releases*](https://github.com/padogrid/padogrid/releases) | [*Templates*](https://github.com/padogrid/padogrid/wiki/Using-Bundle-Templates) | [*Pods*](https://github.com/padogrid/padogrid/wiki/Understanding-Padogrid-Pods) | [*Kubernetes*](https://github.com/padogrid/padogrid/wiki/Kubernetes) | [*Docker*](https://github.com/padogrid/padogrid/wiki/Docker) | [*Apps*](https://github.com/padogrid/padogrid/wiki/Apps) | [*Quick Start*](https://github.com/padogrid/padogrid/wiki/Quick-Start)
