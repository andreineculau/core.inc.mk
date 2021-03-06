# core.inc.mk

I make (pun) a lot of things, and I want to keep them DRY.

The `docs` folder has some tips and tricks as well.

# Usage

I would have this repository as a submodule e.g. as a `core.inc.mk` folder,
and then fetch the submodule, if not already there,
and reference it at the top of the real `Makefile`,
just after setting the `TOP` (root path for the current project):

```make
ifeq (,$(wildcard core.inc.mk/Makefile))
INSTALL_CORE_INC_MK := $(shell git submodule update --init --recursive core.inc.mk)
ifneq (,$(filter undefine,$(.FEATURES)))
undefine INSTALL_CORE_INC_MK
endif
endif

TOP := $(abspath $(shell dirname $(lastword $(MAKEFILE_LIST))))
include core.inc.mk/Makefile
```

Similarly, if I just want bits and pieces of this:

```make
ifeq (,$(wildcard core.inc.mk/Makefile))
INSTALL_CORE_INC_MK := $(shell git submodule update --init --recursive core.inc.mk)
ifneq (,$(filter undefine,$(.FEATURES)))
undefine INSTALL_CORE_INC_MK
endif
endif

include core.inc.mk/core.inc.mk
include core.inc.mk/target.help.inc.mk
```

# Ref

* http://blog.jgc.org/2013/02/updated-list-of-my-gnu-make-articles.html
* https://tech.davis-hansson.com/p/make/

# License

[Unlicense](LICENSE)
