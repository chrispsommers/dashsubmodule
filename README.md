# dashsubmodule - Example project of using DASH as a Git Submodule

This mini-project is the simplest example of importing [Azure/DASH project](https://github.com/Azure/DASH) as  Git Submodule into a "parent project." I followed the [Quick-Start](https://github.com/chrispsommers/DASH/blob/doc-dash-as-submodule/dash-pipeline/README-dash-as-submodule.md#quick-start) instructions documented in the DASH repo. No customization was done. The only objective was to perform the importing and commit the `.gitmodules` and `DASH/` items.
>**TODO** Change URLs to upstream branch when merged).

# Step 1: Regression-test of Community DASH Submodule
You can clone this project and do the following to replicate this project and perform a local sanity-check. It will clone DASH submodule, pull docker images and build all community DASH artifacts. You won't necessarily use them in your parent project but it ensures a good starting point. Once you feel confident, you can follow the [Quick-Start](https://github.com/chrispsommers/DASH/blob/doc-dash-as-submodule/dash-pipeline/README-dash-as-submodule.md#quick-start) instructions in your own Git project.
## Build dash-pipeline
```
git clone https://github.com/chrispsommers/dashsubmodule
cd dashsubmodule
make -f Makefile.3rdpty dash-pipeline-clean
make -f Makefile.3rdpty dash-pipeline-regression
```

The two make commands above are equivalent to running the `make clean && make all` commands under `DASH/dash-pipeline`.

## Test dash-pipeline
This runs the community switch and saithrift tests as another sanity check. It will confirm your environment can perform SW traffic-generator tests with the DASH bmv2 pipeline, which is a good jump-off point for third-party integration and customization.

You can descend into the submodule, i.e. the DASH/dash-pipeline "workspace," any time, as a way to cross-check your own third-party efforts, all in the convenience of your parent project's workspace. Put another way: changing into the DASH submodule directory is (nearly) identical to working within a separately cloned copy of DASH.
```
cd DASH/dash-pipeline
make run-switch         # console 1
make saithrift-server   # console 2
make run-all-tests      # console 3
make kill-all           # console 3 
```
# Step 2: Run Skeletal Custom "make all"
To execute a skeletal build which is the precursor to  integration of community DASH build workflows and your own, do this:
```
make -f Makefile.3rdpty clean
make -f Makefile.3rdpty all
```

This will build artifacts such as P4Info, SAI headers etc. and print placeholder messages where customization is required. Below is a representative output:
```
...various build steps...

make[1]: Leaving directory '/home/chris/dashsubmodule/DASH/dash-pipeline'
Build third-pary libsai
   Put libsai.so under DASH/dash-pipeline/SAI/lib
   For use by saithrift-server build stage.
Build third-party saithrift-server
   Expects libsai.so under DASH/dash-pipeline/SAI/lib
# For reference:
# make -C DASH/dash-pipeline saithrift-server
Build third-pary saithrift-client
   Expects saithrift-server already built
# Uncomment when saithrift server can be built
# make -C DASH/dash-pipeline docker-saithrift-client
```
# Step3: Customize the Makefile
Use this as a starting point to build your custom build workflows by editing the makefiles etc. Follow the general advice in the [README-dash-as-submodule](https://github.com/chrispsommers/DASH/blob/doc-dash-as-submodule/dash-pipeline/README-dash-as-submodule.md) document.