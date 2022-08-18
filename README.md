# dashsubmodule - Example project of using DASH as a Git Submodule

This mini-project is the simplest example of importing [Azure/DASH project](https://github.com/Azure/DASH) as  Git Submodule into a "parent project." I followed the "[Quick-Start" ](https://github.com/chrispsommers/DASH/blob/doc-dash-as-submodule/dash-pipeline/README-dash-as-submodule.md#quick-start)instructions documented in the DASH repo. No customization was done. The only objective was to perform the importing and commit the `.gitmodules` and `DASH/` items.
>**TODO** Change URLs to upstream branch when merged).

You can clone this project and do the following to recreate the state of my project and perform a local sanity-check. It will result with the DASH submodule cloned, docker images pulled and all community DASH artifacts built.

```
git clone https://github.com/chrispsommers/dashsubmodule
cd dashsubmodule
make -f Makefile.3rdpty clean
make -f Makefile.3rdpty all
make -f Makefile.3rdpty dash-pipeline-regression
```
To run the community switch and saithrift tests as another sanity check. It will confirm your environment can perform SW traffic-generator tests with the DASH bmv2 pipeline, which is a good jump-off point for third-party integration and customization.

You can "jump into" the DASH/dash-pipeline "environment" any time as a way to cross-check your own third-party efforts, all in the comfort of your parent project workspace.
```
cd DASH/dash-pipeline
make run-switch         # console 1
make saithrift-server   # console 2
make run-all-tests      # console 3
make kill-all           # console 3 
```