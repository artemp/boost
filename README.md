Boost for Emscripten
====================

2 changes over standard boost:

- hardcoded paths to `emar` and `emranlib` in boost's build tools, based
  on suggestions from
  [StackOverflow](http://stackoverflow.com/questions/15724357/using-boost-with-emscripten).
  Should be possible to use the config file to do this, but I don't
  have the patience.
- Checked in `project-config.jam`, with a custom path for `g++`.  This
  path also specifies emscripten compiler flags.

To compile parts of boost for use:

```
$ ./bootstrap.sh
$ git reset --hard # to revert change to project-config.jam
$ ./b2 --link=static --ignore-site-config --with-program_options --threading=multi
#                                                ^--------------
# change the -with option above to suit your needs

To use in a cmake project:

```
$ BOOST_ROOT=$HOME/PATH/TO/boost cmake [...]
```

(you may have to clear out your build directory so that cmake doesn't
use cached values for what boost things are available)
