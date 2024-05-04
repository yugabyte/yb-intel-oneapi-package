# yb-intel-oneapi-package
A repository for uploading packages of a small subset of Intel oneAPI (MKL, OpenMP libraries/headers) needed for building YugabyteDB

The package is produced using the tooling in the [yugabyte-db-thirdparty](https://github.com/yugabyte/yugabyte-db-thirdparty/) repository. It contains header files and libraries needed to build certain YugabyteDB third-party dependencies that rely on Intel MKL, OpenMP, and other libraries. As of 05/03/2024, the only such third-party dependency is the DiskANN library. Here is an example command that was used to build the first release package of yb-intel-oneapi-package.

```
./build_thirdparty.sh  --toolchain=llvm17 --skip-sanitizers --package-intel-oneapi --delete-build-dir --ignore-build-stamp diskann
```

We will refine the above command and make it more straightforward if it turns out that we need to repackage Intel oneAPI often enough.

The release could then be uploaded like so (from a yb-intel-oneapi-package repository directory):
```
cd yb-intel-oneapi-package
tag=v2024.1-1714789365
hub release create -m "Release $tag" --attach "./yb-intel-oneapi-$tag.tar.gz" --attach "./yb-intel-oneapi-$tag.tar.gz.sha256" "$tag"
```
