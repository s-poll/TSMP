# Debug tips

## Debug Tip 1: Skip component models in TSMP-PDAF build

``` shell
./build_tsmp.ksh -m JURECA -c clm3-cos4-pfl -W skip -X skip
```

Oasis and CLM compilation are skipped with the option `skip` for flags
`-W` and `-X`. Parflow and pdaf are compiled after Cosmo.

All flags can be found using `./build_tsmp.ksh --help`. Here, the
output for flag of component model build options:
``` shell
	-W, --optoas=optoas
                  Build option for Oasis.
                    fresh        #build from scratch in a new folder
                    build        #build clean
                    make         #only (resume) make and make install - no make clean and configure
                    configure    #only make clean and configure - no make
                    skip         #no build
                  The default value is 'fresh'.
  -E, --opticon=opticon
                  Build option for ICON. The default value is 'fresh'.
  -Y, --optcos=optcos
                  Build option for Cosmo. The default value is 'fresh'.
  -X, --optclm=optclm
                  Build option for CLM. The default value is 'fresh'.
  -Z, --optpfl=optpfl
                  Build option for Parflow. The default value is 'fresh'.
  -U, --optda=optda
                  Build option for Data Assimilation. The default value is 'fresh'.
```

## Debug Tip 2: Building TSMP-PDAF after source code changes in component models

``` shell
./build_tsmp.ksh -m JURECA -c clm3-cos4-pfl -W skip -X skip -Y make
```

Oasis and CLM compilation are skipped with the option `skip` for flags
`-W` and `-X`.

Cosmo compilation is resumed without making clean with option `make`
for flag `-Y`. The source code change needs to be made in
`cosmo4_21_JURECA_clm3-cos4-pfl`. **But note**: The source
code change will be lost after the next clean build of cosmo. Thus,
make sure to incorporate the source code changes in the designated
replace structures.

	
## Debug Tip 3: Debugging OASIS3-MCT

In `namcouple`, change the input `$NLOGPRT` to get more debug
output. More information:
<https://cerfacs.fr/oa4web/oasis3-mct_5.0/oasis3mct_UserGuide/node39.html>

## Debug Tip 4: Debugging PDAF

### PDAF Debugging Information

See the following wiki page for information about turning on PDAF
debugging output:

https://pdaf.awi.de/trac/wiki/PDAF_debugging#ActivatingDebuggingOutput

### PDAF's Timing and Memory output

`/intf_DA/pdaf/framework/finalize_pdaf.F90`: The input for the timing
information can be changed for adding more output.

See also <https://pdaf.awi.de/trac/wiki/PDAF_print_info>.
