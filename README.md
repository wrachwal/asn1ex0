ASN1ex0
=======

ASN.1 compiler mix task using patched version of `asn1ct`.

Patched `asn1ct` generates additional database file with `.asn1db.0`
extension. This database contains 'pure' AST of ASN.1 definitions.

The original database `.asn1db` left by the compiler corresponds to
a state where definitions read-in from ASN.1 sources have been
transformed in some way during a consistency checks pass before code
generation. Such transformations, undoubtedly helpful in the process
of the checks, makes the resulting database very hard or impossible
to use for purposes other than default code generation done by the
compiler.  The Erlang documentation is clear in that _(intermediate
format used by the compiler)_, but well, one cannot afford for such
wonderful pieces of software as `asn1ct` is, to be used only in one
obvious context, while armed with knowledge about ASN.1 and having
Elixir macros, we can drag some heavy tasks to the compile-time
space.

At the moment `.asn1db.0` is generated unconditionally - there is no
option to control that.

Mix task part if based on
[`asn1ex`](https://github.com/vicentfg/asn1ex.git) project.

## Configuration

Add the following line on the project function of mix.exs file:

- `compilers: [:asn1] ++ Mix.compilers`

and asn1ex0 as a dependency:

- `{:asn1ex0, git: "https://github.com/wrachwal/asn1ex0.git"}`

Other configuration options:

- `:asn1_paths` - directories to find source files. Defaults to `["asn1"]`.

- `:erlc_paths` - directories to store generated source files. Defaults to
  `["src"]`.

- `:asn1_options` - compilation options that apply to ASN.1's compiler. There
  are many other available options here:
  http://erlang.org/doc/man/asn1ct.html#compile-2.
