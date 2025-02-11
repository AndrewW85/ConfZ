.. _sources_loaders:

Config Sources and Loaders
==========================

Config Sources
--------------

A :class:`~confz.ConfZSource` is a dataclass describing how to load config values from a certain source. It serves
as instructions for the corresponding :class:`~confz.loaders.Loader`.

There are multiple config sources which support a heterogeneous set of use-cases:

- :class:`~confz.ConfZFileSource` allows to load config data from files. Currently, yaml- and json-format is supported.
  The filename can either be passed directly, via environment variable or via command line argument. The latter cases
  allow to easily configure multiple environments by having a separate file for each environment.
- :class:`~confz.ConfZEnvSource` allows to load config data from environment variables and .env files. It supports to
  select the corresponding variables with allow- and deny-lists and with an optional prefix. The variable names are
  either inferred from the config name or can be explicitly mapped.
- :class:`~confz.ConfZCLArgSource` allows to load config data from command line arguments. An optional prefix allows
  to select only parts of the arguments. The argument names are either inferred from the config name or can be
  explicitly mapped.
- :class:`~confz.ConfZDataSource` allows to define constant config data. This can be very useful for unit tests, see
  :ref:`context_manager`.

Furthermore, it is possible to define your own sources with a corresponding loader, see :ref:`extending-confz`.


Loading Order
-------------

When defining config sources as keyword argument or class variable, it is possible to either provide a single source
or a list of sources. In the latter case, config sources are loaded in the same order as in this list and later config
values can override earlier ones.

If keyword arguments are provided to the constructor of a config class, they are read at the beginning and thus can
be overridden by any config source.
